## 底层数据结构
- Array
- Linked
- Hashtable
- Tree
- Graph
## java数据结构框架
1. I-Collection
    1. I-List (An ordered collection)
        1. C-ArrayList implements List<E>, RandomAccess
        2. C-LinkedList implements List<E>, Deque<E>,
    2. I-Set
        1. C-HashSet
        2. C-TreeSet
        3. LinkedHashSet
    3. I-Queue
        1. I-Dqueue 双向队列
            1. C-LinkedList
            2. C-ArrayQueue implements Deque<E>
2. I-Map
    1. C-Hashmap implements Map<K,V>
    2. C-LinkedHashMap 通过双向链表的方式封装了hashtable的逻辑，可以使用链表的方式访问
    3. C-Hashtable 
    3. C-Treemap
I-RandomAccess(Marker interface used by {@code List} implementations to indicate that they support fast (generally constant time) random access.  )标识实现这个接口的list子类，随机访问的时间复杂度是常量级别。
## Collection接口定义的特征，包括方法和属性
``` java


```
## List 接口定义
## ArrayList 底层通过扩容数组实现的有序集合
- implements List<E>, RandomAccess
- 排列有序，可重复
- 底层使用数组
- 查询O(1),增加和删除O(n)
- 线程不安全
- 基本根据index进行增删改查操作。
- 扩容策略
    1. 调用空参数构造方法，data为一个空数组
    2. 增加一个元素时，由于size=1> data.length=0 的，触发扩容，data的长度使用了默认值10.
    3. 当增加第11个元素时，由于size=11 > data.length=10 的，触发扩容，data.length= (old+old<<1) ,即旧长度的1.5倍，new length =15
    ``` java

        public boolean add(E e) {
        modCount++;
        add(e, elementData, size);
        return true;
    }
    
    private void add(E e, Object[] elementData, int s) {
        if (s == elementData.length)
        elementData = grow();
        elementData[s] = e;
        size = s + 1;
    }   

    private Object[] grow() {
        return grow(size + 1);
    }
    private Object[] grow(int minCapacity) {
        return elementData = Arrays.copyOf(elementData,
                                        newCapacity(minCapacity));
    }
    
    private int newCapacity(int minCapacity) {
    //扩容逻辑:
    //如果旧容量1.5倍后依然<默认值10，新容量为10；如果1.5倍后>10，新容量为旧容量的1,5倍值。
    //如果新容量小于数组容量最大值（Integer.max-8),使用新容量，如果大于，使用最大值。


        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity <= 0) {
            if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA)
                return Math.max(DEFAULT_CAPACITY, minCapacity);
            if (minCapacity < 0) // overflow
                throw new OutOfMemoryError();
            return minCapacity;
        }
        return (newCapacity - MAX_ARRAY_SIZE <= 0)
            ? newCapacity
            : hugeCapacity(minCapacity);
    }

    ```
## LinkedList 底层通过双向链表实现的有序集合
- implements List<E>, Deque<E>
- 底层使用双向链表
- 线程不安全
- 查询慢，增删快
- 比着ArrayList增加了一些从双向链表的头和尾增删改查数据的方法。
- 先进先出，队列的特征就是先进先出
- peek()获取到第一个值，但是不删除，只是查看第一个值
- pool()获取到第一个值，并删除。
```java 
    transient int size = 0;

    /**
     * Pointer to first node.
     */
    transient Node<E> first;

    /**
     * Pointer to last node.
     */
    transient Node<E> last;


private static class Node<E> {
        E item;
        Node<E> next;
        Node<E> prev;

        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
    }
```
## HashSet 
- 排列无序不可重复
- 组合了一个HashMap属性map
- 使用的是HashMap的key，value统一使用的同一个object
## Hashmap
- 键不可重复，值可以重复
- 底层hash表
- 线程不安全
- key和value都可以为Null
- 初始化大小为16，懒初始化，每次扩容新容量等于旧容量*2
``` java
    public class HashMap<K,V> extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable{
        //初始化大小6
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16
    //最大容量
    static final int MAXIMUM_CAPACITY = 1 << 30;
    //负载因子，到这个值时开始扩容，不会等到大于容量时再扩容
    static final float DEFAULT_LOAD_FACTOR = 0.75f;
    //单个链表上最多挂载8个node，就要转换为红黑树了，添加第8个时，就要转换了，所以实际能存在的最长链表其实是7个node
    static final int TREEIFY_THRESHOLD = 8;
    //单个卡槽，如果node少于6个就要恢复为链表的形式，
    static final int UNTREEIFY_THRESHOLD = 6;
    //如果容量小于64，单个链表上node数量也已经到第8个了，那么优先扩容。
    static final int MIN_TREEIFY_CAPACITY = 64;

    }
```
- 单向链表和红黑树
## LinkedHashMap
## Treemap
- 使用红黑树实现 自平衡二叉树
- 有序，可导航的
- NavigableMap的主要功能
    1. Map.Entry<K,V> lowerEntry(K key); 获取仅次于当前key的键值对
    2. Map.Entry<K,V> floorEntry(K key); 获取仅次于或者等于当前key的键值对
    3. Map.Entry<K,V> firstEntry(); 获取key值最大的键值对
- SortedMap的主要功能
    1.     SortedMap<K,V> subMap(K fromKey, K toKey); 获取key值在from和to之间的子map。
    2.     SortedMap<K,V> headMap(K toKey); 获取比当前key值大的所有键值对组成的map
    3.     SortedMap<K,V> tailMap(K fromKey); 获取当前key小的所有键值对组成的map
    4.     K firstKey(); 获取最大的key
    5.     K lastKey(); 获取最小的key
```java
public class TreeMap<K,V>
    extends AbstractMap<K,V>
    implements NavigableMap<K,V>{
        //public interface NavigableMap<K,V> extends SortedMap<K,V> 

    }
```