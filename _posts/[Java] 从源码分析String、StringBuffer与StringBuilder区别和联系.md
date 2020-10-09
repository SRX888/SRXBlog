

 - String

> public final class **String** extends Object
implements Serializable, Comparable<String>, CharSequence
String ������ַ�����Java �����е������ַ�������ֵ���� "abc" ������Ϊ�����ʵ��ʵ�֡�

>�ַ����ǳ��������ǵ�ֵ�ڴ���֮���ܸ��ġ��ַ���������֧�ֿɱ���ַ�������Ϊ String **�����ǲ��ɱ�ģ����Կ��Թ���**�����磺
>
     String str = "abc"  
��Ч�ڣ�
>
     char data[] = {'a', 'b', 'c'};
     String str = new String(data);
> 
���������һЩ���ʹ���ַ����ĸ���ʾ����
>
     System.out.println("abc");
     String cde = "cde";
     System.out.println("abc" + cde);
     String c = "abc".substring(2,3);
     String d = cde.substring(1, 2);
 
>String ������ķ��������ڼ�����еĵ����ַ����Ƚ��ַ����������ַ�������ȡ���ַ����������ַ����������������ַ�ȫ��ת��Ϊ��д��Сд����Сдӳ����� Character ��ָ���� Unicode ��׼�档

>Java �����ṩ���ַ����������ţ�"+"���Լ�����������ת��Ϊ�ַ���������֧�֡�**�ַ���������ͨ�� StringBuilder**���� StringBuffer���༰�� **append ����**ʵ�ֵġ��ַ���ת����ͨ�� toString ����ʵ�ֵģ��÷����� Object �ඨ�壬���ɱ� Java �е�������̳С��й��ַ���������ת���ĸ�����Ϣ������� Gosling��Joy �� Steele ������ The Java Language Specification��

>��������˵�������� null �������ݸ������еĹ��췽���򷽷����׳� NullPointerException��

>String ��ʾһ�� UTF-16 ��ʽ���ַ��������е������ַ� �ɴ������ ��ʾ���й���ϸ��Ϣ������� Character ���е� Unicode �ַ���ʾ��ʽ��������ֵ��ָ char ���뵥Ԫ����������ַ��� String ��ռ������λ�á�

>String ���ṩ���� Unicode ����㣨���ַ����� Unicode ���뵥Ԫ���� char ֵ���ķ�����

 - StringBuffer

>public final class **StringBuffer** extends Object
implements Serializable, CharSequence

>**�̰߳�ȫ�Ŀɱ��ַ�����**��һ�������� String ���ַ������������������޸ġ���Ȼ������ʱ�������������ĳ���ض����ַ����У���ͨ��ĳЩ�������ÿ��Ըı�����еĳ��Ⱥ����ݡ�

>�ɽ��ַ�����������ȫ�����ڶ���̡߳������ڱ�Ҫʱ����Щ��������ͬ������������ض�ʵ���ϵ����в����ͺ������Դ���˳�����ģ���˳�������漰��ÿ���߳̽��еķ�������˳��һ�¡�

>StringBuffer �ϵ���Ҫ������ append �� insert ��������������Щ�������Խ����������͵����ݡ�ÿ������������Ч�ؽ�����������ת�����ַ�����Ȼ�󽫸��ַ������ַ�׷�ӻ���뵽�ַ����������С�append ����ʼ�ս���Щ�ַ���ӵ���������ĩ�ˣ��� insert ��������ָ���ĵ�����ַ���

>���磬��� z ����һ����ǰ����Ϊ "start" ���ַ���������������˷������� z.append("le") ��ʹ�ַ������������� "startle"���� z.insert(4, "le") �������ַ�����������ʹ֮���� "starlet"��

>ͨ������� sb ���� StringBuilder ��һ��ʵ������ sb.append(x) �� sb.insert(sb.length(), x) ������ͬ��Ч����

>��������Դ�����йصĲ�������Դ�����е�׷�ӻ���������ʱ������ֻ��ִ�д˲������ַ����������϶�������Դ��ʵ��ͬ����

>ÿ���ַ�������������һ����������ֻҪ�ַ������������������ַ����еĳ���û�г���������������������µ��ڲ����������顣����ڲ��������������������Զ����󡣴� JDK 5 ��ʼ��Ϊ���ಹ����һ�������߳�ʹ�õĵȼ��࣬�� StringBuilder���������ȣ�ͨ��Ӧ������ʹ�� StringBuilder �࣬��Ϊ��֧��������ͬ�Ĳ���������������ִ��ͬ���������ٶȸ��졣

 - StringBuilder

>public final class **StringBuilder** extends Object
implements Serializable, CharSequence

>**һ���ɱ���ַ�����**�������ṩһ���� StringBuffer ���ݵ� API����**����֤ͬ��**�����౻������� StringBuffer ��һ�������滻�������ַ����������������߳�ʹ�õ�ʱ������������ձ飩��������ܣ��������Ȳ��ø��࣬��Ϊ�ڴ����ʵ���У����� StringBuffer Ҫ�졣

>�� StringBuilder �ϵ���Ҫ������ append �� insert ��������������Щ�������Խ����������͵����ݡ�ÿ������������Ч�ؽ�����������ת�����ַ�����Ȼ�󽫸��ַ������ַ�׷�ӻ���뵽�ַ����������С�append ����ʼ�ս���Щ�ַ���ӵ���������ĩ�ˣ��� insert ��������ָ���ĵ�����ַ���

