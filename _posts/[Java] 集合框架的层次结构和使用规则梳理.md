> ��Java�����У�Java���Ե�����߶Գ��õ����ݽṹ���㷨����һЩ�淶���ӿڣ���ʵ�֣�����ʵ�ֽӿڵ��ࣩ�����г�����������ݽṹ�Ͳ������㷨��ͳ��ΪJava���Ͽ�ܣ�JavaCollectionFramework����
> 
Java����Ա�ھ���Ӧ��ʱ�����ؿ������ݽṹ���㷨ʵ��ϸ�ڣ�ֻ��Ҫ����Щ�ഴ������һЩ����Ȼ��ֱ��Ӧ�þͿ����ˣ������ʹ������˱��Ч�ʡ� 

#����

 - ʲô�ǿ�ܣ�
����

> ���ļ���

 - ʲô�Ǽ��ϣ�

> ������ݵ�����

 - ���Ͽ��������ʲô��

> ������ʾ�Ͳ�����ͳһ�ļܹ�

���Ͽ�ܰ����������֣�һ�������࣬һ�����ǽӿڣ������淶���ƹ��ܵ��ࣩ

��Ҫ�ṹͼ��

![����дͼƬ����](http://img.blog.csdn.net/20160427155321833)��

����Java���Ϲ��߰�λ��Java.util���£������˺ܶೣ�õ����ݽṹ�������顢����ջ�����С����ϡ���ϣ��ȡ���
����
����Java���Ͽ�ܵ�ʹ���ص㣺List�б�Set���ϡ�Mapӳ�䡢��������Iterator��Enumeration���������ࣨArrays��Collections������

#Collection

���� Collection��List��Set�ȼ��ϸ߶ȳ�������Ľӿڣ�����������Щ���ϵĻ���������ʵ�ָýӿڼ����ӽӿڵ������඼��Ӧ��clone()�������������л��ࡣ
������
��Ҫʵ�ֹ�ϵ���ͼ����

������![����дͼƬ����](http://img.blog.csdn.net/20160427155936816)��

Collection�ĳ��÷�����

 - ���
 boolean add(E e);
 boolean addAll(Collection<> c)���� 
 - ɾ��
 boolean remove(E e);
 boolean removeAll(Collection<> c) ;
 void clear();
 - �ж�
 boolean contains(Object o)
 boolean containsAll(Collection<> c)
 boolean isEmply();
 - ��ȡ
 int size();
 Iterator<E> iterator();
 - ����
 boolean retainAll(Collection coll);
 Object[] toArray();����

##List
  
����List�ӿ�ͨ����ʾһ���б�**���������**������Ԫ�أ�Ԫ����**�����**����������λ������ɾԪ�أ����ܷ��ʶ��ٴΣ�Ԫ��λ�ò��䣬**�����ظ�**Ԫ�ء���
����
������Iteratorʵ�ֵ��������Ҳ����ListIteratorʵ��˫�������

List���еĳ���������

 - ���
    void add(index,element);
    void add(index,collection);
 - ɾ��
    Object remove(index);
 - ��ȡ
    Object get(index);
    int indexOf(object);
    int lastIndexOf(object);
    Last subList(from,to);
 - �޸�
    Object set(index,element); 

###LinkedList

�����ڲ���**����**���ݽṹ��**������ʺ���**��**��ɾ�����ܿ�**�����ķѶ�����Դ��**����nullԪ��**��**���̰߳�ȫ** ���������߳�ͬʱ����һ��List��������Լ�ʵ�ַ���ͬ���� ��������

```
List list = Collections.synchronizedList(new LinkedList(...));
```

###ArrayList 

�����ڲ���**����**���ݽṹ��Ԫ��˳��洢������Ԫ�ظı�List��Сʱ���ڲ����½�һ�����飬�ڽ����Ԫ��ǰ���������ݿ������������� ��**������ʺܿ�**��**ɾ����ͷβԪ����������Ԫ����**���ҷ���Դ ������������Ƶ����ɾ����������������飬50%�ӳ���������Ч�ʵͣ����������Ҫ�ɱ����飬�ɿ���ʹ�����飬**���̰߳�ȫ**��


###Vector

������һ��ArrayList���߱�ArrayList�����ԡ����з�������**�̰߳�ȫ**�ģ�˫�н�����ArrayList����Ҫ���� ��ArrayListЧ�ʵ͡�

####Stack

����LIFO�����ݽṹ��Stack�̳���Vector��Ҳ��**ͬ����**��

##Set

����ͨ����ʾһ�����ϣ��ӿ��еķ�����Collection�е�һ�¡���һ���������ظ�Ԫ�ص�Collection��**������һ����Ԫ��**��**�������**���ʰ�����Ԫ�أ�ֻ����Iteratorʵ�ֵ��������Set**��ͬ��**��

###HashSet 

�����ڲ����ݽṹ�ǹ�ϣ��HashMap����Ԫ����**�����**����������Ԫ�ص�˳��ͼ����˳��ͬ .��ε������ʣ�Ԫ�ص�˳����ܲ�ͬ��**���̰߳�ȫ**��

####LinkedHashSet 

��������HashMap�������Setʵ�֣���������Ԫ�ص�˳��ͼ����˳����ͬ����ε������ʣ�Ԫ�ص�**˳�򲻱�**��

###SortedSet 

��������SortedSet������Ԫ�ر���ʵ��Comparable�ӿڣ�Ԫ����**�����**��

####TreeSet

��������TreeMapʵ�ֵ�SortedSet�����Զ�Set�����е�Ԫ�ؽ������������**����**����Ԫ�أ�**���̰߳�ȫ**��
��
������������ʽ��

 - ��Ԫ������߱��ȽϹ��ܣ�**Ԫ��**����Ҫʵ��Compareable��������compareTo������
 - �ü�������߱��ȽϹ��ܣ�����һ����ʵ��Comparator�ӿڣ�����compare������


#Map

������һ��ӳ��ӿڣ�Mapû�м̳�Collection�ӿڣ�Map�ṩkey��value��ӳ�䡣һ��Map�в��ܰ�����ͬ��key��ÿ��keyֻ��ӳ��һ��value����
����
����������AbstractMapͨ��������ģʽʵ����Map�ӿ��еĴ󲿷ֺ�����TreeMap��HashMap��WeakHashMap��ʵ���඼ͨ���̳�AbstractMap��ʵ�֣��������õ�HashTableֱ��ʵ����Map�ӿڡ���

����ʵ�ֹ�ϵ���ͼ����

![����дͼƬ����](http://img.blog.csdn.net/20160427163254642)��

map�г��õķ�����

 - ���
        value put(key,value):����ǰһ����key������ֵ�����û���򷵻�null
 - ɾ��
        void clear():���map���ϡ�
        value remove(key):����ָ����keyɾ�������ֵ��
 - �ж�
        boolean containKey(key)
        boolean containValue(value)
        boolean isEmpty();
 - ��ȡ
        value get(key);ͨ������ȡֵ�����û�иü�����null����Ȼ����ͨ������null���ж��Ƿ����ָ����
        int size()��ȡ��ֵ�Ը�����

ȡ��Map�����е�����ֵ�ķ�����

 - ͨ��keySet������ȡmap�����еļ����ڵ�Set���ϣ���ͨ��Set�ĵ�������ȡ��ÿһ�������ٶ�ÿһ������ͨ��map���ϵ�get����ȡ���Ӧֵ���ɡ���
 

```
		Map map = new LinkedHashMap();
        map.put("1", "��һ����");
        map.put("2", "�ڶ�����");
        map.put("3", "��������");
        for (Object obj : map.keySet()) {
            String key = (String) obj;
            String value = (String) map.get(key);
        }
```

 - ͨ��map���ϵ�entryset����Ҳ��ȡ��map���ϵ������еļ�ֵ�ԣ����صľ���Map.Entry������ͨ��Map.Entry�����getkey��getvalue�����Ϳ���ȡ����Ӧ�ļ���ֵ����

```
		Map map = new LinkedHashMap();
        map.put("1", "one");
        map.put("2", "two");
        map.put("3", "three");
        for (Object obj : map.entrySet()) {
            Entry entry = (Entry) obj;
            String key = (String) entry.getKey();
            String value = (String) entry.getValue();
        }
```

 
 - ͨ��Iterator����keySet��entryset

```
		Map map = new HashMap();
        map.put("1", "one");
        map.put("2", "two");
        map.put("3", "three");
        Set set = map.keySet();
        Iterator it = set.iterator();
        while (it.hasNext()) {
            String key = (String) it.next();
            String value = (String) map.get(key);
        }
```

```
		Map map = new HashMap();
        map.put("1", "one");
        map.put("2", "two");
        map.put("3", "three");
        Set set = map.entrySet();
        Iterator it = set.iterator();
        while (it.hasNext()) {
            Entry entry = (Entry) it.next();
            String key = (String) entry.getKey();
            String value = (String) entry.getValue();
        }
```

��
##Hashtable

�����������Ķ������ʵ����hashcode()��equals()������Ҳ����˵ֻ��Object�����������������Hashtable�̳���Dictionary�ֵ䣬ʵ��Map�ӿڡ�**����ֵ�������ǿն���**����η��ʣ�ӳ��Ԫ�ص�**˳����ͬ** ��**�̰߳�ȫ**��

###Properties 

�����̳���Hashtable��**����ֵ�����ַ���**��

##HashMap 

�����ڲ��ṹ�ǹ�ϣ��**����ֵ�������ǿն��󣬲���֤ӳ���˳��**����η��ʣ�ӳ��Ԫ�ص�˳����ܲ�ͬ��**���̰߳�ȫ**����

###LinkedHashMap 

�����̳���HashMap ����η��ʣ�ӳ��Ԫ�ص�**˳������ͬ��**�����ܱ�HashMap�

##WeakHashMap

������ĳ������������ʹ��ʱ�������ռ������Ƴ�����������ӳ���ϵ���ڣ�**���̰߳�ȫ**��

##SortedMap

��������**����**���У����м�������ʵ��Comparable�ӿڡ�

###TreeMap

�����ڲ��ṹ�Ƕ����������ں����ʵ�֣���**��ͬ��**�����Զ�Map�����еļ���������

#Iterator

����Iterator�Ǳ���**����**�ĵ����������ܱ���Map��ֻ��������Collection����Collection��ʵ���඼ʵ����iterator()������������һ��Iterator���󡣡�
����
����ListIterator��ר����������List����
������Enumeration����JDK1.0ʱ����ģ�������Iterator��ͬ�������Ĺ��ܱ�IteratorҪ�٣���ֻ����Hashtable��Vector��Stack��ʹ�á�

����Arrays��Collections�������������顢���ϵ����������ࡣ

#ʹ�ü���

 - ��Ҫ**Ψһ**��Set
������������������Ҫָ��˳��TreeSet
       ��������������������������Ҫ��HashSet��
       ����������������������
       ���������������õ���洢һ�µ�˳��LinkedHashSet��
       �������������� 
 - ����Ҫ**Ψһ**��List
����������������ҪƵ����ɾ�����ã�LinkedList
������������������Ҫ��ArrayList��
��������������������
 - ����漰����ջ�����еȲ�����Ӧ�ÿ�����List��

 

 - ������Ҫ���ٲ��룬ɾ��Ԫ�أ�Ӧ��ʹ��LinkedList��
 - �����Ҫ�����������Ԫ�أ�Ӧ��ʹ��ArrayList�� 
 
 - ��������ڵ��̻߳����У����߷��ʽ�����һ���߳��н��У����Ƿ�ͬ�����࣬��Ч�ʽϸߡ� 
 
 - �������߳̿���ͬʱ����һ���࣬Ӧ��ʹ��ͬ�����ࡣ Ҫ�ر�ע��Թ�ϣ��Ĳ�������Ϊkey�Ķ���Ҫ��ȷ��дequals��hashCode������ �������ؽӿڶ���ʵ�ʵ����ͣ��緵��List����ArrayList����������Ժ���Ҫ��ArrayList����LinkedListʱ���ͻ��˴��벻�øı䣬�������Գ����̡