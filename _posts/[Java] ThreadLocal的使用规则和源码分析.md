#ThreadLocal��ʲô��

�����ֲ߳̾�����������ĳ��������ÿ���̶߳����Լ��ľֲ��������������ڱ����ĳ�ʼ������������
����
�������Ĺ��÷ǳ��򵥣�����Ϊÿһ��ʹ�øñ������̶߳��ṩһ������ֵ�ĸ�������ÿһ���̶߳����Զ����ظı��Լ��ĸ�����������������̵߳ĸ�����ͻ�����̵߳ĽǶȿ����ͺ���ÿһ���̶߳���ȫӵ�иñ�������
���� 
����ThreadLocal ʵ��ͨ�������е� private static �ֶΣ�����ϣ����״̬��ĳһ���̣߳����磬�û� ID ������ ID���������ÿ���̶߳����ֶ����ֲ߳̾�������������ʽ���ã�ֻҪ�߳��ǻ�Ĳ��� ThreadLocal ʵ���ǿɷ��ʵģ����߳���ʧ֮�����ֲ߳̾�ʵ�������и������ᱻ�������գ����Ǵ��ڶ���Щ�������������ã�����

#ThreadLocal�Ľӿڷ���

 - protected T initialValue()�������ش��ֲ߳̾������ĳ�ʼֵ

�����̵߳�һ��ʹ�� get() �������ʱ���ʱ�����ô˷�����������߳�֮ǰ������ set(T) �������򲻻�Ը��߳��ٵ��� initialValue ������ͨ�����˷�����ÿ���߳�������һ�Σ�������ڵ��� get() ���ֵ����� remove()��������ٴε��ô˷�����
������ʵ�ַ��� null���������Աϣ���ֲ߳̾��������� null �����ֵ�������Ϊ ThreadLocal �������࣬����д�˷�����ͨ����ʹ�������ڲ�����ɴ˲�����

 - public T get()�������ش��ֲ߳̾������ĵ�ǰ�̵߳�ֵ

�����������û�����ڵ�ǰ�̵߳�ֵ�����Ƚ����ʼ��Ϊ���� initialValue() �������ص�ֵ��

 - public void set(T value)���������ֲ߳̾������ĵ�ǰ�̸߳����е�ֵ����Ϊָ��ֵ

�����󲿷����಻��Ҫ��д�˷���������ֻ���� initialValue() �����������ֲ߳̾�������ֵ��

 - public void remove()�����Ƴ����ֲ߳̾�������ǰ�̵߳�ֵ

����������ֲ߳̾�������󱻵�ǰ�߳� ��ȡ�������ڼ䵱ǰ�߳�û�� ������ֵ���򽫵����� initialValue() �������³�ʼ����ֵ���⽫�����ڵ�ǰ�̶߳�ε��� initialValue ������

�����ϣ���ֲ߳̾�������ʼ������ֵ����ô��Ҫ�Լ�ʵ��ThreadLocal�����ಢ��д�÷�����ͨ��ʹ��һ���ڲ����ThreadLocal����ʵ������
��������������ӣ�SerialNum��Ϊÿһ�������һ����ţ� ��

```
public class SerialNum {
    // The next serial number to be assigned
    private static int nextSerialNum = 0;

    private static ThreadLocal serialNum = new ThreadLocal() {
        protected synchronized Object initialValue() {
            return new Integer(nextSerialNum++);
        }
    }

    public static int get() {
        return ((Integer) (serialNum.get())).intValue();
    }
}

```

#ThreadLocal���ڲ�ʵ��

�����ȿ���ThreadLocal��Ĳ���Դ�룺

```
 public class ThreadLocal<T> {
������
//ʡ��...

126    protected T initialValue() {
127        return null;
128    }


159    public T get() {
160        Thread t = Thread.currentThread();
           //��ǰ�߳�Ϊkey����ThreadLocalMap ��
161        ThreadLocalMap map = getMap(t);
162        if (map != null) {
163            ThreadLocalMap.Entry e = map.getEntry(this);
164            if (e != null) {
165                @SuppressWarnings("unchecked")
166                T result = (T)e.value;
167                return result;
168            }
169        }
170        return setInitialValue();
171    }

199    public void set(T value) {
200        Thread t = Thread.currentThread();
201        ThreadLocalMap map = getMap(t);
202        if (map != null)
203            map.set(this, value);
204        else
205            createMap(t, value);
206    }

219     public void remove() {
220         ThreadLocalMap m = getMap(Thread.currentThread());
221         if (m != null)
222             m.remove(this);
223     }


��
```

�������ǿ��Ժ����ԵĿ���ThreadLocal���̺߳��ֲ߳̾���������ThreadLocalMap�У���ThreadLocalMap��ThreadLocal�ľ�̬�ಿ�࣬����������ThreadLocalMap �Ĳ���Դ�룺

