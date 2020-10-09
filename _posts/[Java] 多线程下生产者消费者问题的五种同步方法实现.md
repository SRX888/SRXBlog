

 ����������������ģʽ��ͨ��һ����������������ߺ������ߵ�ǿ������⡣
 ����
 ����������������ģʽ���ŵ�

	- ����
	-  ֧�ֲ���
	-  ֧��æ�в���
 ������������ɷ�Ϊ���ࣺ��
 ������1�����ź�����������ʵ�������ߺ�������֮���ͬ����
 ����
����������- wait() / notify()����
����������- await() / signal()����
����������- BlockingQueue�������з���
����������- Semaphore����
����������
 ������2���������ߺ�������֮�佨��һ���ܵ�����һ�㲻ʹ�ã����������׿��ơ����ݲ��׷�װ�ʹ��䣩
��������
����������- PipedInputStream / PipedOutputStream��



## 1 wait() / notify()����ʵ��

����wait() / nofity()������Object���������������[Object����Щ���÷�����](http://blog.csdn.net/amazing7/article/details/51219376)��������Object�����඼����ʹ��������������
����
����wait()��������
�����������̵߳��ô˶���� notify() ����ǰ�����µ�ǰ�̵߳ȴ�����ǰ�̱߳���ӵ�д˶�������������̷߳����Դ˼�����������Ȩ���ȴ���ֱ�������߳�ͨ������ notify �������� notifyAll ����֪ͨ�ڴ˶���ļ������ϵȴ����߳�������Ȼ����߳̽��ȵ����»�öԼ�����������Ȩ����ܼ���ִ�С�
�����˷���ֻӦ����Ϊ�˶���������������ߵ��߳������á�

����notify()������
���������ڴ˶���������ϵȴ��ĵ����̡߳���������̶߳��ڴ˶����ϵȴ������ѡ��������һ���̡߳�ѡ���������Եģ����ڶ�ʵ����������ʱ�������߳�ͨ����������һ�� wait �������ڶ���ļ������ϵȴ���
ֱ����ǰ�̷߳����˶����ϵ����������ܼ���ִ�б����ѵ��̡߳������ѵ��߳̽��Գ��淽ʽ���ڸö���������ͬ�������������߳̽��о��������磬���ѵ��߳�����Ϊ�����˶������һ���̷߳���û�пɿ�����Ȩ�����ơ�
�����˷���ֻӦ����Ϊ�˶���������������ߵ��߳������á�ͨ���������ַ���֮һ���߳̿��Գ�Ϊ�˶���������������ߣ�
������ͨ��ִ�д˶����ͬ��ʵ��������
������ͨ��ִ���ڴ˶����Ͻ���ͬ���� synchronized �������ġ�
���������� Class ���͵Ķ��󣬿���ͨ��ִ�и����ͬ����̬������
һ��ֻ����һ���߳�ӵ�ж���ļ�������

����ʾ����

```
public class Test
{
    private static Integer count = 0;
    private final Integer FULL = 5;
    private static String lock = "lock";
 
    public static void main(String[] args) 
    {
        Test t = new Test();
        new Thread(t.new Producer()).start();
        new Thread(t.new Consumer()).start();
        new Thread(t.new Producer()).start();
        new Thread(t.new Consumer()).start();
    }
    class Producer implements Runnable
    {
        @Override
        public void run()
        {
            for (int i = 0; i < 5; i++)
            {
            	try {
					Thread.sleep(1000);
				} catch (InterruptedException e1) {
					// TODO Auto-generated catch block
					e1.printStackTrace();
				}
                synchronized (lock)
                {
                    while (count == FULL)
                    {
                            try {
								lock.wait();
							} catch (InterruptedException e) {
								// TODO Auto-generated catch block
								e.printStackTrace();
							}
                    }
                    count++;
                    System.out.println(Thread.currentThread().getName() + "produce:: " + count);
                    lock.notifyAll();
                }
            }
        }
    }
    class Consumer implements Runnable
    {
        @Override
        public void run()
        {
            for (int i = 0; i < 5; i++)
            {
            	try {
					Thread.sleep(1000);
				} catch (InterruptedException e1) {
					// TODO Auto-generated catch block
					e1.printStackTrace();
				}
                synchronized (lock)
                {
                    while (count == 0)
                    {
                            try {
								lock.wait();
							} catch (InterruptedException e) {
								// TODO Auto-generated catch block
								e.printStackTrace();
							}
                    }
                    count--;
                    System.out.println(Thread.currentThread().getName()+ "consume:: " + count);
                    lock.notifyAll();
                }
            }
        }
    }
}

```
����ļ��������������������Ҳ���Ǵ����е�lock���󣩣�ע���ǵ����������wait() / nofity()������

���н����
![����дͼƬ����](http://img.blog.csdn.net/20160423102010734)


##2 await() / signal()����

����await()/signal()�Ƕ�wait()/notify()�ĸĽ������ܸ���ǿ�󣬸������ڸ߼��û���synchronized���йܸ�JVMִ�еģ���lock��javaд�Ŀ������Ĵ��롣 
����
����ReentrantLock��ʵ��lock�ӿڣ������synchronized���������߼����ܣ����� 
�����ٵȴ����ж� 
���������ڳ��������̳߳�ʱ�䲻�ͷ�����ʱ��,�ȴ����߳̿���ѡ������ȴ�. ����������������������
> tryLock(long timeout, TimeUnit unit)

�������ڹ�ƽ�� 
��������������������˳����һ�λ������Ϊ��ƽ��.synchronized���Ƿǹ�ƽ��,ReentrantLock����ͨ�����캯��ʵ�ֹ�ƽ��.

> new RenentrantLock(boolean fair)

������ƽ���ͷǹ�ƽ������2�ֻ��Ƶ���˼��������Ҳ���˽����ţ������ڶ��߳���˵����ƽ���������߳̽�����˳�򣬺�������̺߳����������ǹ�ƽ������˼���Ǻ��������Ҳ���Ժ�ǰ�ߵȴ������߳�ͬʱ��������Դ������Ч����������Ȼ�Ƿǹ�ƽ��Ч�ʸ��ߣ���Ϊ��ƽ����Ҫ�ж��ǲ����̶߳��еĵ�һ���Ż����̻߳������ 
���� 
�����۰󶨶��Condition 
������ͨ�����newCondition���Ի�ö��Condition����,���Լ򵥵�ʵ�ֱȽϸ��ӵ��߳�ͬ���Ĺ���.ͨ��await(),signal();

   һ������¶�����synchronizedԭ��ʵ��ͬ���������������ʹ��ReentrantLock ������ 
��������ĳ���߳��ڵȴ�һ�����Ŀ���Ȩ�����ʱ����Ҫ�ж� 
����������Ҫ�ֿ�����һЩwait-notify��ReentrantLock�����ConditionӦ�ã��ܹ�����notify�ĸ��߳� 
������ �۾��й�ƽ�����ܣ�ÿ���������̶߳����ŶӵȺ�
������ 
�����˽⣺[�߳�ͬ���ķ�����sychronized��lock��reentrantLock����](http://blog.csdn.net/amazing7/article/details/51219714)

����
������ʹ��ReentrantLock��ʵ������������������

����ʾ����
```
public class Test {
    private static Integer count = 0;//������
    private final Integer FULL = 5;
    final Lock lock = new ReentrantLock(); //��ÿ�������
    final Condition put = lock.newCondition();
    final Condition get = lock.newCondition();
 
    public static void main(String[] args)  {
    	
        Test t = new Test();
        new Thread(t.new Producer()).start();
        new Thread(t.new Consumer()).start();
        new Thread(t.new Consumer()).start();
        new Thread(t.new Producer()).start();
    }
    class Producer implements Runnable {
        @Override
        public void run() {
            for (int i = 0; i < 5; i++) {
             	try {
					Thread.sleep(1000);
				} catch (InterruptedException e1) {
					// TODO Auto-generated catch block
					e1.printStackTrace();
				}
                lock.lock();
                try {
                    while (count == FULL) {
                        try {
                            put.await();
                        } catch (InterruptedException e) {
                            // TODO Auto-generated catch block
                            e.printStackTrace();
                        }
                    }
                    count++;
                    System.out.println(Thread.currentThread().getName() + "produce:: " + count);
                    get.signal();
                } finally {
                    lock.unlock();
                }
            }
        }
    }
 
    class Consumer implements Runnable {
 
        @Override
        public void run() {
            for (int i = 0; i < 5; i++) {
            	try {
					Thread.sleep(1000);
				} catch (InterruptedException e1) {
					// TODO Auto-generated catch block
					e1.printStackTrace();
				}
                lock.lock();
                try {
                    while (count == 0) {
                        try {
                            get.await();
                        } catch (Exception e) {
                            // TODO: handle exception
                            e.printStackTrace();
                        }
                    }
                    count--;
                    System.out.println(Thread.currentThread().getName()+ "consume:: " + count);
                    put.signal();
                } finally {
                    lock.unlock();
                }
            }
        }
    }
}
```
���н����
![����дͼƬ����](http://img.blog.csdn.net/20160423101751985)


##3 BlockingQueue�������з���

����BlockingQueue ʵ����Ҫ����������-ʹ���߶��У��������⻹֧�� Collection �ӿڡ����̰߳�ȫ�ģ������Ŷӷ���������ʹ���ڲ�����������ʽ�Ĳ����������Զ��ﵽ���ǵ�Ŀ�ġ�
����BlockingQueue ������������ʽ���֣����ڲ����������㵫�����ڽ���ĳһʱ�̿�������Ĳ�������������ʽ�Ĵ���ʽ��ͬ����һ�����׳�һ���쳣���ڶ����Ƿ���һ������ֵ��null �� false������ȡ���ڲ����������������ڲ������Գɹ�ǰ�������ڵ�������ǰ�̣߳����������ڷ���ǰֻ�ڸ��������ʱ���������������±����ܽ�����Щ������
����

����![����дͼƬ����](http://img.blog.csdn.net/20160423103531099)
������Ҫ˵˵�����������Ǹ�����
����
����put()��������ָ��Ԫ�ز���˶����У����ȴ����õĿռ䣨����б�Ҫ����

����take()��������ȡ���Ƴ��˶��е�ͷ������ָ���ĵȴ�ʱ��ǰ�ȴ����õ�Ԫ�أ�����б�Ҫ����
����
����ʾ����
```
public class Test {
    private static Integer count = 0;
    final BlockingQueue<Integer> bq = new ArrayBlockingQueue<Integer>(5);//����Ϊ5����������
    
  public static void main(String[] args)  {
        Test t = new Test();
        new Thread(t.new Producer()).start();
        new Thread(t.new Consumer()).start();
        new Thread(t.new Consumer()).start();
        new Thread(t.new Producer()).start();
    }
    class Producer implements Runnable {
        @Override
        public void run() {
            for (int i = 0; i < 5; i++) {
                try {
                    Thread.sleep(1000);
                } catch (Exception e) {
                    e.printStackTrace();
                }
                try {
                    bq.put(1);
                    count++;
                    System.out.println(Thread.currentThread().getName() + "produce:: " + count);
                } catch (InterruptedException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }
            }
        }
    }
    class Consumer implements Runnable {
 
        @Override
        public void run() {
            for (int i = 0; i < 5; i++) {
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e1) {
                    e1.printStackTrace();
                }
                try {
                    bq.take();
                    count--;
                    System.out.println(Thread.currentThread().getName()+ "consume:: " + count);
                } catch (Exception e) {
                    // TODO: handle exception
                    e.printStackTrace();
                }
            }
        }
    }
}
```
���н����
![����дͼƬ����](http://img.blog.csdn.net/20160423104129979)

����

## 4 Semaphore����ʵ��ͬ��

�����ź�����Semaphore��ά����һ����ɼ�������ɿ���ǰ������ÿһ�� acquire()��Ȼ���ٻ�ȡ����ɡ�ÿ�� release() ���һ����ɣ��Ӷ������ͷ�һ�����������Ļ�ȡ�ߡ����ǣ���ʹ��ʵ�ʵ���ɶ���Semaphore ֻ�Կ�����ɵĺ�����м���������ȡ��Ӧ���ж���
Semaphore ͨ���������ƿ��Է���ĳЩ��Դ��������߼��ģ����߳���Ŀ�� 

����ע�⣬���� acquire() ʱ�޷�����ͬ��������Ϊ�����ֹ����ص����С��ź�����װ�����ͬ���������ƶԳصķ��ʣ���ͬά�ָóر���һ���������ͬ���Ƿֿ��ġ�

����ʾ����
```
public class Test
{
    int count = 0;
    final Semaphore put = new Semaphore(5);//��ʼ���Ƹ���
    final Semaphore get = new Semaphore(0);
    final Semaphore mutex = new Semaphore(1);
 
    
    public static void main(String[] args)  {
        Test t = new Test();
        new Thread(t.new Producer()).start();
        new Thread(t.new Consumer()).start();
        new Thread(t.new Consumer()).start();
        new Thread(t.new Producer()).start();
    }
    
    class Producer implements Runnable
    {
        @Override
        public void run()
        {
            for (int i = 0; i < 5; i++)
            {
                try
                {
                    Thread.sleep(1000);
                }
                catch (Exception e)
                {
                    e.printStackTrace();
                }
                try
                {
                    put.acquire();//ע��˳��
                    mutex.acquire();
                    count++;
                    System.out.println(Thread.currentThread().getName() + "produce:: " + count);
                }
                catch (Exception e)
                {
                    e.printStackTrace();
                }
                finally
                {
                    mutex.release();
                    get.release();
                }
 
            }
        }
    }
 
    class Consumer implements Runnable
    {
 
        @Override
        public void run()
        {
            for (int i = 0; i < 5; i++)
            {
                try
                {
                    Thread.sleep(1000);
                }
                catch (InterruptedException e1)
                {
                    e1.printStackTrace();
                }
                try
                {
                    get.acquire();//ע��˳��
                    mutex.acquire();
                    count--;
                    System.out.println(Thread.currentThread().getName()+ "consume:: " + count);
                }
                catch (Exception e)
                {
                    e.printStackTrace();
                }
                finally
                {
                    mutex.release();
                    put.release();
                }
            }
        }
    }
}
```
���н����
 
   ![����дͼƬ����](http://img.blog.csdn.net/20160423110117024)

����ע��ͬ�����ƣ�notFull.acquire()�������ڻ������ƣ�mutex.acquire()��ǰ���ã�����ȵõ��������ٷ����ȴ��������������

##5 PipedInputStream / PipedOutputStream

���������λ��java.io���У��ǽ��ͬ���������򵥵İ취��һ���߳̽�����д��ܵ�����һ���̴߳ӹܵ���ȡ���ݣ������㹹����һ��������/�����ߵĻ��������ģʽ��PipedInputStream/PipedOutputStreamֻ�����ڶ��߳�ģʽ�����ڵ��߳��¿��ܻ�����������

����ʾ����
```
public class Test {
    final PipedInputStream pis = new PipedInputStream();
    final PipedOutputStream pos = new PipedOutputStream();
	public static void main(String[] args) {
	       Test t = new Test();
	       new Thread(t.new Producer()).start();
	       new Thread(t.new Consumer()).start();
	}
  class Producer implements Runnable{

	@Override
	public void run() {
			try {
				pis.connect(pos);
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			try {
				while(true){ //���ϵĲ�������
					int n = (int)(Math.random()*255);
					System.out.println(Thread.currentThread().getName()+"produce::"+n);
					pos.write(n);
					pos.flush();
				}
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}finally {
				try {
					pis.close();
					pos.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
		}
		
	}
  }
  class Consumer implements Runnable{

	@Override
	public void run() {
			int n;
			try {
				while(true){
					n = pis.read();
					System.out.println(Thread.currentThread().getName()+"consume::"+n);
				}
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}finally{
				try {
					pis.close();
					pos.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			
		}
	}
  }
}
```
���н����
![����дͼƬ����](http://img.blog.csdn.net/20160423094138234)

�����ӽ���Ͽ���Ҳ����ʵ��ͬ������һ�㲻ʹ�ã���Ϊ���������׿��ơ����ݲ��׷�װ�ʹ��䡣
