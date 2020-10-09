<table>
<tr>
<td bgcolor=#f4f31a>
<font color=#00aaff size=5 face="΢���ź�">
 1��ThreadPool���ŵ�
 </font>
</td>
</tr>
</table>
##  

 ������java.util.concurrent���£��ṩ��һϵ�����̳߳���ص��ࡣ�����ʹ���̳߳أ����Դ�������ô���
 ����
��1��������Դ���ġ�ͨ���ظ������Ѵ������߳̽����̴߳�����������ɵ����ģ�
��2�������Ӧ�ٶȡ������񵽴�ʱ��������Բ���Ҫ�ȵ��̴߳�����������ִ�У�
��3������̵߳Ŀɹ����ԡ��߳���ϡȱ��Դ����������ƵĴ���������������ϵͳ��Դ�����ή��ϵͳ���ȶ��ԣ�ʹ���̳߳ؿ��Խ���ͳһ�ķ��䣬���źͼ�ء�

�����̳߳ؿ���Ӧ��ͻȻ�󱬷����ķ��ʣ�ͨ�����޸��̶��߳�Ϊ�����Ĳ������񣬼��ٴ����������߳������ʱ�䡣

<table>
<tr>
<td bgcolor=#f4f31a>
<font color=#00aaff size=5 face="΢���ź�">
 1��ThreadPool�Ĵ���
 </font>
</td>
</tr>
</table>
##  

��������һ��ͨ��Executors���µ��ĸ���Ա����������Ӧ���̳߳أ�

```
//����һ����ʱ������̳߳�
ScheduledExecutorService scheduledThreadPool = Executors.newScheduledThreadPool(4);

//�������̵߳��̳߳�
ExecutorService singleThreadPool = Executors.newSingleThreadExecutor();

//���������̳߳أ�������ǰ���̣߳�
ExecutorService cachedThreadPool = Executors.newCachedThreadPool();

//����һ�����й̶��̵߳��̳߳�
ExecutorService threadPool = Executors.newFixedThreadPool(4);

```

���ǿ��Դ�Դ�뿴���������ĸ����������ThreadPoolExecutor�Ĺ��췽�������̳߳ء�

```
public static ExecutorService newFixedThreadPool(int nThreads) {
        return new ThreadPoolExecutor(nThreads, nThreads,
0L, TimeUnit.MILLISECONDS,
new LinkedBlockingQueue<Runnable>());
    }
```

����һ��ThreadPoolExecutor�̳߳�һ����Ҫ���¼���������

 - corePoolSize���̳߳صĻ�����С����
 
  �������ύһ�������̳߳�ʱ���̳߳ػᴴ��һ���߳���ִ�����񣬼�ʹ�������еĻ����߳��ܹ�ִ��������Ҳ�ᴴ���̣߳��ȵ���Ҫִ�е������������̳߳ػ�����Сʱ�Ͳ��ٴ���������������̳߳ص�prestartAllCoreThreads�������̳߳ػ���ǰ�������������л����̡߳� 

 - maximumPoolSize���̳߳�����С����

�����̳߳�������������߳���������������ˣ������Ѵ������߳���С������߳��������̳߳ػ��ٴ����µ��߳�ִ������ֵ��ע��������ʹ�����޽������������������ûʲôЧ����
 
 - keepAliveTime���̻߳����ʱ�䣩����
 ����
 �����̳߳صĹ����߳̿��к󣬱��ִ���ʱ�䡣�����������ܶ࣬����ÿ������ִ�е�ʱ��Ƚ϶̣����Ե������ʱ�䣬����̵߳������ʡ�
 - TimeUnit���̻߳����ʱ��ĵ�λ����
 
 ������ѡ�ĵ�λ���죨DAYS����Сʱ��HOURS�������ӣ�MINUTES��������(MILLISECONDS)�ȡ�
 ����
 - workQueue��������У�����

�������ڱ���ȴ�ִ�е�������������С� ����ѡ�����¼����������У�ArrayBlockingQueue��LinkedBlockingQueue��SynchronousQueue��PriorityBlockingQueue��
����
 - threadFactory����
 ����
 �����������ô����̵߳Ĺ���������ͨ���̹߳�����ÿ�������������߳����ø�����������֡���
 ����
 - handler�����Ͳ��ԣ�����
 ����
 ���������к��̳߳ض����ˣ�˵���̳߳ش��ڱ���״̬����ô�����ȡһ�ֲ��Դ����ύ���������������Ĭ���������AbortPolicy����ʾ�޷�����������ʱ�׳��쳣��

�������Ǿ�������ʹ��Executors�ṩ�ľ�̬�����������̳߳أ����Executors�ṩ�ķ����޷�����Ҫ�����Լ�ͨ��ThreadPoolExecutor���������̳߳ء�

<table>
<tr>
<td bgcolor=#f4f31a>
<font color=#00aaff size=5 face="΢���ź�">
 �������̳߳��ύ����
 </font>
</td>
</tr>
</table>
##  
�����ַ�ʽ��

�١����ǿ���ʹ��execute�ύ�����񣬵���execute����û�з���ֵ�������޷��ж������Ƿ��̳߳�ִ�гɹ���ͨ�����´����֪execute���������������һ��Runnable���ʵ����

```
threadsPool.execute(new Runnable() {
            @Override
            public void run() {
                // TODO Auto-generated method stub
            }
        });
```

�ڡ�ʹ��submit �������ύ�������᷵��һ��future,��ô���ǿ���ͨ�����future���ж������Ƿ�ִ�гɹ���ͨ��future��get��������ȡ����ֵ��get����������סֱ��������ɣ���ʹ��get(long timeout, TimeUnit unit)�����������һ��ʱ����������أ���ʱ�п�������û��ִ���ꡣ

```
Future<Object> future = executor.submit(harReturnValuetask);
try {
     Object s = future.get();
} catch (InterruptedException e) {
    // �����ж��쳣
} catch (ExecutionException e) {
    // �����޷�ִ�������쳣
} finally {
    // �ر��̳߳�
    executor.shutdown();
}
```

<table>
<tr>
<td bgcolor=#f4f31a>
<font color=#00aaff size=5 face="΢���ź�">
 �����̳߳صĹر�
 </font>
</td>
</tr>
</table>
##  

�������ǿ���ͨ�������̳߳أ�ExecutorService�Ķ��󣩵�shutdown��shutdownNow�������ر��̳߳أ����ǵ�ԭ���Ǳ����̳߳��еĹ����̣߳�Ȼ����������̵߳�interrupt�������ж��̣߳������޷���Ӧ�жϵ����������Զ�޷���ֹ���������Ǵ���һ��������shutdownNow���Ƚ��̳߳ص�״̬���ó�STOP��Ȼ����ֹͣ���е�����ִ�л���ͣ������̣߳������صȴ�ִ��������б���shutdownֻ�ǽ��̳߳ص�״̬���ó�SHUTDOWN״̬��Ȼ���ж�����û������ִ��������̡߳�

����ֻҪ�������������رշ���������һ����isShutdown�����ͻ᷵��true�������е������ѹرպ�,�ű�ʾ�̳߳عرճɹ�����ʱ����isTerminaed�����᷵��true����������Ӧ�õ�����һ�ַ������ر��̳߳أ�Ӧ�����ύ���̳߳ص��������Ծ�����ͨ������shutdown���ر��̳߳أ��������һ��Ҫִ���꣬����Ե���shutdownNow��

<table>
<tr>
<td bgcolor=#f4f31a>
<font color=#00aaff size=5 face="΢���ź�">
 �����̳߳صĹ�������
 </font>
</td>
</tr>
</table>
##  

