#1.����

����Hashmap�̳���AbstractMap��ʵ����Map��Cloneable��java.io.Serializable�ӿڡ�����key��value������Ϊnull��ӳ�䲻������ġ�
����
����Hashmap����ͬ���ģ������Ҫ�̰߳�ȫ��HashMap������ͨ��Collections��ľ�̬����synchronizedMap����̰߳�ȫ��HashMap��
	��������
```
Map map = Collections.synchronizedMap(new HashMap());
```



�����˲�ͬ��������ʹ�� null ֮�⣬HashMap ���� Hashtable ������ͬ����

HashMap ��������Ҫ�Ĳ���������ʼ������ �� ���������ӡ���

> **����** �ǹ�ϣ����Ͱ����������ʼ���� ֻ�ǹ�ϣ���ڴ���ʱ������
> 
> **��������** �ǹ�ϣ�����������Զ�����֮ǰ���Դﵽ������һ�ֳ߶ȣ�Ĭ��0.75������
> 
>����ϣ���е���Ŀ�������˼��������뵱ǰ�����ĳ˻�ʱ����Ҫ�Ըù�ϣ����� rehash ���������ؽ��ڲ����ݽṹ��Ͱ���أ�����
>
>��������Խ��,������Ԫ��Խ��,�ô���,�ռ������ʸ���,��:��ͻ�Ļ���Ӵ���.��֮,��������ԽС,������Ԫ��Խ��, �ô���:��ͻ�Ļ����С��,��:�ռ��˷Ѷ���.

#2.HashMap�����ݽṹ

 ����Hashmap������**���������**��ͨ��key��hashCode������hashֵ�ģ�ֻҪhashCode��ͬ�����������hashֵ��һ����Ȼ���ټ���������±꣬������key��Ӧ��ͬһ���±꣬���������������²������**ǰ��**��

�����ṹͼ���£�ͨ��key����value����

![����дͼƬ����](http://img.blog.csdn.net/20160429162312540)��
��ͼ��Դ�����磩

��������HashMap��Entry��Ĵ��룺

```
static class Entry<K,V> implements Map.Entry<K,V> {
    final K key;
    V value;
    // ָ����һ���ڵ�
    Entry<K,V> next;
    final int hash;
    // ���캯����
    // �����������"��ϣֵ(h)", "��(k)", "ֵ(v)", "��һ�ڵ�(n)"
    Entry(int h, K k, V v, Entry<K,V> n) {
        value = v;
        next = n;
        key = k;
        hash = h;
    }
    public final K getKey() {
        return key;
    }
    public final V getValue() {
        return value;
    }
    public final V setValue(V newValue) {
        V oldValue = value;
        value = newValue;
        return oldValue;
    }
    // �ж�����Entry�Ƿ����
    // ������Entry�ġ�key���͡�value������ȣ��򷵻�true��
    // ���򣬷���false
    public final boolean equals(Object o) {
        if (!(o instanceof Map.Entry))
            return false;
        Map.Entry e = (Map.Entry)o;
        Object k1 = getKey();
        Object k2 = e.getKey();
        if (k1 == k2 || (k1 != null && k1.equals(k2))) {
            Object v1 = getValue();
            Object v2 = e.getValue();
            if (v1 == v2 || (v1 != null && v1.equals(v2)))
                return true;
        }
        return false;
    }
    // ʵ��hashCode()
    public final int hashCode() {
        return (key==null   ? 0 : key.hashCode()) ^
               (value==null ? 0 : value.hashCode());
    }
    public final String toString() {
        return getKey() + "=" + getValue();
    }
    // ����HashMap�����Ԫ��ʱ�������recordAccess()��
    // ���ﲻ���κδ���
    void recordAccess(HashMap<K,V> m) {
    }
    // ����HashMap��ɾ��Ԫ��ʱ�������recordRemoval()��
    // ���ﲻ���κδ���
    void recordRemoval(HashMap<K,V> m) {
    }
}
```
���ǿ������HashMap����һ��Entry���飬Entry�����а����˼���ֵ��

#3.HashMapԴ�����

HashMap����4�����캯��,���£�

> HashMap() 
          ����һ������Ĭ�ϳ�ʼ���� (16) ��Ĭ�ϼ������� (0.75) �Ŀ� HashMap��
          
>HashMap(int initialCapacity) 
          ����һ����ָ����ʼ������Ĭ�ϼ������� (0.75) �Ŀ� HashMap����
          
>HashMap(int initialCapacity, float loadFactor) 
          ����һ����ָ����ʼ�����ͼ������ӵĿ� HashMap����
          
>HashMap(Map<�� extends K, extends V> m) 
          ����һ��ӳ���ϵ��ָ�� Map ��ͬ���� HashMap����


HashMap�ṩ��API������

>  void	clear() 
          �Ӵ�ӳ�����Ƴ�����ӳ���ϵ����
          
> Object	clone() 
          ���ش� HashMap ʵ����ǳ�������������Ƽ���ֵ����
          
 >boolean	containsKey(Object key) 
          �����ӳ���������ָ������ӳ���ϵ���򷵻� true��
          
> boolean	containsValue(Object value) 
          �����ӳ�佫һ��������ӳ�䵽ָ��ֵ���򷵻� true��
          
> Set	entrySet() 
          ���ش�ӳ����������ӳ���ϵ�� Set��Map.Entry�� ��ͼ����
          
>  V	get(Object key) 
          ����ָ������ӳ���ֵ��������ڸü���˵����ӳ�䲻�����κ�ӳ���ϵ���򷵻� null��
          
>  boolean	isEmpty() 
          �����ӳ�䲻������-ֵӳ���ϵ���򷵻� true����
          
>  Set	keySet() 
          ���ش�ӳ�����������ļ��� Set���ˣ� ��ͼ��
          
 >V	put(K key, V value) 
          �ڴ�ӳ���й���ָ��ֵ��ָ��������
          
> void��	putAll(Map< extends K, extends V> m) 
          ��ָ��ӳ�������ӳ���ϵ���Ƶ���ӳ���У���Щӳ���ϵ���滻��ӳ��Ŀǰ���ָ��ӳ�������м�������ӳ���ϵ��
          
> V	remove(Object key) 
          �Ӵ�ӳ�����Ƴ�ָ������ӳ���ϵ��������ڣ���
          
> int	��size() 
          ���ش�ӳ���еļ�-ֵӳ���ϵ����
          
> Collection	values() 
          ���ش�ӳ����������ֵ�� Collection<V> ��ͼ��


HashMapԴ�룺

```
package java.util;
import java.io.*;
public class HashMap<K,V>
    extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable
{
    //  Ĭ�ϵĳ�ʼ����������ΪHashMap��Ͱ����Ŀ����16����ʵ������������2���������ݡ� 
    static final int DEFAULT_INITIAL_CAPACITY = 16;
	
    // ���������������2������С��2��30�η��������������󽫱����ֵ�滻��
    static final int MAXIMUM_CAPACITY = 1 << 30;
	
    // Ĭ�ϼ�������
    static final float DEFAULT_LOAD_FACTOR = 0.75f;
	
    // �洢���ݵ�Entry���飬������2���ݡ�
    // HashMap�ǲ���������ʵ�ֵģ�ÿһ��Entry��������һ����������
    transient Entry[] table;
	
    // HashMap�Ĵ�С������HashMap����ļ�ֵ�Ե�����
    transient int size;
	
    // HashMap����ֵ�������ж��Ƿ���Ҫ����HashMap��������threshold = ����*�������ӣ�
    int threshold;
	
    // ��������ʵ�ʴ�С
    final float loadFactor;
	
    // HashMap���ı�Ĵ���
    transient volatile int modCount;
	
    // ָ����������С���͡��������ӡ��Ĺ��캯��
    public HashMap(int initialCapacity, float loadFactor) {
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal initial capacity: " +
                                               initialCapacity);
        // HashMap���������ֻ����MAXIMUM_CAPACITY
        if (initialCapacity > MAXIMUM_CAPACITY)
            initialCapacity = MAXIMUM_CAPACITY;
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal load factor: " +
                                               loadFactor);
        // �ҳ�������initialCapacity������С��2����
        int capacity = 1;
        while (capacity < initialCapacity)
            capacity <<= 1;
        // ���á��������ӡ�
        this.loadFactor = loadFactor;
        // ���á�HashMap��ֵ������HashMap�д洢���ݵ������ﵽthresholdʱ������Ҫ��HashMap�������ӱ���
        threshold = (int)(capacity * loadFactor);
        // ����Entry���飬������������
        table = new Entry[capacity];
        init();
    }
	
    // ָ����������С���Ĺ��캯��
    public HashMap(int initialCapacity) {
        this(initialCapacity, DEFAULT_LOAD_FACTOR);
    }
	
    // Ĭ�Ϲ��캯����
    public HashMap() {
        // ���á��������ӡ�
        this.loadFactor = DEFAULT_LOAD_FACTOR;
        // ���á�HashMap��ֵ������HashMap�д洢���ݵ������ﵽthresholdʱ������Ҫ��HashMap�������ӱ���
        threshold = (int)(DEFAULT_INITIAL_CAPACITY * DEFAULT_LOAD_FACTOR);
        // ����Entry���飬������������
        table = new Entry[DEFAULT_INITIAL_CAPACITY];
        init();
    }
	
    // ��������Map���Ĺ��캯��
    public HashMap(Map<? extends K, ? extends V> m) {
        this(Math.max((int) (m.size() / DEFAULT_LOAD_FACTOR) + 1,
                      DEFAULT_INITIAL_CAPACITY), DEFAULT_LOAD_FACTOR);
        // ��m�е�ȫ��Ԫ�������ӵ�HashMap��
        putAllForCreate(m);
    }
	
    static int hash(int h) {
        h ^= (h >>> 20) ^ (h >>> 12);
        return h ^ (h >>> 7) ^ (h >>> 4);
    }
	
    // ��������ֵ
    // h & (length-1)��֤����ֵ��С��length
    static int indexFor(int h, int length) {
        return h & (length-1);
    }
	
    public int size() {
        return size;
    }
	
    public boolean isEmpty() {
        return size == 0;
    }
	
    // ��ȡkey��Ӧ��value
    public V get(Object key) {
        if (key == null)
            return getForNullKey();
        // ��ȡkey��hashֵ
        int hash = hash(key.hashCode());
        // �ڡ���hashֵ��Ӧ�������ϲ��ҡ���ֵ����key����Ԫ��
        for (Entry<K,V> e = table[indexFor(hash, table.length)];
             e != null;
             e = e.next) {
            Object k;
            if (e.hash == hash && ((k = e.key) == key || key.equals(k)))
                return e.value;
        }
        return null;
    }
	
    // ��ȡ��keyΪnull����Ԫ�ص�ֵ
    // HashMap����keyΪnull����Ԫ�ش洢��table[0]λ�ã�
    private V getForNullKey() {
        for (Entry<K,V> e = table[0]; e != null; e = e.next) {
            if (e.key == null)
                return e.value;
        }
        return null;
    }
	
    // HashMap�Ƿ����key
    public boolean containsKey(Object key) {
        return getEntry(key) != null;
    }
	
    // ���ء���Ϊkey���ļ�ֵ��
    final Entry<K,V> getEntry(Object key) {
        // ��ȡ��ϣֵ
        // HashMap����keyΪnull����Ԫ�ش洢��table[0]λ�ã���key��Ϊnull���������hash()�����ϣֵ
        int hash = (key == null) ? 0 : hash(key.hashCode());
        // �ڡ���hashֵ��Ӧ�������ϲ��ҡ���ֵ����key����Ԫ��
        for (Entry<K,V> e = table[indexFor(hash, table.length)];
             e != null;
             e = e.next) {
            Object k;
            if (e.hash == hash &&
                ((k = e.key) == key || (key != null && key.equals(k))))
                return e;
        }
        return null;
    }
	
    // ����key-value����ӵ�HashMap��
    public V put(K key, V value) {
        // ����keyΪnull�����򽫸ü�ֵ����ӵ�table[0]�С�
        if (key == null)
            return putForNullKey(value);
        // ����key��Ϊnull����������key�Ĺ�ϣֵ��Ȼ������ӵ��ù�ϣֵ��Ӧ�������С�
        int hash = hash(key.hashCode());
        int i = indexFor(hash, table.length);
        for (Entry<K,V> e = table[i]; e != null; e = e.next) {
            Object k;
            // ������key����Ӧ�ļ�ֵ���Ѿ����ڣ������µ�valueȡ���ɵ�value��Ȼ���˳���
            if (e.hash == hash && ((k = e.key) == key || key.equals(k))) {
                V oldValue = e.value;
                e.value = value;
                e.recordAccess(this);
                return oldValue;
            }
        }
        // ������key����Ӧ�ļ�ֵ�Բ����ڣ��򽫡�key-value����ӵ�table��
        modCount++;
        addEntry(hash, key, value, i);
        return null;
    }
	
    // putForNullKey()�������ǽ���keyΪnull����ֵ����ӵ�table[0]λ��
    private V putForNullKey(V value) {
        for (Entry<K,V> e = table[0]; e != null; e = e.next) {
            if (e.key == null) {
                V oldValue = e.value;
                e.value = value;
                e.recordAccess(this);
                return oldValue;
            }
        }
        // �������ȫ���ᱻִ�е�!
        modCount++;
        addEntry(0, null, value, 0);
        return null;
    }
	
    // ����HashMap��Ӧ�ġ���ӷ�������
    // ����put()��ͬ��putForCreate()���ڲ��������������캯���ȵ��ã���������HashMap
    // ��put()�Ƕ����ṩ����HashMap�����Ԫ�صķ�����
    private void putForCreate(K key, V value) {
        int hash = (key == null) ? 0 : hash(key.hashCode());
        int i = indexFor(hash, table.length);
        // ����HashMap���д��ڡ���ֵ����key����Ԫ�أ����滻��Ԫ�ص�valueֵ
        for (Entry<K,V> e = table[i]; e != null; e = e.next) {
            Object k;
            if (e.hash == hash &&
                ((k = e.key) == key || (key != null && key.equals(k)))) {
                e.value = value;
                return;
            }
        }
        // ����HashMap���в����ڡ���ֵ����key����Ԫ�أ��򽫸�key-value��ӵ�HashMap��
        createEntry(hash, key, value, i);
    }
	
    // ����m���е�ȫ��Ԫ�ض���ӵ�HashMap�С�
    // �÷������ڲ��Ĺ���HashMap�ķ��������á�
    private void putAllForCreate(Map<? extends K, ? extends V> m) {
        // ���õ�������Ԫ�������ӵ�HashMap��
        for (Iterator<? extends Map.Entry<? extends K, ? extends V>> i = m.entrySet().iterator(); i.hasNext(); ) {
            Map.Entry<? extends K, ? extends V> e = i.next();
            putForCreate(e.getKey(), e.getValue());
        }
    }
	
    // ���µ���HashMap�Ĵ�С��newCapacity�ǵ�����ĵ�λ
    void resize(int newCapacity) {
        Entry[] oldTable = table;
        int oldCapacity = oldTable.length;
        if (oldCapacity == MAXIMUM_CAPACITY) {
            threshold = Integer.MAX_VALUE;
            return;
        }
        // �½�һ��HashMap��������HashMap����ȫ��Ԫ����ӵ�����HashMap���У�
        // Ȼ�󣬽�����HashMap����ֵ������HashMap����
        Entry[] newTable = new Entry[newCapacity];
        transfer(newTable);
        table = newTable;
        threshold = (int)(newCapacity * loadFactor);
    }
	
    // ��HashMap�е�ȫ��Ԫ�ض���ӵ�newTable��
    void transfer(Entry[] newTable) {
        Entry[] src = table;
        int newCapacity = newTable.length;
        for (int j = 0; j < src.length; j++) {
            Entry<K,V> e = src[j];
            if (e != null) {
                src[j] = null;
                do {
                    Entry<K,V> next = e.next;
                    int i = indexFor(e.hash, newCapacity);
                    e.next = newTable[i];
                    newTable[i] = e;
                    e = next;
                } while (e != null);
            }
        }
    }
	
    // ��"m"��ȫ��Ԫ�ض���ӵ�HashMap��
    public void putAll(Map<? extends K, ? extends V> m) {
        // ��Ч���ж�
        int numKeysToBeAdded = m.size();
        if (numKeysToBeAdded == 0)
            return;
        // ���������Ƿ��㹻��
        // ������ǰʵ������ < ��Ҫ����������������x2��
        if (numKeysToBeAdded > threshold) {
            int targetCapacity = (int)(numKeysToBeAdded / loadFactor + 1);
            if (targetCapacity > MAXIMUM_CAPACITY)
                targetCapacity = MAXIMUM_CAPACITY;
            int newCapacity = table.length;
            while (newCapacity < targetCapacity)
                newCapacity <<= 1;
            if (newCapacity > table.length)
                resize(newCapacity);
        }
        // ͨ��������������m���е�Ԫ�������ӵ�HashMap�С�
        for (Iterator<? extends Map.Entry<? extends K, ? extends V>> i = m.entrySet().iterator(); i.hasNext(); ) {
            Map.Entry<? extends K, ? extends V> e = i.next();
            put(e.getKey(), e.getValue());
        }
    }
	
    // ɾ������Ϊkey��Ԫ��
    public V remove(Object key) {
        Entry<K,V> e = removeEntryForKey(key);
        return (e == null ? null : e.value);
    }
	
    // ɾ������Ϊkey����Ԫ��
    final Entry<K,V> removeEntryForKey(Object key) {
        // ��ȡ��ϣֵ����keyΪnull�����ϣֵΪ0���������hash()���м���
        int hash = (key == null) ? 0 : hash(key.hashCode());
        int i = indexFor(hash, table.length);
        Entry<K,V> prev = table[i];
        Entry<K,V> e = prev;
        // ɾ�������С���Ϊkey����Ԫ��
        // �����ǡ�ɾ�����������еĽڵ㡱
        while (e != null) {
            Entry<K,V> next = e.next;
            Object k;
            if (e.hash == hash &&
                ((k = e.key) == key || (key != null && key.equals(k)))) {
                modCount++;
                size--;
                if (prev == e)
                    table[i] = next;
                else
                    prev.next = next;
                e.recordRemoval(this);
                return e;
            }
            prev = e;
            e = next;
        }
        return e;
    }
	
    // ɾ������ֵ�ԡ�
    final Entry<K,V> removeMapping(Object o) {
        if (!(o instanceof Map.Entry))
            return null;
        Map.Entry<K,V> entry = (Map.Entry<K,V>) o;
        Object key = entry.getKey();
        int hash = (key == null) ? 0 : hash(key.hashCode());
        int i = indexFor(hash, table.length);
        Entry<K,V> prev = table[i];
        Entry<K,V> e = prev;
        // ɾ�������еġ���ֵ��e��
        // �����ǡ�ɾ�����������еĽڵ㡱
        while (e != null) {
            Entry<K,V> next = e.next;
            if (e.hash == hash && e.equals(entry)) {
                modCount++;
                size--;
                if (prev == e)
                    table[i] = next;
                else
                    prev.next = next;
                e.recordRemoval(this);
                return e;
            }
            prev = e;
            e = next;
        }
        return e;
    }
	
    // ���HashMap�������е�Ԫ����Ϊnull
    public void clear() {
        modCount++;
        Entry[] tab = table;
        for (int i = 0; i < tab.length; i++)
            tab[i] = null;
        size = 0;
    }
	
    // �Ƿ������ֵΪvalue����Ԫ��
    public boolean containsValue(Object value) {
    // ����valueΪnull���������containsNullValue()����
    if (value == null)
            return containsNullValue();
    // ����value��Ϊnull���������HashMap���Ƿ���ֵΪvalue�Ľڵ㡣
    Entry[] tab = table;
        for (int i = 0; i < tab.length ; i++)
            for (Entry e = tab[i] ; e != null ; e = e.next)
                if (value.equals(e.value))
                    return true;
    return false;
    }
	
    // �Ƿ����nullֵ
    private boolean containsNullValue() {
    Entry[] tab = table;
        for (int i = 0; i < tab.length ; i++)
            for (Entry e = tab[i] ; e != null ; e = e.next)
                if (e.value == null)
                    return true;
    return false;
    }
	
    // ��¡һ��HashMap��������Object����
    public Object clone() {
        HashMap<K,V> result = null;
        try {
            result = (HashMap<K,V>)super.clone();
        } catch (CloneNotSupportedException e) {
            // assert false;
        }
        result.table = new Entry[table.length];
        result.entrySet = null;
        result.modCount = 0;
        result.size = 0;
        result.init();
        // ����putAllForCreate()��ȫ��Ԫ����ӵ�HashMap��
        result.putAllForCreate(this);
        return result;
    }
	
    // Entry�ǵ�������
    // ���� ��HashMap��ʽ�洢������Ӧ������
    // ��ʵ����Map.Entry �ӿڣ���ʵ��getKey(), getValue(), setValue(V value), equals(Object o), hashCode()��Щ����
    static class Entry<K,V> implements Map.Entry<K,V> {
        final K key;
        V value;
        // ָ����һ���ڵ�
        Entry<K,V> next;
        final int hash;
        // ���캯����
        // �����������"��ϣֵ(h)", "��(k)", "ֵ(v)", "��һ�ڵ�(n)"
        Entry(int h, K k, V v, Entry<K,V> n) {
            value = v;
            next = n;
            key = k;
            hash = h;
        }
        public final K getKey() {
            return key;
        }
        public final V getValue() {
            return value;
        }
        public final V setValue(V newValue) {
            V oldValue = value;
            value = newValue;
            return oldValue;
        }
        // �ж�����Entry�Ƿ����
        // ������Entry�ġ�key���͡�value������ȣ��򷵻�true��
        // ���򣬷���false
        public final boolean equals(Object o) {
            if (!(o instanceof Map.Entry))
                return false;
            Map.Entry e = (Map.Entry)o;
            Object k1 = getKey();
            Object k2 = e.getKey();
            if (k1 == k2 || (k1 != null && k1.equals(k2))) {
                Object v1 = getValue();
                Object v2 = e.getValue();
                if (v1 == v2 || (v1 != null && v1.equals(v2)))
                    return true;
            }
            return false;
        }
        // ʵ��hashCode()
        public final int hashCode() {
            return (key==null   ? 0 : key.hashCode()) ^
                   (value==null ? 0 : value.hashCode());
        }
        public final String toString() {
            return getKey() + "=" + getValue();
        }
        // ����HashMap�����Ԫ��ʱ�������recordAccess()��
        // ���ﲻ���κδ���
        void recordAccess(HashMap<K,V> m) {
        }
        // ����HashMap��ɾ��Ԫ��ʱ�������recordRemoval()��
        // ���ﲻ���κδ���
        void recordRemoval(HashMap<K,V> m) {
        }
    }
	
    // ����Entry������key-value������ָ��λ�ã�bucketIndex��λ��������
    void addEntry(int hash, K key, V value, int bucketIndex) {
        // ���桰bucketIndex��λ�õ�ֵ����e����
        Entry<K,V> e = table[bucketIndex];
        // ���á�bucketIndex��λ�õ�Ԫ��Ϊ����Entry����
        // ���á�e��Ϊ����Entry����һ���ڵ㡱
        table[bucketIndex] = new Entry<K,V>(hash, key, value, e);
        // ��HashMap��ʵ�ʴ�С ��С�� ����ֵ���������HashMap�Ĵ�С
        if (size++ >= threshold)
            resize(2 * table.length);
    }
	
    // ����Entry������key-value������ָ��λ�ã�bucketIndex��λ��������
    // ����addEntry�������ǣ�
    // (01) addEntry()һ������ ����Entry���ܵ��¡�HashMap��ʵ����������������ֵ��������¡�
    //   ���磬�����½�һ��HashMap��Ȼ�󲻶�ͨ��put()��HashMap�����Ԫ�أ�
    // put()��ͨ��addEntry()����Entry�ġ�
    //   ����������£����ǲ�֪����ʱ��HashMap��ʵ���������ᳬ������ֵ����
    //   ��ˣ���Ҫ����addEntry()
    // (02) createEntry() һ������ ����Entry���ᵼ�¡�HashMap��ʵ����������������ֵ��������¡�
    //   ���磬���ǵ���HashMap������Map���Ĺ��캯�������潫Map��ȫ��Ԫ����ӵ�HashMap�У�
    // �������֮ǰ�������Ѿ�����á�HashMap����������ֵ����Ҳ���ǣ�����ȷ������ʹ��Map��
    // ��ȫ��Ԫ����ӵ�HashMap�У������ᳬ��HashMap����ֵ����
    //   ��ʱ������createEntry()���ɡ�
    void createEntry(int hash, K key, V value, int bucketIndex) {
        // ���桰bucketIndex��λ�õ�ֵ����e����
        Entry<K,V> e = table[bucketIndex];
        // ���á�bucketIndex��λ�õ�Ԫ��Ϊ����Entry����
        // ���á�e��Ϊ����Entry����һ���ڵ㡱
        table[bucketIndex] = new Entry<K,V>(hash, key, value, e);
        size++;
    }
	
    // HashIterator��HashMap�������ĳ�������ĸ��࣬ʵ���˹����˺�����
    // ��������key������(KeyIterator)������Value������(ValueIterator)���͡�Entry������(EntryIterator)��3�����ࡣ
    private abstract class HashIterator<E> implements Iterator<E> {
        // ��һ��Ԫ��
        Entry<K,V> next;
        // expectedModCount����ʵ��fast-fail���ơ�
        int expectedModCount;
        // ��ǰ����
        int index;
        // ��ǰԪ��
        Entry<K,V> current;
        HashIterator() {
            expectedModCount = modCount;
            if (size > 0) { // advance to first entry
                Entry[] t = table;
                // ��nextָ��table�е�һ����Ϊnull��Ԫ�ء�
                // ����������index�ĳ�ʼֵΪ0����0��ʼ������������ֱ���ҵ���Ϊnull��Ԫ�ؾ��˳�ѭ����
                while (index < t.length && (next = t[index++]) == null)

            }
        }
        public final boolean hasNext() {
            return next != null;
        }
        // ��ȡ��һ��Ԫ��
        final Entry<K,V> nextEntry() {
            if (modCount != expectedModCount)
                throw new ConcurrentModificationException();
            Entry<K,V> e = next;
            if (e == null)
                throw new NoSuchElementException();
            // ע�⣡����
            // һ��Entry����һ����������
            // ����Entry����һ���ڵ㲻Ϊ�գ��ͽ�nextָ����һ���ڵ�;
            // ���򣬽�nextָ����һ������(Ҳ����һ��Entry)�Ĳ�Ϊnull�Ľڵ㡣
            if ((next = e.next) == null) {
                Entry[] t = table;
                while (index < t.length && (next = t[index++]) == null)

            }
            current = e;
            return e;
        }
        // ɾ����ǰԪ��
        public void remove() {
            if (current == null)
                throw new IllegalStateException();
            if (modCount != expectedModCount)
                throw new ConcurrentModificationException();
            Object k = current.key;
            current = null;
            HashMap.this.removeEntryForKey(k);
            expectedModCount = modCount;
        }
    }
    // value�ĵ�����
    private final class ValueIterator extends HashIterator<V> {
        public V next() {
            return nextEntry().value;
        }
    }
    // key�ĵ�����
    private final class KeyIterator extends HashIterator<K> {
        public K next() {
            return nextEntry().getKey();
        }
    }
    // Entry�ĵ�����
    private final class EntryIterator extends HashIterator<Map.Entry<K,V>> {
        public Map.Entry<K,V> next() {
            return nextEntry();
        }
    }
    // ����һ����key��������
    Iterator<K> newKeyIterator()   {
        return new KeyIterator();
    }
    // ����һ����value��������
    Iterator<V> newValueIterator()   {
        return new ValueIterator();
    }
    // ����һ����entry��������
    Iterator<Map.Entry<K,V>> newEntryIterator()   {
        return new EntryIterator();
    }
    // HashMap��Entry��Ӧ�ļ���
    private transient Set<Map.Entry<K,V>> entrySet = null;
    // ���ء�key�ļ��ϡ���ʵ���Ϸ���һ����KeySet����
    public Set<K> keySet() {
        Set<K> ks = keySet;
        return (ks != null ? ks : (keySet = new KeySet()));
    }
    // Key��Ӧ�ļ���
    // KeySet�̳���AbstractSet��˵���ü�����û���ظ���Key��
    private final class KeySet extends AbstractSet<K> {
        public Iterator<K> iterator() {
            return newKeyIterator();
        }
        public int size() {
            return size;
        }
        public boolean contains(Object o) {
            return containsKey(o);
        }
        public boolean remove(Object o) {
            return HashMap.this.removeEntryForKey(o) != null;
        }
        public void clear() {
            HashMap.this.clear();
        }
    }
    // ���ء�value���ϡ���ʵ���Ϸ��ص���һ��Values����
    public Collection<V> values() {
        Collection<V> vs = values;
        return (vs != null ? vs : (values = new Values()));
    }
    // ��value���ϡ�
    // Values�̳���AbstractCollection����ͬ�ڡ�KeySet�̳���AbstractSet����
    // Values�е�Ԫ���ܹ��ظ�����Ϊ��ͬ��key����ָ����ͬ��value��
    private final class Values extends AbstractCollection<V> {
        public Iterator<V> iterator() {
            return newValueIterator();
        }
        public int size() {
            return size;
        }
        public boolean contains(Object o) {
            return containsValue(o);
        }
        public void clear() {
            HashMap.this.clear();
        }
    }
    // ���ء�HashMap��Entry���ϡ�
    public Set<Map.Entry<K,V>> entrySet() {
        return entrySet0();
    }
    // ���ء�HashMap��Entry���ϡ�����ʵ���Ƿ���һ��EntrySet����
    private Set<Map.Entry<K,V>> entrySet0() {
        Set<Map.Entry<K,V>> es = entrySet;
        return es != null ? es : (entrySet = new EntrySet());
    }
    // EntrySet��Ӧ�ļ���
    // EntrySet�̳���AbstractSet��˵���ü�����û���ظ���EntrySet��
    private final class EntrySet extends AbstractSet<Map.Entry<K,V>> {
        public Iterator<Map.Entry<K,V>> iterator() {
            return newEntryIterator();
        }
        public boolean contains(Object o) {
            if (!(o instanceof Map.Entry))
                return false;
            Map.Entry<K,V> e = (Map.Entry<K,V>) o;
            Entry<K,V> candidate = getEntry(e.getKey());
            return candidate != null && candidate.equals(e);
        }
        public boolean remove(Object o) {
            return removeMapping(o) != null;
        }
        public int size() {
            return size;
        }
        public void clear() {
            HashMap.this.clear();
        }
    }
    // java.io.Serializable��д�뺯��
    // ��HashMap�ġ��ܵ�������ʵ�����������е�Entry����д�뵽�������
    private void writeObject(java.io.ObjectOutputStream s)
        throws IOException
    {
        Iterator<Map.Entry<K,V>> i =
            (size > 0) ? entrySet0().iterator() : null;
        // Write out the threshold, loadfactor, and any hidden stuff
        s.defaultWriteObject();
        // Write out number of buckets
        s.writeInt(table.length);
        // Write out size (number of Mappings)
        s.writeInt(size);
        // Write out keys and values (alternating)
        if (i != null) {
            while (i.hasNext()) {
            Map.Entry<K,V> e = i.next();
            s.writeObject(e.getKey());
            s.writeObject(e.getValue());
            }
        }
    }
    private static final long serialVersionUID = 362498820763181265L;
    // java.io.Serializable�Ķ�ȡ����������д�뷽ʽ����
    // ��HashMap�ġ��ܵ�������ʵ�����������е�Entry�����ζ���
    private void readObject(java.io.ObjectInputStream s)
         throws IOException, ClassNotFoundException
    {
        // Read in the threshold, loadfactor, and any hidden stuff
        s.defaultReadObject();
        // Read in number of buckets and allocate the bucket array;
        int numBuckets = s.readInt();
        table = new Entry[numBuckets];
        init();  // Give subclass a chance to do its thing.
        // Read in size (number of Mappings)
        int size = s.readInt();
        // Read the keys and values, and put the mappings in the HashMap
        for (int i=0; i<size; i++) {
            K key = (K) s.readObject();
            V value = (V) s.readObject();
            putForCreate(key, value);
        }
    }
    // ���ء�HashMap�ܵ�������
    int   capacity()     { return table.length; }
    // ���ء�HashMap�ļ������ӡ�
    float loadFactor()   { return loadFactor;   }
}
```

 - ��public V get(Object key)�����У�

�������key��Ϊnull���������key��hashֵ������hashֵ�ҵ���table�е��������ڸ�������Ӧ�ĵ������в����Ƿ��м�ֵ�Ե�key��Ŀ��key��ȣ��оͷ��ض�Ӧ��value��û���򷵻�null��
�������keyΪnull����ֱ�Ӵӹ�ϣ��ĵ�һ��λ��table[0]��Ӧ�������ϲ��ҡ���ס��keyΪnull�ļ�ֵ����Զ��������table[0]Ϊͷ���������У���Ȼ��һ���Ǵ����ͷ���table[0]�С�

 - public V put(K key, V value) �����У�

���� ���key��Ϊnull����ͬ�������key��hashֵ������hashֵ�ó���table�е����������������Ӧ�ĵ���������������д�����Ŀ��key��ȵļ�ֵ�ԣ����µ�value���Ǿɵ�value�������ɵ�value���أ�����Ҳ�����Ŀ��key��ȵļ�ֵ�ԣ����߸õ�����Ϊ�գ��򽫸ü�ֵ�Բ��뵽�ĵ������ͷ���λ�ã�ÿ���²���Ľڵ㶼�Ƿ���ͷ����λ�ã����ò�������addEntry����ʵ�ֵģ�����Դ�����£�

```
  void addEntry(int hash, K key, V value, int bucketIndex) {
        Entry<K,V> e = table[bucketIndex]; //���Ҫ�����λ����ֵ������λ��ԭ�ȵ�ֵ����Ϊ��entry��next,Ҳ������entry�������һ���ڵ�
        table[bucketIndex] = new Entry<>(hash, key, value, e);
        if (size++ >= threshold) //��������ٽ�ֵ������
            resize(2 * table.length); //��2�ı�������
    }
```
��������bucketIndex����indexFor�����������������ֵ����2�д�����ȡ������������ΪbucketIndex��Entry���󣬵�3�о�����hash��key��value����һ���µ�Entry����ŵ�����ΪbucketIndex��λ�ã����ҽ���λ��ԭ�ȵĶ�������Ϊ�¶����next����������4�к͵�5�о����ж�put��size�Ƿ�ﵽ���ٽ�ֵthreshold������ﵽ���ٽ�ֵ��Ҫ�������ݣ�HashMap��������Ϊԭ����������


�������keyΪnull��������ӵ�table[0]��Ӧ�������У���putForNullKey����ʵ�֡�

����

```
    // putForNullKey()�������ǽ���keyΪnull����ֵ����ӵ�table[0]λ��  
    private V putForNullKey(V value) {  
        for (Entry<K,V> e = table[0]; e != null; e = e.next) {  
            if (e.key == null) {  
                V oldValue = e.value;  
                e.value = value;  
                e.recordAccess(this);  
                return oldValue;  
            }  
        }  
        // ���û�д���keyΪnull�ļ�ֵ�ԣ���ֱ���Ⱒ����table[0]��!  
        modCount++;  
        addEntry(0, null, value, 0);  
        return null;  
    } 
```

 - resize���ݷ���

```
   void resize(int newCapacity) {
        Entry[] oldTable = table;
        int oldCapacity = oldTable.length;
        if (oldCapacity == MAXIMUM_CAPACITY) {
            threshold = Integer.MAX_VALUE;
            return;
        }

        Entry[] newTable = new Entry[newCapacity];
        transfer(newTable);//������ԭ��table��Ԫ��ȫ���Ƶ�newTable����
        table = newTable;  //�ٽ�newTable��ֵ��table
        threshold = (int)(newCapacity * loadFactor);//���¼����ٽ�ֵ
    } 
```
�������½���һ��HashMap�ĵײ����飬�������transfer����������HashMap��ȫ��Ԫ����ӵ��µ�HashMap�У�Ҫ���¼���Ԫ�����µ������е�����λ�ã���
������������Ҫ�������鸴�Ƶģ��ǳ��������ܵĲ�����������������Ѿ�Ԥ֪HashMap��Ԫ�صĸ�������ôԤ��Ԫ�صĸ����ܹ���Ч�����HashMap�����ܡ�

```
    // ��HashMap�е�ȫ��Ԫ�ض���ӵ�newTable��  
    void transfer(Entry[] newTable) {  
        Entry[] src = table;  
        int newCapacity = newTable.length;  
        for (int j = 0; j < src.length; j++) {  
            Entry<K,V> e = src[j];  
            if (e != null) {  
                src[j] = null;  
                do {  
                    Entry<K,V> next = e.next;  
                    int i = indexFor(e.hash, newCapacity);  
                    e.next = newTable[i];  
                    newTable[i] = e;  
                    e = next;  
                } while (e != null);  
            }  
        }  
    }  
```

 - �����ϣֵ�ķ���

```
static int hash(int h) {
        h ^= (h >>> 20) ^ (h >>> 12);
        return h ^ (h >>> 7) ^ (h >>> 4);
    }
```

��λ�Ĳ���ʹhashֵ�ļ���Ч�ʸ��ߡ�


 - ��hashֵ�ҵ���Ӧ�����ķ���

```
static int indexFor(int h, int length) {
        return h & (length-1);
    }
```

����HashMap����ͨ��h&(length-1)�ķ���������ȡģ��ͬ��ʵ���˾��ȵ�ɢ�У���Ч��Ҫ�ߺܶ࣬��Ҳ��HashMap��Hashtable��һ���Ľ���
����lengthΪ2���������ݵĻ���h&(length-1)���൱�ڶ�lengthȡģ�������㱣֤��ɢ�еľ��ȣ�ͬʱҲ������Ч�ʣ�

> lengthΪ2���������ݵĻ���Ϊż��������length-1Ϊ���������������һλ��1�������㱣֤��h&(length-1)�����һλ����Ϊ0��Ҳ����Ϊ1����ȡ����h��ֵ���������Ľ������Ϊż����Ҳ����Ϊ��������������Ա�֤ɢ�еľ����ԣ������lengthΪ�����Ļ���������length-1Ϊż�����������һλ��0������h&(length-1)�����һλ�϶�Ϊ0����ֻ��Ϊż���������κ�hashֵ��ֻ�ᱻɢ�е������ż���±�λ���ϣ�����˷��˽�һ��Ŀռ䡣

#4.HashMap��ConcurrentHashMap������

����ConcurrentHashMap����hashMap�Ļ����ϣ������ݷ�Ϊ���segment(����hashtable)��Ĭ��16����concurrency level����Ȼ����ÿһ���ֶ��϶��������б������Ӷ����������ȸ���ϸһЩ���������ܸ��á�


 