>�� StringBuilder ��ʵ�����ڶ���߳��ǲ���ȫ�ġ������Ҫ������ͬ��������ʹ�� StringBuffer��

 1 .��String��StringBuffer��StringBuilder��ԭ�����еĲ��ִ���

```
//String   
public final class String  
implements java.io.Serializable, Comparable<String>, CharSequence 
{  
        private final char value[];  
        
         /**
	     * Allocates a new {@code String} so that it represents the sequence of
	     * characters currently contained in the character array argument. The
	     * contents of the character array are copied; subsequent modification of
	     * the character array does not affect the newly created string.
	     *
	     * @param  value
	     *         The initial value of the string
	     */
     
         public String(String original) {  
              this.value = Arrays.copyOf(value, value.length);
              // �Ѵ��빹�캯��original�ַ����зֳ��ַ����鲢����value[];  
         }  
}  
  

  
//StringBuffer   
public final class StringBuffer extends AbstractStringBuilder  
implements java.io.Serializable, CharSequence
{  
      
	 /**
     * Constructs a string buffer initialized to the contents of the
     * specified string. The initial capacity of the string buffer is
     * <code>16</code> plus the length of the string argument.
     *
     * @param   str   the initial contents of the buffer.
     * @exception NullPointerException if <code>str</code> is <code>null</code>
     */
         public StringBuffer(String str) {  
                 super(str.length() + 16); //�̳и���Ĺ�������������һ����СΪstr.length()+16��value[]����  
                 append(str); //��str�зֳ��ַ����в����뵽value[]��  
        }  
	  public synchronized StringBuffer append(String str) {
        super.append(str);
        return this;
    }

}  





//StringBuilder

public final class StringBuilder
    extends AbstractStringBuilder
    implements java.io.Serializable, CharSequence
{
	/**
     * Constructs a string builder initialized to the contents of the
     * specified string. The initial capacity of the string builder is
     * <code>16</code> plus the length of the string argument.
     *
     * @param   str   the initial contents of the buffer.
     * @throws    NullPointerException if <code>str</code> is <code>null</code>
     */
    public StringBuilder(String str) {
        super(str.length() + 16);
        append(str);
    }
	 public StringBuilder append(String str) {
        super.append(str);
        return this;
    }
}




//AbstractStringBuilder

abstract class AbstractStringBuilder implements Appendable, CharSequence {
    /**
     * The value is used for character storage.
     */
    char[] value;
	
	  /**
     * Creates an AbstractStringBuilder of the specified capacity.
     */
    AbstractStringBuilder(int capacity) {
        value = new char[capacity];
    }
	 public AbstractStringBuilder append(String str) {
        if (str == null) str = "null";
        int len = str.length();
        ensureCapacityInternal(count + len);
        str.getChars(0, len, value, count);
        count += len;
        return this;
    }
}
```

2 .���ǿ��Կ�����String�й�����������ַ��������зֳ��ַ����У��������˽��final�������value[]�С�
new String("java")ʹ��value[]={'j','a','v','a'}��֮�����String�����е�value[]��Ҳ���ܸı��ˣ�ֻ�ܶ���������**�̰߳�ȫ��**��

StringBuffer��StringBuilder���̳���AbstractStringBuilder ��������࣬�����ǵĹ��캯���д����ַ���������ø���AbstractStringBuilder�ж�Ӧ�Ĺ��캯����append���������๹�캯���½�һ������Ϊ���ַ�������+ĩβ����16����Ԫ�أ�������Ȼ��ͨ������append�������ַ���ת�����ַ�����value[]�У������char[] value û��final��StringBuffer��StringBuilder�е�**�ַ����ǿɱ��**�����Ժ�ͨ��append()���������ַ�������value[]ĩβ������Ҳ�͸ı���value[]�����ݺʹ�С�ˡ�

StringBuffer�Է�������ͬ�������߶Ե��õķ�������ͬ������������**�̰߳�ȫ��**��
��**StringBuilder�����̰߳�ȫ��**��

��

```
String s = "ja" +"va"

```

��

```
String s1="ja";   
                                                                      StringBuffer sb=new StringBuffer("va");
sb.append(s1);
```

��

```
String s1="ja"; 
String s2 = "va"; 
String s = s1 +s2
```


> �ڱ���׶ξ��ܹ�ȷ�����ַ�����������ȫû�б�Ҫ����String��StringBuffer����ֱ��ʹ���ַ���������"+"���Ӳ���Ч����ߡ�
>    ʱ���� ��<�� 
>
   StringBuffer�����appendЧ��Ҫ��������String�����"+"���Ӳ�����
 ʱ���� ��<�� 
	
>	һ����˵ ִ��ʱ���ϴӿ쵽�� StringBuilder��StringBuffer��String
>
> �Ƕ��̲߳����ַ�������������ʹ�� StringBuilder��

 - ������ͽӿ�

> �������п��Զ���һЩ����Ĺ�������������ֻ��Ҫ�����µĹ��ܣ�����Ҫ�ظ�д�Ѿ����ڵķ����� 
> 
> ���ӿ���ֻ�ǶԷ����������ͳ����Ķ��塣
> 