����![����дͼƬ����](http://img.blog.csdn.net/20160519124839474)��


����ͼ���ǿ��Կ��������ύһ���������̳߳�ʱ���̳߳صĴ����������£���

1�������̳߳��жϻ����̳߳��Ƿ������� corePoolSize ��û��������һ�������߳���ִ���������ˣ�������¸����̡���

2������̳߳��жϹ��������Ƿ�������û���������ύ������洢�ڹ�����������ˣ�������¸����̡���

3������̳߳��ж������̳߳��Ƿ�������< maximumPoolSize ������û�����򴴽�һ���µĹ����߳���ִ���������ˣ��򽻸����Ͳ����������������

Ҳ����˵���̳߳�����Ҫ�����������̳߳ش�С��corePoolSize�����߳�������û�дﵽ�������ʱ��ÿ���ύ�����񶼻�ֱ�Ӵ���һ�����̣߳����ﵽ�˻����߳����������������񵽴���ȷ���ȴ����У�����������ˣ���ȥ�����µ��̣߳����ܳ����̳߳ص������maxmumPoolSize����

�����̳߳ش����߳�ʱ���Ὣ�̷߳�װ�ɹ����߳�Worker��Worker��ִ��������󣬻�������ѭ����ȡ�����������������ִ�С����ǿ��Դ�Worker��run�����￴����㣺

```
public void run() {
     try {
           Runnable task = firstTask;
           firstTask = null;
            while (task != null || (task = getTask()) != null) {
                    runTask(task);
                    task = null;
            }
      } finally {
             workerDone(this);
      }
} 
```

<table>
<tr>
<td bgcolor=#f4f31a>
<font color=#00aaff size=5 face="΢���ź�">
 �����̳߳صļ��
 </font>
</td>
</tr>
</table>
##  

����ͨ���̳��̳߳ز���д�̳߳ص�beforeExecute��afterExecute��terminated���������ǿ���������ִ��ǰ��ִ�к���̳߳عر�ǰ��һЩ���顣���������ƽ��ִ��ʱ�䣬���ִ��ʱ�����Сִ��ʱ��ȡ��⼸���������̳߳����ǿշ�����

<table>
<tr>
<td bgcolor=#f4f31a>
<font color=#00aaff size=5 face="΢���ź�">
 �����̳߳ص�����
 </font>
</td>
</tr>
</table>
##  

ʾ��һ��

```
public class DifferentKindsThreadPool {

	public static void main(String[] args) {
//		displayScheduledThreadPool();
//		displaySingleThreadPool();
//		displayCachedThreadPool();
		displayThreadPool();
	}
	
	/**
	 * ����һ����ʱ������̳߳�
	 */
	public static void displayScheduledThreadPool() {
		ScheduledExecutorService scheduledThreadPool = Executors.newScheduledThreadPool(4);
		//��������̶��̳߳�һ��ִ������
		distributeTaskForThreadPool(scheduledThreadPool);
		//������������֮�������Զ�ʱ����
		scheduledThreadPool.schedule(
				new Runnable() {
					@Override
					public void run() {
						System.out.println("��ʼִ������1");
					}
				}, 
				5, 
				TimeUnit.SECONDS);
		//ÿ��2���ٴ�����ִ������
		scheduledThreadPool.scheduleAtFixedRate(
				new Runnable() {
					@Override
					public void run() {
						System.out.println("��ʼִ������2");
					}
				}, 
				5, 
				3, 
				TimeUnit.SECONDS);
	}

	/**
	 * ����ֻ��һ���̵߳��̳߳أ�����߳���ֹ��
	 * �����ᴴ��һ���µ��̼߳��뵽�����У���
	 * ���̳߳ػᱣ֤������ʼ����һ���߳�
	 */
	public static void displaySingleThreadPool() {
		ExecutorService singleThreadPool = Executors.newSingleThreadExecutor();
		distributeTaskForThreadPool(singleThreadPool);
	}

	/**
	 * ����һ���ɸ�����Ҫ�����̵߳��̳߳أ�����
	 * ����ǰ�������߳̿ɵõ�ʱ�ͻ�������ǰ����
	 * �̣���������ڿɵõ����̣߳�һ���µ��߳�
	 * ���������������뵽�����С�60��û�б��õ�
	 * ���߳̽�����ֹ���ӻ������Ƴ�
	 */
	public static void displayCachedThreadPool() {
		ExecutorService cachedThreadPool = Executors.newCachedThreadPool();
		distributeTaskForThreadPool(cachedThreadPool);
	}

	/**
	 * ����һ�����й̶��̵߳��̳߳�
	 */
	public static void displayThreadPool() {
		// ����һ������4���̶��̵߳��̳߳�
		ExecutorService threadPool = Executors.newFixedThreadPool(4);
		distributeTaskForThreadPool(threadPool);
	}

	/**
	 * Ϊ�̳߳ط���8������ʹ������
	 * @param threadPool
	 */
	public static void distributeTaskForThreadPool(ExecutorService threadPool) {
		// ���̳߳�����8������
		for (int i = 1; i <= 8; i++) {
			// �����ڲ������治�ܷ�һ����final�ı����������Ұ�i��ֵ����task
			final int task = i;

			threadPool.execute(new Runnable() {
				@Override
				public void run() {
					System.out.println("����" + Thread.currentThread().getName()
							+ "��" + "�õ��˵�" + task + "�������ҿ�ʼִ����");
				}
			});
		}
	}
}

```

ʾ������

```
public class BankCount {
    public synchronized void addMoney(int money){//��Ǯ
        System.out.println(Thread.currentThread().getName() + ">���룺" + money);
    }

    public synchronized void getMoney(int money){//ȡǮ
        System.out.println(Thread.currentThread().getName() + ">ȡǮ��" + money);
    }
}
```

```
public class BankTest {
    public static void main(String[] args) {
        final BankCount bankCount = new BankCount();

        ExecutorService executor = Executors.newFixedThreadPool(10);
        executor.execute(new Runnable() {//��Ǯ�߳�
            @Override
            public void run() {
                int i = 5;
                while(i-- > 0){
                    bankCount.addMoney(200);
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        });
        Future<?> future = executor.submit(new Runnable() {//ȡǮ�߳�
            @Override
            public void run() {
                int i = 5;
                while(i-- > 0){
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    bankCount.getMoney(200);
                }
            }
        });
        try {
            Object res = future.get();
            System.out.println(res);
        } catch (InterruptedException e) {
            // �����ж��쳣
            e.printStackTrace();
        } catch (ExecutionException e) {
            // �����޷�ִ�������쳣
            e.printStackTrace();
        }finally{
            // �ر��̳߳�
            executor.shutdown();
        }
    }
}
```
