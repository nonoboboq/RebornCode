# 一、ArrayList  
## 1.基本用法
```
        ArrayList a1 = new ArrayList(10);//指定大小
        a1.add(10);
        System.out.println(a1);
        ArrayList<String> a2 = new ArrayList<String>();//默认大小
        a2.add("abc");
        a2.add("qwe");
        a2.add("iop");
        System.out.println(a2);
        //迭代器访问
        Iterator<String> it = a2.iterator();
        while (it.hasNext()){
            String str = it.next();
            System.out.println(str);
        }
        //通过索引访问
        for(int i=0;i<a2.size();i++){
            System.out.println(a2.get(i));
        }
        //判断是否含有某个对象
        if (a2.contains("abc")){
            System.out.println("Yes!");
        }

```
## 2.分析
### add()
```
    public boolean add(E e) {
        modCount++;
        add(e, elementData, size);
        return true;
    }

    private void add(E e, Object[] elementData, int s) {
        if (s == elementData.length)//到达数组的最大长度，扩张
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

    //ArrayList初始容量为oldcapacity = 0，在add()第一个对象后，其容量变为DEFAULT_CAPACITY = 10。后续按照1.5倍增加扩大容量
    private int newCapacity(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + (oldCapacity >> 1);//1.5倍扩张
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


# 二、Vector

## 1.基本用法
```
        Vector<Integer> v1 = new Vector<Integer>();
        Vector<Integer> v2 = new Vector<Integer>(10);//指定大小
        Vector<Integer> v3 = new Vector<Integer>(10,2);//指定大小和增长因子

```
构造方法多了一个增长因子的设置

## 2.分析
```
    //相对于ArrayList多了一个modCount参数，用于记录集合类对象被修改的次数
    同时多了Vector方法中多了synchronized 保证是线程安全的
    public synchronized boolean add(E e) {
        modCount++;
        add(e, elementData, elementCount);
        return true;
    }

    //每次扩充容量增加int newCapacity = oldCapacity + ((capacityIncrement > 0) ?
                                         capacityIncrement : oldCapacity);
    若不指定capacityIncrement，每次以2倍方式增加。若是指定capacityIncrement，则在原有基础上“+”capacityIncrement增加
    private int newCapacity(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + ((capacityIncrement > 0) ?
                                         capacityIncrement : oldCapacity);
        if (newCapacity - minCapacity <= 0) {
            if (minCapacity < 0) // overflow
                throw new OutOfMemoryError();
            return minCapacity;
        }
        return (newCapacity - MAX_ARRAY_SIZE <= 0)
            ? newCapacity
            : hugeCapacity(minCapacity);
    }



    //在iterator方法中：modCount被赋予了 expectedModCount，在多线程或是单线程迭代该对象时，会对进行判断当前对象是否被其他线程改变掉过
    private class Itr implements Iterator<E> {
        int cursor;       // index of next element to return
        int lastRet = -1; // index of last element returned; -1 if no such
        int expectedModCount = modCount;
        ...

        public E next() {
            synchronized (Vector.this) {
                checkForComodification();//判断一下modCount是否发生了变化
                int i = cursor;
                if (i >= elementCount)
                    throw new NoSuchElementException();
                cursor = i + 1;
                return elementData(lastRet = i);
            }
        }

        final void checkForComodification() {
            if (modCount != expectedModCount)
                throw new ConcurrentModificationException();
        }

    }

```
# 三、hashmap
