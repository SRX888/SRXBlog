**��д(Override)**

������д������Ը����������ʵķ�����ʵ�ֹ��̽������±�д��
����**����ֵ���βζ����ܸı�**������ǲ��䣬��д����ʵ�֣�
����
������д�ĺô�����**������Ը�����Ҫ�������ض����Լ�����Ϊ**��
Ҳ����˵�����ܹ�������Ҫʵ�ָ���ķ�����
�������������ԭ�����д��ζ�ſ�����д�κ����з�����ʵ�����£� 

```

class Animal{

   public void move(){
      System.out.println("Animal��can move");
  �� }
}

class Pig extends Animal{

   public void move(){
      System.out.println("Pig can Climb tree");
    }
}

public class Test{

   public static void main(String args[]){
      Animal a = new Animal(); 
      Animal b = new Pig (); 

      a.move();// ִ�� Animal ��ķ���

      b.move();//ִ�� Pig ��ķ���
   }
}
```

����ʵ���������н�����£�

```
Animal��can move
Pig can Climb tree
```

����������������п��Կ�����b ��������Animal�� �����ã������е���Pig���move������
����������Ϊ����**�ڱ���׶Σ�ֻ�Ǽ���������������**��
Ȼ����**����ʱ��Java�����(JVM)ָ����������Ͳ������иö���ķ�����**
����������������У�֮�����ܱ���ɹ�������ΪAnimal���д���move������Ȼ������ʱ�����е����ض�����Pig ���󣩵ķ�����
����������ӣ�


```
class Animal{

   public void move(){
      System.out.println("Animal��can move");
   }
}

class Pig extends Animal{

   public void move(){
      System.out.println("Pig can Climb tree");
   }
   public void bark(){
      System.out.println("Pig can bray");
   }
}

public class Test{

   public static void main(String args[]){
      Animal a = new Animal(); 
      Animal b = new Pig(); 

      a.move();// ִ�� Animal ��ķ���
      b.move();//ִ�� Pig ��ķ���
      b.bark();
   }
}

```

����ʵ���������н���ᱨ���´���


```
Test.java:30: cannot find symbol
symbol  : method bark()
location: class Animal
                b.bark();
                 ^
```

����һ�����������Ϊb����������Animal ����û��bark������

**��������д����**��

**�����б������ȫ**�뱻��д������**��ͬ**��

**��������**������ȫ�뱻��д�����ķ�������**��ͬ**��

**����Ȩ�޲��ܱȸ����б���д�ķ����ķ���Ȩ�޸��ߡ�**���磺��������һ������������Ϊpublic����ô����������д�÷����Ͳ�������Ϊprotected �� private��

����ĳ�Ա����ֻ�ܱ�����������д��

����Ϊ**final�ķ������ܱ���д**��

����Ϊ**static�ķ������ܱ���д�������ܹ����ٴ�����**��

����͸�����ͬһ�����У���ô���������д�������з�������������Ϊprivate��final�ķ�����

����͸��಻��ͬһ�����У���ô����ֻ�ܹ���д���������Ϊpublic��protected�ķ�final������

��д�ķ����ܹ��׳��κη�ǿ���쳣�����۱���д�ķ����Ƿ��׳��쳣��

���ǣ���д�ķ��������׳��µ�ǿ�����쳣�����߱ȱ���д���������ĸ��㷺��ǿ�����쳣����֮����ԡ�

**���췽�����ܱ���д**��

������ܼ̳�һ��������������д�������( �����private����)��



**����(Overload)**

��������(overloading) ����ͬһ�������棬**����������ͬ����������ͬ���������Ϳ�����ͬҲ���Բ�ͬ**�Ķ��������
ÿ�����صķ�����ֻ�����ع��캯������������һ����һ�޶��Ĳ��������б�
����
����
���ع���

�����صķ���**����ı�����б�**��
�����صķ���**����**�ı䷵�����ͣ�
�����صķ���**����**�ı�������η���
�����صķ������������µĻ����ļ���쳣��
�����ܹ���ͬһ�����л���**��һ������**�б����ء�


```
public class Test{
 
	public int test(){
		System.out.println("Overload1");
		return 1;
	}
 
	public void test(int a){
		System.out.println("Overload2");
	}	
 
	//����������������˳��ͬ
	public String test(int a,String s){
		return "Overload3" + s;
	}	
 
	public String test(String s,int a){
		return "Overload4"+s;
	}	
 
	public static void main(String[] args){
		Test t = new Test();
		System.out.println(t.test());
		t.test(1);
		System.out.println(t.test(1,"test3"));
		System.out.println(t.test("test4",1));
	}
}

```

**��д������֮�������**

 ���ط�����
		
     �����б�      �����޸�
     
     ��������      �����޸� 
     
     �쳣         �����޸� 
     
     �������η�    �����޸�
               
��д������

     �����б�      ���ܸ�
     
     ��������      ���ܸ� 
     
     �쳣         ���Լ��ٻ�ɾ���������׳��µĻ������쳣
     
     �������η�    ֻ�ܽ������ƣ����ܱ�ɸ�����
                      

> �����ɵ͵��� �� public  ��protected ��private