```
308        static class Entry extends ����������WeakReference<ThreadLocal<?>> {
            
309
310            Object value;
311
312           Entry(ThreadLocal<?> k, Object v) {
313                super(k);
314                value = v;
315            }
316        }
```

�������Map��key��ThreadLocal����������ã���Ҫ������ThreadLocal����ʱ�������ռ�����������key�����ö������ThreadLocal���� ��

������ô������ThreadLocal����Thread����ThreadLocalMap����������أ�

������ThreadԴ���з��֣�

```
180     /* ThreadLocal values pertaining to this thread. This map is maintained
181      * by the ThreadLocal class. */
182     ThreadLocal.ThreadLocalMap threadLocals = null;
```

����ThreadLocalMap��������Thread���ڲ�����,��ͬ��Threadӵ����ȫ��ͬ��ThreadLocalMap����.��
����
���� Thread�е�ThreadLocalMap������ֵ����ThreadLocal�������set����get����ʱ������.��
���� 
���� �ڴ���ThreadLocalMap֮ǰ,�����ȼ�鵱ǰThread�е�ThreadLocalMap�����Ƿ��Ѿ�����,����������򴴽�һ��������Ѿ�����,��ʹ�õ�ǰThread�Ѵ�����ThreadLocalMap.��
���� 
#ThreadLocal��������̰߳�ȫ

����������ķ������ǿ��Եó���

����

 - ��Ϊÿ��Thread�ڽ��ж������ʱ,���ʵĶ��Ǹ����߳��Լ���ThreadLocalMap�����Ա�֤��Thread��Thread֮������ݷ��ʸ��롣��
 
 
 - ��ͬ��ThreadLocalʵ������ͬһThreadʱ��ThreadLocalMap�ڴ洢ʱ���õ�ǰThreadLocal��ʵ����Ϊkey����֤���ݷ��ʸ��루����Դ��Entry�����Կ���������

�ٸ�����˵����

```
public class Test
{
	static ThreadLocal<Integer> local=new ThreadLocal<Integer>(){
		protected synchronized Integer initialValue(){  
            return 0;  
        }
	};  
    public static void main( String args[]){
    	 testRun t = new testRun();
    	 new Thread(t).start();
    	 new Thread(t).start();
    }
    public static  class testRun implements Runnable{
	@Override
	public void run() {
		// TODO Auto-generated method stub
		for(int i=5 ;i>0;i--){
			try {  
		        Thread.sleep(1000);  
		    } catch (InterruptedException e) {  
		        e.printStackTrace();  
		    }
			System.out.println(Thread.currentThread().getName()+"::"+local.get());
			
		     int localValue=local.get();  
		     local.set(++localValue);  
		        } 
		}
	}   
   }
```
������Ϊ��

```
Thread-0::0
Thread-1::0
Thread-0::1
Thread-1::1
Thread-1::2
Thread-0::2
Thread-1::3
Thread-0::3
Thread-0::4
Thread-1::4
```

#TheadLocalģʽ��ͬ�����Ƶ�����

 - ͬ�����Ʋ����ˡ���ʱ�任�ռ䡱�ķ�ʽ,�ṩһ�ݱ���,�ò�ͬ���߳��Ŷӷ���.��ThreadLocal�����ˡ��Կռ任ʱ�䡱�ķ�ʽ,Ϊÿһ���̶߳��ṩһ�ݱ����ĸ���,�Ӷ�ʵ��ͬʱ���ʶ�����Ӱ�졣��
 
 - Java�е�synchronized��һ��������,������JVM����������ʵ���ٽ����ĺ������߱����ķ����е�ԭ����.��ͬ��������,ͨ������������Ʊ�֤ͬһʱ��ֻ��һ���̷߳��ʱ���.��ʱ,�������������ơ��ı����Ƕ���̹߳���ģ�
 ������ThreadLocal��Ϊÿһ���߳�ά��һ���͸��̰߳󶨵ı����ĸ������Ӷ������˶���̵߳����ݣ�ÿһ���̶߳�ӵ���Լ��ı����������Ӷ�Ҳ��û�б�Ҫ�Ըñ�������ͬ���ˡ���
 ��
 - ͬ��������Ϊ��ͬ������̶߳���ͬ��Դ�Ĳ������ʣ���Ϊ�˶���߳�֮�����ͨ�ŵ���Ч��ʽ��
 ������ThreadLocal�Ǹ������̵߳����ݹ����Ӹ����ϾͲ��ڶ���߳�֮�乲����Դ����������������Ȼ����Ҫ�Զ���߳̽���ͬ���ˡ�
 �������ԣ��������Ҫ���ж���߳�֮�����ͨ�ţ���ʹ��ͬ�����ơ������Ҫ�������߳�֮��Ĺ����ͻ������ʹ��ThreadLocal��

