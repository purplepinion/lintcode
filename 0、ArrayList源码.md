### 一、ArrayList源码总结

##### 继承关系

ArrayList在java.util包下。

ArrayList继承AbstractList类、实现List接口。

并且继承RandomAccess, Cloneable, java.io.Serializable接口。支持随机访问，克隆，序列化。

##### 底层实现

> 底层是一个Object数组
>
> transient Object[] elementData
>
> 默认容量大小10
>
> private static final int DEFAULT_CAPACITY = 10;
>
> 扩容倍数1.5
> int newCapacity = oldCapacity + (oldCapacity >> 1);

##### 遍历方式

```java
//1、通过迭代器遍历：
Iterator iter = list.iterator();
    while (iter.hasNext())
    {
        System.out.println(iter.next());
    }     
//2、随机访问，通过索引值去遍历，由于ArrayList实现了RandomAccess接口
 int size = list.size();
    for (int i=0; i<size; i++) 
    {
        System.out.println(list.get(i));        
    }    
//3、for循环遍历：
for(String str:list)
    {
    System.out.println(str);
　　 }  
```

##### 主要方法

```java
//带初始容量的构造函数
public ArrayList(int initialCapacity) ;
//无参构造函数,默认容量为10
public ArrayList();
//创建一个包含collection的ArrayList
public ArrayList(Collection<? extends E> c);
//ArrayList实际大小
public int size();
//判断ArrayList是否为空
public boolean isEmpty();
//判断ArrayList中是否有元素o
public boolean contains(Object o);
//返回指定元素的下标（从前向后）、返回值大于0找到，-1为没找到
public int indexOf(Object o);
//返回指定元素的下标（从后向前）、返回值大于0找到，-1为没找到
public int lastIndexOf(Object o);
//返回此 ArrayList实例的浅拷贝。
public Object clone()
//返回一个包含ArrayList中所有元素的Object数组
public Object[] toArray();
//传入一个指定类型数组，返回一个指定类型数组
@SuppressWarnings("unchecked")
public <T> T[] toArray(T[] a) ;
//返回指定index运行时类型元素，
@SuppressWarnings("unchecked")
E elementData(int index) ;
//返回指定index运行时类型元素，
public E get(int index);
//替换指定index位置的元素，并返回原来元素的值
public E set(int index, E element) 
//添加一个元素、若ArrayList容量小于size+1、1.5倍扩容
public boolean add(E e) ;
//指定index添加元素
public void add(int index, E element);
//删除制定index元素，返回值
public E remove(int index) ;
//查找指定元素并删除
public boolean remove(Object o) ;
//删除所有元素，并置null，有利于GC
public void clear() ;
//添加Collection类型所有元素到ArrayList
public boolean addAll(Collection<? extends E> c) ;
//插入Collection类型所有元素到ArrayList指定index
public boolean addAll(int index, Collection<? extends E> c) ;
//移除指定index区间的元素
protected void removeRange(int fromIndex, int toIndex) ;
//删除ArrayList中包含在c中的元素
public boolean removeAll(Collection<?> c) ;
//删除ArrayList中除包含在c中的元素，和removeAll相反
public boolean retainAll(Collection<?> c) ;
//返回list迭代器
public ListIterator<E> listIterator() ;
//返回collection迭代器
public Iterator<E> iterator() ;
//返回指定范围的subArrayList
public List<E> subList(int fromIndex, int toIndex) ；
```



### 二、ArrayList源码注释版

```java
package java.util;

public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{
	//序列化ID
    private static final long serialVersionUID = 8683452581122892189L;
	//默认初始容量10
    private static final int DEFAULT_CAPACITY = 10;
    private static final Object[] EMPTY_ELEMENTDATA = {};
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
    transient Object[] elementData; 
	//ArrayList实际容量
    private int size;
	//带初始容量的构造函数
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {//初始容量大于0,实例化数组
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {//初始化等于0，将空数组赋给elementData
            this.elementData = EMPTY_ELEMENTDATA;
        } else {//初始容量小于0，抛异常
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }
	//无参构造函数,默认容量为10
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }
    //创建一个包含collection的ArrayList
    public ArrayList(Collection<? extends E> c) {
        elementData = c.toArray();//返回包含c所有元素的数组
        if ((size = elementData.length) != 0) {
            // c.toArray might (incorrectly) not return Object[] (see 6260652)
            //BUG详细介绍博客：https://blog.csdn.net/aitangyong/article/details/30274749
            if (elementData.getClass() != Object[].class)
                //复制指定数组，使elementData具有指定长度
                elementData = Arrays.copyOf(elementData, size, Object[].class);
        } else {
            // replace with empty array.
            this.elementData = EMPTY_ELEMENTDATA;
        }
    }

   //将当前容量值设为当前实际元素大小
    public void trimToSize() {
        modCount++;
        if (size < elementData.length) {
            elementData = (size == 0)
              ? EMPTY_ELEMENTDATA
              : Arrays.copyOf(elementData, size);
        }
    }

    //将集合的capacity增加minCapacity
    public void ensureCapacity(int minCapacity) {
        int minExpand = (elementData != DEFAULTCAPACITY_EMPTY_ELEMENTDATA)
            ? 0: DEFAULT_CAPACITY;
        if (minCapacity > minExpand) {
            ensureExplicitCapacity(minCapacity);
        }
    }
    private static int calculateCapacity(Object[] elementData, int minCapacity) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        }
        return minCapacity;
    }
    private void ensureCapacityInternal(int minCapacity) {
        ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
    }
    private void ensureExplicitCapacity(int minCapacity) {
        modCount++;
        // overflow-conscious code
        if (minCapacity - elementData.length > 0)
            grow(minCapacity);
    }
	//数组最大大小Integer.MAX_VALUE - 8
    private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;
    private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        //每次扩容1.5倍
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }

    private static int hugeCapacity(int minCapacity) {
        if (minCapacity < 0) // overflow
            throw new OutOfMemoryError();
        return (minCapacity > MAX_ARRAY_SIZE) ?
            Integer.MAX_VALUE :
            MAX_ARRAY_SIZE;
    }
	//ArrayList实际大小
    public int size() {
        return size;
    }
	//判断ArrayList是否为空
    public boolean isEmpty() {
        return size == 0;
    }
	//判断ArrayList中是否有元素o
    public boolean contains(Object o) {
        return indexOf(o) >= 0;
    }
	//返回指定元素的下标（从前向后）、返回值大于0找到，-1为没找到
    public int indexOf(Object o) {
    	//注意空元素特殊处理
        if (o == null) {
            for (int i = 0; i < size; i++)
                if (elementData[i]==null)
                    return i;
        } else {
            for (int i = 0; i < size; i++)
                if (o.equals(elementData[i]))
                    return i;
        }
        return -1;
    }
	//返回指定元素的下标（从后向前）、返回值大于0找到，-1为没找到
    public int lastIndexOf(Object o) {
    	//注意空元素特殊处理
        if (o == null) {
            for (int i = size-1; i >= 0; i--)
                if (elementData[i]==null)
                    return i;
        } else {
            for (int i = size-1; i >= 0; i--)
                if (o.equals(elementData[i]))
                    return i;
        }
        return -1;
    }
	//返回此 ArrayList实例的浅拷贝。
    public Object clone() {
        try {
            ArrayList<?> v = (ArrayList<?>) super.clone();
            v.elementData = Arrays.copyOf(elementData, size);
            v.modCount = 0;
            return v;
        } catch (CloneNotSupportedException e) {
            // this shouldn't happen, since we are Cloneable
            throw new InternalError(e);
        }
    }
	//返回一个包含ArrayList中所有元素的Object数组
    public Object[] toArray() {
        return Arrays.copyOf(elementData, size);
    }
	//传入一个指定类型数组，返回一个指定类型数组
    @SuppressWarnings("unchecked")
    public <T> T[] toArray(T[] a) {
        if (a.length < size)
            // Make a new array of a's runtime type, but my contents:
            /*
            public static <T> T[] copyOf(T[] original, int newLength) {
        		return (T[]) copyOf(original, newLength, original.getClass());
    		}*/
            return (T[]) Arrays.copyOf(elementData, size, a.getClass());
        System.arraycopy(elementData, 0, a, 0, size);
        //若传入数组大小大于ArrayList的size则a[size]=null
        if (a.length > size)
            a[size] = null;
        return a;
    }
	//返回指定index运行时类型元素，
    @SuppressWarnings("unchecked")
    E elementData(int index) {
        return (E) elementData[index];
    }
	//返回指定index运行时类型元素，
    public E get(int index) {
    	//检查index合法性
        rangeCheck(index);
        return elementData(index);
    }
	//替换指定index位置的元素，并返回原来元素的值
    public E set(int index, E element) {
    	//检查index合法性
        rangeCheck(index);

        E oldValue = elementData(index);
        elementData[index] = element;
        return oldValue;
    }

	//添加一个元素
    public boolean add(E e) {
    	//若ArrayList容量小于size+1、1.5倍扩容
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        elementData[size++] = e;
        return true;
    }

	//指定index添加元素
    public void add(int index, E element) {
   		//判断index合法性
        rangeCheckForAdd(index);
		//确保ArrayList容量大于size+1
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        //index及以后元素后移一位
        System.arraycopy(elementData, index, elementData, index + 1,
                         size - index);
        //插入元素
        elementData[index] = element;
        //size+1
        size++;
    }

	//删除制定index元素，返回值
    public E remove(int index) {
    	//检查index合法性
        rangeCheck(index);
        modCount++;
        //取出旧值
        E oldValue = elementData(index);
        int numMoved = size - index - 1;
        //index及以后元素前移一位
        if (numMoved > 0)
            System.arraycopy(elementData, index+1, elementData, index,
                             numMoved);
        elementData[--size] = null; // clear to let GC do its work
        return oldValue;
    }

	//查找指定元素并删除
    public boolean remove(Object o) {
        if (o == null) {
            for (int index = 0; index < size; index++)
                if (elementData[index] == null) {
                    fastRemove(index);
                    return true;
                }
        } else {
            for (int index = 0; index < size; index++)
                if (o.equals(elementData[index])) {
                    fastRemove(index);
                    return true;
                }
        }
        return false;
    }

	//不判断index合法性，删除指定index元素，因为remove(Object o)中保证index合法性
    private void fastRemove(int index) {
        modCount++;
        int numMoved = size - index - 1;
        if (numMoved > 0)
            System.arraycopy(elementData, index+1, elementData, index,
                             numMoved);
        elementData[--size] = null; // clear to let GC do its work
    }
	//删除所有元素，并置null，有利于GC
    public void clear() {
        modCount++;
        // clear to let GC do its work
        for (int i = 0; i < size; i++)
            elementData[i] = null;
        size = 0;
    }
	//添加Collection类型所有元素到ArrayList
    public boolean addAll(Collection<? extends E> c) {
        Object[] a = c.toArray();
        int numNew = a.length;
        ensureCapacityInternal(size + numNew);  // Increments modCount
        System.arraycopy(a, 0, elementData, size, numNew);
        size += numNew;
        return numNew != 0;
    }
	//插入Collection类型所有元素到ArrayList指定index
    public boolean addAll(int index, Collection<? extends E> c) {
        rangeCheckForAdd(index);

        Object[] a = c.toArray();
        int numNew = a.length;
        ensureCapacityInternal(size + numNew);  // Increments modCount

        int numMoved = size - index;
        if (numMoved > 0)
            System.arraycopy(elementData, index, elementData, index + numNew,
                             numMoved);
                             
        System.arraycopy(a, 0, elementData, index, numNew);
        size += numNew;
        return numNew != 0;
    }
	//移除指定index区间的元素
    protected void removeRange(int fromIndex, int toIndex) {
        modCount++;
        int numMoved = size - toIndex;
        System.arraycopy(elementData, toIndex, elementData, fromIndex,
                         numMoved);

        // clear to let GC do its work
        int newSize = size - (toIndex-fromIndex);
        for (int i = newSize; i < size; i++) {
            elementData[i] = null;
        }
        size = newSize;
    }
	//index越界检查
    private void rangeCheck(int index) {
        if (index >= size)
            throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
    }
	//插入index越界检查
    private void rangeCheckForAdd(int index) {
        if (index > size || index < 0)
            throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
    }
	//返回index和ArrayList的size
    private String outOfBoundsMsg(int index) {
        return "Index: "+index+", Size: "+size;
    }
	//删除ArrayList中包含在c中的元素
    public boolean removeAll(Collection<?> c) {
        Objects.requireNonNull(c);
        return batchRemove(c, false);
    }
	//删除ArrayList中除包含在c中的元素，和removeAll相反
    public boolean retainAll(Collection<?> c) {
        Objects.requireNonNull(c);
        return batchRemove(c, true);
    }

    private boolean batchRemove(Collection<?> c, boolean complement) {
        final Object[] elementData = this.elementData;
        int r = 0, w = 0;
        boolean modified = false;
        try {
            for (; r < size; r++)
                if (c.contains(elementData[r]) == complement)
                    elementData[w++] = elementData[r];
        } finally {
            // Preserve behavioral compatibility with AbstractCollection,
            // even if c.contains() throws.
            if (r != size) {
                System.arraycopy(elementData, r,
                                 elementData, w,
                                 size - r);
                w += size - r;
            }
            if (w != size) {
                // clear to let GC do its work
                for (int i = w; i < size; i++)
                    elementData[i] = null;
                modCount += size - w;
                size = w;
                modified = true;
            }
        }
        return modified;
    }
	//将ArrayList的“容量，所有的元素值”都写入到输出流中
    private void writeObject(java.io.ObjectOutputStream s)
        throws java.io.IOException{
        // Write out element count, and any hidden stuff
        int expectedModCount = modCount;
        s.defaultWriteObject();

        // Write out size as capacity for behavioural compatibility with clone()
        s.writeInt(size);

        // Write out all elements in the proper order.
        for (int i=0; i<size; i++) {
            s.writeObject(elementData[i]);
        }
		//并发修改异常
        if (modCount != expectedModCount) {
            throw new ConcurrentModificationException();
        }
    }
	//先将ArrayList的“大小”读出，然后将“所有的元素值”读出
    private void readObject(java.io.ObjectInputStream s)
        throws java.io.IOException, ClassNotFoundException {
        elementData = EMPTY_ELEMENTDATA;

        // Read in size, and any hidden stuff
        s.defaultReadObject();

        // Read in capacity
        s.readInt(); // ignored

        if (size > 0) {
            // be like clone(), allocate array based upon size not capacity
            int capacity = calculateCapacity(elementData, size);
            SharedSecrets.getJavaOISAccess().checkArray(s, Object[].class, capacity);
            ensureCapacityInternal(size);

            Object[] a = elementData;
            // Read in all elements in the proper order.
            for (int i=0; i<size; i++) {
                a[i] = s.readObject();
            }
        }
    }
	
    public ListIterator<E> listIterator(int index) {
        if (index < 0 || index > size)
            throw new IndexOutOfBoundsException("Index: "+index);
        return new ListItr(index);
    }
	//返回list迭代器
    public ListIterator<E> listIterator() {
        return new ListItr(0);
    }
	//返回collection迭代器
    public Iterator<E> iterator() {
        return new Itr();
    }

    public List<E> subList(int fromIndex, int toIndex) {
        subListRangeCheck(fromIndex, toIndex, size);
        return new SubList(this, 0, fromIndex, toIndex);
    }

    static void subListRangeCheck(int fromIndex, int toIndex, int size) {
        if (fromIndex < 0)
            throw new IndexOutOfBoundsException("fromIndex = " + fromIndex);
        if (toIndex > size)
            throw new IndexOutOfBoundsException("toIndex = " + toIndex);
        if (fromIndex > toIndex)
            throw new IllegalArgumentException("fromIndex(" + fromIndex +
                                               ") > toIndex(" + toIndex + ")");
    }
```

