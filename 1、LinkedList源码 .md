### 一、LinkedList源码总结

##### 继承关系

LinkedList在java.util包下。

LinkedList继承AbstractSequentialList类。

并且实现List<E>, Deque<E>, Cloneable, java.io.Serializable接口。支持list操作，Deque双端队列操作，克隆，序列化。

##### 底层实现

> 底层是双向链表
>
>  E item;   //表示该节点包含的值
> Node<E> next; //表达当前节点的下一个节点
> Node<E> prev; //表示当前节点的上一个节点
>
> 
>
> 有一个头指针和一个尾指针
> 	//指向首节点
>     transient Node<E> first;
> 	//指向最后一个节点
>     transient Node<E> last;
>
> 
>
> 维护一个size变量记录list中节点个数
>
> // LinkedList中元素个数
>     transient int size = 0;
>
> 
>
> first、last、size
>
> 序列化时该域是不会序列化的。

##### 核心方法

```java
/*
构造方法有两个，一个时无参构造，一个是将传入集合元素构造成双向链表
*/
//构建一个空列表
public LinkedList() ;

//构建一个包含集合c的列表
public LinkedList(Collection<? extends E> c);
---------------------------------------------------------
/*
add方法调用linkLast方法，添加元素到末尾
*/
//添加元素，默认到list尾部
public boolean add(E e) ;
---------------------------------------------------------
/*
remove方法调用unLink方法，删除元素
*/
//删除元素为o的节点
public boolean remove(Object o) ;
---------------------------------------------------------
/*
addAll方法调用addAll（int，collection）方法插入元素
*/
//集合c中元素全部添加到list末尾
public boolean addAll(Collection<? extends E> c) ;

//从指定的位置index开始，将集合c中的元素插入到列表中
public boolean addAll(int index, Collection<? extends E> c) ;
---------------------------------------------------------
/*
get方法会有调用一个node(int index)方法，判断index与size/2之间关系
若index<size/2，则从first开始向后查找
否则从last开始向前查找
*/
//获得index位置的元素
public E get(int index) ;
```



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
	//构建一个空列表
    public LinkedList() ;

	//构建一个包含集合c的列表
    public LinkedList(Collection<? extends E> c);

	//将节点值为e的作为首节点（头插法）
    private void linkFirst(E e);

	//将节点值为e的作为尾节点（尾插法）
    void linkLast(E e) ;

	//在非空节点前插入一个值为e的节点
    void linkBefore(E e, Node<E> succ) ;

	//释放非空节点first
    private E unlinkFirst(Node<E> f);

    //释放非空节点last
    private E unlinkLast(Node<E> l);

	//删除非空节点
    E unlink(Node<E> x) ;

	//获得链表第一个节点
    public E getFirst() ;

	//获得链表最后一个节点
    public E getLast() ;

	//删除第一个节点
    public E removeFirst() ;

	//删除最后一个节点
    public E removeLast() ;

	//添加一个节点到头部
    public void addFirst(E e) ;

	//添加一个节点到尾部
    public void addLast(E e) ;

	//查询list中是否有元素o，有返回索引，否则返回-1（从前到后）
    public boolean contains(Object o);

	//返回list中节点个数
    public int size() ;

	//添加元素，默认到list尾部
    public boolean add(E e) ;

	//删除元素为o的节点
    public boolean remove(Object o) ;

	//集合c中元素全部添加到list末尾
    public boolean addAll(Collection<? extends E> c) ;

	//从指定的位置index开始，将集合c中的元素插入到列表中
    public boolean addAll(int index, Collection<? extends E> c) ;

	//删除全部节点
    public void clear() ;

	//获得index位置的元素
    public E get(int index) ;

	//设置指定index位置元素为element，并返回旧值
    public E set(int index, E element);

	//添加元素到指定位置
    public void add(int index, E element) ;

	//移除指定index的元素，并返回值
    public E remove(int index) ;

	//判断index的是元素索引合法性
    private boolean isElementIndex(int index) ;

	//判断index的是插入位置合法性
    private boolean isPositionIndex(int index) ;

	//构建 IndexOutOfBoundsException详细信息
    private String outOfBoundsMsg(int index) ;

	//判断元素索引合法性
    private void checkElementIndex(int index) ;

	//判断插入位置的合法性
    private void checkPositionIndex(int index) ;

	//查询指定index的节点，若index<size/2从first开始向后找
	//否则从last向前找
    Node<E> node(int index) ;

	//返回列表中第一次出现o的位置，若不存在则返回-1
    public int indexOf(Object o) ;

 //逆向搜索，返回第一出现o的位置，不存在则返回-1
    public int lastIndexOf(Object o) ;

//获取列表首节点元素值
    public E peek() ;

//获取列表首节点元素值，若为空则抛异常
    public E element();

//检索首节点，若空则返回null,不为空则返回其元素值并删除首节点
    public E poll() ;

//检索首节点，若空则抛异常,不为空则返回其元素值并删除首节点
    public E remove();

//在列表尾部增加节点e
    public boolean offer(E e);

 //在列表首部插入节点e
    public boolean offerFirst(E e) ;

  //在列表尾部插入节点e
    public boolean offerLast(E e) ;

//获取列表首节点元素值
    public E peekFirst();

//获取列表尾节点元素值
    public E peekLast() ;

//检索首节点，若空则返回null,不为空则返回其元素值并删除首节点
    public E pollFirst() ;

//检索尾节点，若空则返回null,不为空则返回其元素值并删除尾节点
    public E pollLast() ;

//入栈
    public void push(E e);

//出栈
    public E pop() ;

//删除列表中第一出现o的节点
    public boolean removeFirstOccurrence(Object o);

//逆向搜索，删除第一次出现o的节点
    public boolean removeLastOccurrence(Object o) ;


//返回ListIterator
    public ListIterator<E> listIterator(int index) ;

    //浅拷贝
    public Object clone() ;

//返回list中所有元素的数组
    public Object[] toArray() ;

    @SuppressWarnings("unchecked")
    public <T> T[] toArray(T[] a) ;

    private static final long serialVersionUID = 876323262645176354L;

    private void writeObject(java.io.ObjectOutputStream s);


    @SuppressWarnings("unchecked")
    private void readObject(java.io.ObjectInputStream s);


    @Override
    public Spliterator<E> spliterator() {
        return new LLSpliterator<E>(this, -1, 0);
    }

```



### 二、LinkedList源码注释版

```java

package java.util;

import java.util.function.Consumer;

public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable
{
	//实现Serilizable接口时，将不需要序列化的属性前添加关键字transient，序列化对象的时候，这个属性就不会序列化到指定的目的地中。
	// LinkedList中元素个数
    transient int size = 0;
	//指向首节点
    transient Node<E> first;
	//指向最后一个节点
    transient Node<E> last;
    
     private static class Node<E> {
        E item;   //表示该节点包含的值
        Node<E> next; //表达当前节点的下一个节点
        Node<E> prev; //表示当前节点的上一个节点

        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
    }
    
	//构建一个空列表
    public LinkedList() {
    }
	//构建一个包含集合c的列表
    public LinkedList(Collection<? extends E> c) {
        this();
        addAll(c);
    }

	//将节点值为e的作为首节点（头插法）
    private void linkFirst(E e) {
    	//保存first节点地址
        final Node<E> f = first;
        //newNode的pre为null，值为e，next为first
        final Node<E> newNode = new Node<>(null, e, f);
        //将newNode设为first
        first = newNode;
        //若原来first为空。则设置last为newNode
        if (f == null)
            last = newNode;
        //若原来first为不为空，则设置原来first的pre为newNode
        else
            f.prev = newNode;
        //链表节点个数加一
        size++;
        modCount++;
    }

	//将节点值为e的作为尾节点（尾插法）
    void linkLast(E e) {
    	//保存last节点地址
        final Node<E> l = last;
        //新建一个节点newNode，pre为last，值为e，next为null
        final Node<E> newNode = new Node<>(l, e, null);
        //将newNode设置为last节点
        last = newNode;
        //如果原来last为空，现在节点为last同时也是first
        if (l == null)
            first = newNode;
        //否则现在newNode为原来last的next节点
        else
            l.next = newNode;
        //链表节点个数加一
        size++;
        modCount++;
    }

	//在非空节点前插入一个值为e的节点
    void linkBefore(E e, Node<E> succ) {
        // assert succ != null;
        //保存非空节点pred
        final Node<E> pred = succ.prev;
        //新建一个值为e，pre为非空节点pred，next为非空节点的新节点
        final Node<E> newNode = new Node<>(pred, e, succ);
        //设置非空节点前驱为新节点
        succ.prev = newNode;
        //非空节点pred为空，则新节点为first
        if (pred == null)
            first = newNode;
        //非空节点pred不为空，则新节点为pred的next
        else
            pred.next = newNode;
        //链表节点数加一
        size++;
        modCount++;
    }

	//释放非空节点first
    private E unlinkFirst(Node<E> f) {
        // assert f == first && f != null;
        final E element = f.item;
        final Node<E> next = f.next;
        //释放first节点
        f.item = null;
        f.next = null; // help GC
        //first的next设置为first节点
        first = next;
        if (next == null)
            last = null;
        else//next前驱清空
            next.prev = null;
        size--;
        modCount++;
        return element;
    }

	//释放非空节点last
    private E unlinkLast(Node<E> l) {
        // assert l == last && l != null;
        //保存last节点值和pre
        final E element = l.item;
        final Node<E> prev = l.prev;
        //释放last节点
        l.item = null;
        l.prev = null; // help GC
        //设置last节点为原来last前驱
        last = prev;
        //原来last的pre为空，则first设置为空
        if (prev == null)
            first = null;
        else//原来last的pre不为空，则pre的next设置为空
            prev.next = null;
        size--;
        modCount++;
        return element;
    }

	//删除非空节点
    E unlink(Node<E> x) {
        // assert x != null;
        //保存非空节点值、pre、next
        final E element = x.item;
        final Node<E> next = x.next;
        final Node<E> prev = x.prev;
		//pre为空则设置first为空
		//pre不为空则设置pre.next为非空节点值的next，并将非空节点值的pre设置为空
        if (prev == null) {
            first = next;
        } else {
            prev.next = next;
            x.prev = null;
        }
		//next为空则设置last为x.prev
        if (next == null) {
            last = prev;
        } else {
            next.prev = prev;
            x.next = null;
        }

        x.item = null;//help gc
        size--;
        modCount++;
        return element;
    }

	//获得链表第一个节点
    public E getFirst() {
        final Node<E> f = first;
        if (f == null)
            throw new NoSuchElementException();
        return f.item;
    }

	//获得链表最后一个节点
    public E getLast() {
        final Node<E> l = last;
        if (l == null)
            throw new NoSuchElementException();
        return l.item;
    }

	//删除第一个节点
    public E removeFirst() {
        final Node<E> f = first;
        if (f == null)
            throw new NoSuchElementException();
        return unlinkFirst(f);
    }
	//删除最后一个节点
    public E removeLast() {
        final Node<E> l = last;
        if (l == null)
            throw new NoSuchElementException();
        return unlinkLast(l);
    }

	//添加一个节点到头部
    public void addFirst(E e) {
        linkFirst(e);
    }
	//添加一个节点到尾部
    public void addLast(E e) {
        linkLast(e);
    }
	//查询list中是否有元素o，有返回索引，否则返回-1（从前到后）
    public boolean contains(Object o) {
        return indexOf(o) != -1;
    }
	//返回list中节点个数
    public int size() {
        return size;
    }
	//添加元素，默认到list尾部
    public boolean add(E e) {
        linkLast(e);
        return true;
    }
	//删除元素为o的节点
    public boolean remove(Object o) {
        if (o == null) {
            for (Node<E> x = first; x != null; x = x.next) {
                if (x.item == null) {
                    unlink(x);
                    return true;
                }
            }
        } else {
            for (Node<E> x = first; x != null; x = x.next) {
                if (o.equals(x.item)) {
                    unlink(x);
                    return true;
                }
            }
        }
        return false;
    }
	//集合c中元素全部添加到list末尾
    public boolean addAll(Collection<? extends E> c) {
        return addAll(size, c);
    }
	//从指定的位置index开始，将集合c中的元素插入到列表中
    public boolean addAll(int index, Collection<? extends E> c) {
    //首先判断插入位置的合法性
        checkPositionIndex(index);

        Object[] a = c.toArray();
        int numNew = a.length;
        if (numNew == 0)//集合c的size为0，则返回false
            return false;

        Node<E> pred, succ;
        if (index == size) {//说明在列表尾部插入集合元素
            succ = null;
            pred = last;
        } else {//否则，找到index所在的节点
            succ = node(index);
            pred = succ.prev;
        }

		//从index位置插入集合c中元素
        for (Object o : a) {
            @SuppressWarnings("unchecked") E e = (E) o;
            Node<E> newNode = new Node<>(pred, e, null);
            if (pred == null)
                first = newNode;
            else
                pred.next = newNode;
            pred = newNode;
        }

		//若index位置为空，则设置插入后最后一个元素为last
        if (succ == null) {
            last = pred;
        } else {//否则将index位置节点连接在插入后最后一个元素之后
            pred.next = succ;
            succ.prev = pred;
        }

        size += numNew;
        modCount++;
        return true;
    }
	//删除全部节点
    public void clear() {
        
        for (Node<E> x = first; x != null; ) {
            Node<E> next = x.next;
            x.item = null;
            x.next = null;
            x.prev = null;
            x = next;
        }
        first = last = null;
        size = 0;
        modCount++;
    }

	//获得index位置的元素
    public E get(int index) {
        checkElementIndex(index);
        return node(index).item;
    }

	//设置指定index位置元素为element，并返回旧值
    public E set(int index, E element) {
        checkElementIndex(index);
        Node<E> x = node(index);
        E oldVal = x.item;
        x.item = element;
        return oldVal;
    }

	//添加元素到指定位置
    public void add(int index, E element) {
        checkPositionIndex(index);

        if (index == size)
            linkLast(element);
        else
            linkBefore(element, node(index));
    }
	//移除指定index的元素，并返回值
    public E remove(int index) {
        checkElementIndex(index);
        return unlink(node(index));
    }
	//判断index的是元素索引合法性
    private boolean isElementIndex(int index) {
        return index >= 0 && index < size;
    }
	//判断index的是插入位置合法性
    private boolean isPositionIndex(int index) {
        return index >= 0 && index <= size;
    }
	//构建 IndexOutOfBoundsException详细信息
    private String outOfBoundsMsg(int index) {
        return "Index: "+index+", Size: "+size;
    }
	//判断元素索引合法性
    private void checkElementIndex(int index) {
        if (!isElementIndex(index))
            throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
    }
	//判断插入位置的合法性
    private void checkPositionIndex(int index) {
        if (!isPositionIndex(index))
            throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
    }

	//查询指定index的节点，若index<size/2从first开始向后找
	//否则从last向前找
    Node<E> node(int index) {
        // assert isElementIndex(index);

        if (index < (size >> 1)) {
            Node<E> x = first;
            for (int i = 0; i < index; i++)
                x = x.next;
            return x;
        } else {
            Node<E> x = last;
            for (int i = size - 1; i > index; i--)
                x = x.prev;
            return x;
        }
    }
	//返回列表中第一次出现o的位置，若不存在则返回-1
    public int indexOf(Object o) {
        int index = 0;
        if (o == null) {
            for (Node<E> x = first; x != null; x = x.next) {
                if (x.item == null)
                    return index;
                index++;
            }
        } else {
            for (Node<E> x = first; x != null; x = x.next) {
                if (o.equals(x.item))
                    return index;
                index++;
            }
        }
        return -1;
    }

 //逆向搜索，返回第一出现o的位置，不存在则返回-1
    public int lastIndexOf(Object o) {
        int index = size;
        if (o == null) {
            for (Node<E> x = last; x != null; x = x.prev) {
                index--;
                if (x.item == null)
                    return index;
            }
        } else {
            for (Node<E> x = last; x != null; x = x.prev) {
                index--;
                if (o.equals(x.item))
                    return index;
            }
        }
        return -1;
    }

//获取列表首节点元素值
    public E peek() {
        final Node<E> f = first;
        return (f == null) ? null : f.item;
    }

//获取列表首节点元素值，若为空则抛异常
    public E element() {
        return getFirst();
    }

//检索首节点，若空则返回null,不为空则返回其元素值并删除首节点
    public E poll() {
        final Node<E> f = first;
        return (f == null) ? null : unlinkFirst(f);
    }
//检索首节点，若空则抛异常,不为空则返回其元素值并删除首节点
    public E remove() {
        return removeFirst();
    }
//在列表尾部增加节点e
    public boolean offer(E e) {
        return add(e);
    }
 //在列表首部插入节点e
    public boolean offerFirst(E e) {
        addFirst(e);
        return true;
    }
  //在列表尾部插入节点e
    public boolean offerLast(E e) {
        addLast(e);
        return true;
    }
//获取列表首节点元素值
    public E peekFirst() {
        final Node<E> f = first;
        return (f == null) ? null : f.item;
     }
//获取列表尾节点元素值
    public E peekLast() {
        final Node<E> l = last;
        return (l == null) ? null : l.item;
    }
//检索首节点，若空则返回null,不为空则返回其元素值并删除首节点
    public E pollFirst() {
        final Node<E> f = first;
        return (f == null) ? null : unlinkFirst(f);
    }
//检索尾节点，若空则返回null,不为空则返回其元素值并删除尾节点
    public E pollLast() {
        final Node<E> l = last;
        return (l == null) ? null : unlinkLast(l);
    }
//入栈
    public void push(E e) {
        addFirst(e);
    }
//出栈
    public E pop() {
        return removeFirst();
    }
//删除列表中第一出现o的节点
    public boolean removeFirstOccurrence(Object o) {
        return remove(o);
    }
//逆向搜索，删除第一次出现o的节点
    public boolean removeLastOccurrence(Object o) {
        if (o == null) {
            for (Node<E> x = last; x != null; x = x.prev) {
                if (x.item == null) {
                    unlink(x);
                    return true;
                }
            }
        } else {
            for (Node<E> x = last; x != null; x = x.prev) {
                if (o.equals(x.item)) {
                    unlink(x);
                    return true;
                }
            }
        }
        return false;
    }

//返回ListIterator
    public ListIterator<E> listIterator(int index) {
        checkPositionIndex(index);
        return new ListItr(index);
    }

    //浅拷贝
    public Object clone() {
        LinkedList<E> clone = superClone();

        // Put clone into "virgin" state
        clone.first = clone.last = null;
        clone.size = 0;
        clone.modCount = 0;

        // Initialize clone with our elements
        for (Node<E> x = first; x != null; x = x.next)
            clone.add(x.item);

        return clone;
    }

//返回list中所有元素的数组
    public Object[] toArray() {
        Object[] result = new Object[size];
        int i = 0;
        for (Node<E> x = first; x != null; x = x.next)
            result[i++] = x.item;
        return result;
    }

    @SuppressWarnings("unchecked")
    public <T> T[] toArray(T[] a) {
        if (a.length < size)
            a = (T[])java.lang.reflect.Array.newInstance(
                                a.getClass().getComponentType(), size);
        int i = 0;
        Object[] result = a;
        for (Node<E> x = first; x != null; x = x.next)
            result[i++] = x.item;

        if (a.length > size)
            a[size] = null;

        return a;
    }

    private static final long serialVersionUID = 876323262645176354L;


    private void writeObject(java.io.ObjectOutputStream s)
        throws java.io.IOException {
        // Write out any hidden serialization magic
        s.defaultWriteObject();

        // Write out size
        s.writeInt(size);

        // Write out all elements in the proper order.
        for (Node<E> x = first; x != null; x = x.next)
            s.writeObject(x.item);
    }


    @SuppressWarnings("unchecked")
    private void readObject(java.io.ObjectInputStream s)
        throws java.io.IOException, ClassNotFoundException {
        // Read in any hidden serialization magic
        s.defaultReadObject();

        // Read in size
        int size = s.readInt();

        // Read in all elements in the proper order.
        for (int i = 0; i < size; i++)
            linkLast((E)s.readObject());
    }


    @Override
    public Spliterator<E> spliterator() {
        return new LLSpliterator<E>(this, -1, 0);
    }

   
```

