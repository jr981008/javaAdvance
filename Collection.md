# 集合框架及泛型

## 所有抽象出来的数据结构和算法统称为JAVA集合框架；
- 为什么需要集合框架？
	- 当需要容纳一定量的数据时，我们会选择数组；
	- 如果写程序时，并不知道程序运行时会需要多少对象，或者需要更复杂的方式存储对象--那么，可以使用Java集合框架，来解决这类问题；
## JAVA集合框架：
JAVA集合框架位于java.util包中，为我们提供了一套性能优良、使用方便的接口和类。JAVA集合框架是为了表示和操作集合而规定的一种统一的、标准的体系结构；  
集合框架的层次结构：  

##JAVA集合框架由三部分组成： 
- 接口：表示集合的抽象数据类型；例如：`Collection List Set Map` 等；
	* JAVA集合框架有两大类接口，`Collection`和`Map`；其中`Collection`有两个子接口，`List`和`Set`；通常在程序开发中不直接使用`Collection`而是使用`List`和`Set`；
- 实现类：集合框架中的具体的实现类；例如：`ArrayList`、`HashMap`等；

- 算法：是对实现接口的对象执行计算的方法；例如：对集合对象进行查找、排序等；提供了对集合进行排序、遍历等多种算法实现；  

##为什么在JAVA集合框架中要定义这么多的接口：
- 这是为了以不同的方式操作集合对象；  
##在JAVA集合框架中有四个常用的表示集合的接口，它们分别是：
- Collection，最基本的集合接口;一个`Collection`代表一组元素，可以存放不唯一、无序的对象；
	- Collection的子接口，`List`接口，是有序集合。存储一组不唯一、有序（插入顺序）的对象；使用`List`能够精确控制每个元素的位置；用户能够使用索引来访问`List`当中的元素，索引类似于数组当中的下标的概念；`List`接口允许存放重复的元素；
	- Collection接口的另一个子接口，`Set`，是无序集合。基本功能与`List`接口相似，区别是`Set`是一个不允许重复，且无序的集合。

- Map接口：提供关键字到值的映射，一个`Map`中不能包含相同的关键字，每个关键字只能映射到一个值；Map接口存储一组键值对象，提供key（键）到value（值）的映射；  

接口只是体现了集合框架的基本结构，开发中还要使用到具体的集合类来存储和操作对象；  
	
## 集合框架的实现类：将重点介绍List和Map接口的实现类；
- 常用的`List`接口实现类有`ArrayList`和`LinkedList`两个，它们都可以容纳`所有类型`的对象，包括null，运行重复，并且都保证元素的存储顺序；

- ArrayList对数组进行了封装，实现了长度可变的数组，和数组采用相同的存储方式，在内存中分配连续的空间，所以遍历元素和随机访问元素的效率比较高，而添加和删除元素时效率不高；比如：删除第三个元素，则要先删除第三个元素之后再将后面的元素依次前移一位；  

- LikedList采用链表存储方式，优点在于插入、删除元素时效率比较高；比如：删除第三个元素，只要将第二个元素的引用改为第四个元素就可以了；  

## ArrayList类的常用方法和使用方式：
- 对于一个集合类来说最重要的就是存储数据的`add`方法，和从集合中取出数据的`get`方法；
- 需要注意的是`add`方法的参数是`Object`类型，就是说任意类型都可以放到集合对象中，同时`get`方法的返回类型也是`Object`类型，也就是说要进行相应的类型转换；同时元素的添加是按顺序添加的；元素在集合中的位置是通过索引来确定的。初始索引位置从0开始，也就是第一个元素索引位置为0；第二个元素索引位置为1，与数组的下标概念类似；  
- 对于一个可变大小的集合对象来说，我们可以通过`size`方法，获取集合对象的元素个数；`size`方法和数组的`Length`属性概念是一样的；  

## ArrayList常用方法：
|方法名|说明|
|---|---|
|boolean| add(Object o)|
- 在列表的末尾顺序添加元素，起始索引位置从0开始;  
```java
void add(int index,Object o)
```
- 在指定的索引位置添加元素，索引位置必须介于0和列表中元素个数之间；
```java
int size()
```
- 返回列表中元素个数；
```java
Object get(int index)
```

- 返回指定索引位置处的元素。取出的元素是Object类型，使用前需要进行强制类型转换；
```java
boolean contains(Object o)
```
- 判断列表中是否存在指定元素；
```java
boolean remove(Object o)
```
- 从列表中删除元素；
```java
Object remove(int index)
```
```java
从列表中删除指定位置元素，起始位置从0开始；
```
## LinkedList的用法：
- 由于`ArrayList`类和`LinkedList`类对功能的实现方式上的不同，所以，针对的场合还是有差别的；
- ArrayList类采用了和数组相同的存储方式，在内存中分配连续的空间，所以随机访问和遍历访问元素时，它提供了更好地性能；
- LinkedList采用了链表的存储方式，每个元素之间的前后顺序是以引用的方式确定的，所以，在删除、插入对象的时候，它提供了更好的性能；  同时，也增加了一些不太一样的方法，比如：在列表的首部和列表的末尾添加元素的`addFirst`方法和`addLast`方法；获取第一个元素和最后一个元素的`getFirst`方法和`getLast`方法；删除的`removeFirst`和`removeLast`方法；

## LinedList类的使用方法：
- 有添加元素的add方法，获取元素的get方法和获取元素个数的size方法；
## LinkedList的特殊方法：
|方法名  |    说明|
|---|---|
|void addFirst(Object o)| 在列表的首部添加元素|
|void addLast(Object o)  |在列表的尾部添加元素|
|Object getFirst()       |返回列表中的第一个元素|
|Object getLast()       | 返回列表中的最后一个元素|
|Object removeFirst()  | 删除并返回列表中的第一个元素|
|Object removeLast()  |删除并返回列表中的最后一个元素|

```java
LinkedList newsTitleList = new LinkedList(); 
```

- 在声明时，应用`LinkedList`，而不是`List`，因为操作第一个元素和最后一个元素的方法都是`LinkedList`这个类独有的方法，在`List`接口中并未声明；所以在使用`LinkedList`时，前面声明必须使用`LinkedList`，而不是`List`；

## Set接口：
- Set接口描述的是一种比较简单的一种集合，集合中的对象并不按特定的方式排序，并且不能保存重复的对象；

- Set接口存储一组唯一，无序的对象；
	- `HashSet`是`Set`接口的常用实现类；而`Set`接口继承了`Collection`接口，同时没有添加新的方法，所以在使用上与`List`接口的实现类使用类使用方式一致；都有增加元素的`add`方法，所以只需要进行类的替换就可以了；  
	
`但是注意：Set接口不存在get方法，也就是说没有List接口`  

## 通过索引取值的方法；
- 没有`get`方法，`Set`集合要怎么遍历输出呢？  
	- `List`接口是使用`for`循环通过`get`方法取出每个对象的方式遍历输出整个集合的，`Set`接口虽然没有`get`方法，但是，它可以通过`JAVA`集合框架中一个叫迭代器的接口实现遍历输出；  
	
## 迭代器接口---`Iterator`接口：
- 表示对集合进行迭代的迭代器；
- `Iterator`接口中常用方法有:  
	- `hasNext`方法表示判断是否还有元素可以迭代，
	- `next`方法返回迭代的下一个元素，通过调用集合对象的`iterator`方法可以获得`Iterator对象`，通过Iterator对象就可以迭代Set集合中的内容了；
```java
Set newsTitleSet = new HashSet();
Iterator iterator = newsTitleSet.iterator();
while(iterator.hasNext()) {
  NewTitle title = (NewTitle)iterator.next();
  System.out.println(title.getTitleName());
}
  
java.util.Iterator iterator =  dogs.iterator();
 while(iterator.hasNext()){
  Dog dog = (Dog) iterator.next();
  System.out.println(dog.getName()+"\t"+dog.getStrain());

}//Iterator 是一个接口；
```

## Map接口：
- `Map`接口表示一组成对的键值映射对象，保存一个键到一个值的映射；我们通过键来操作值；
- `Map`接口中最常用的实现类就是`HashMap`类；对于`HashMap`最重要的还是存储数据和从集合中取出数据的方法；
- 不同于`List`接口的是：
	- 在`Map`接口的实现类中是使用`put`方法存储数据的，参数也不同，第一个参数是关键字，第二个参数是保存的值；
	- 在`HashMap`类中使用`get`方法，通过关键字，从集合中取值；
- `Map`接口中很多方法与`List`接口中定义的方法功能相同，如：`size、remove`方法；
- `containsKey`和`containsValue`方法与`List`接口中`contains`方法功能相似；
- `containsKey`方法判断关键字是否存在，如果存在就返回true；
## HashMap类常用方法：
|方法名|说明|
|--|-----|
|Object put(Object key,Object value)|以“键-值对”的方式进行存储|
|Object get(Object key)|根据键返回相关联的值，如果不存在指定的键，返回null|
|Object remove(Object key)|删除由指定的键映射的“键-值对”|
|int size()|返回元素个数|    
|Set keySet()|返回键的集合   | 
|Collection values()|返回值的集合|  
|boolean containsKey(Object key)|如果存在由指定的键映射的“键-值对”，返回true；|

## JAVA的集合框架由对外提供的接口，接口的实现类和对集合类操作的算法三部分组成；
- 对集合操作的算法：
- JAVA集合框架将针对不同数据结构算法的实现都保存在工具类中；
- 工具类`(Utilities类)`中包括了`Collections`类和`Arrays`类；其中`Arrays`类我们已经学习过了，它定义了用来操作数组的各种操作，在这里我们主要讲解`Collections` 类；
- `Collections`类定义了一系列用于操作集合的工具方法，这些方法都是静态方法，也就是说我们不必实例化`Collection`类就可以使用的方法；而且是泛型方法，通过泛型保证了这些算法的类型安全；  

## Collections类中的工具方法：
### 1，对集合排序、交换的方法；  
- 反转指定List集合中元素的顺序； 
`static void reverse(List list)`;
- 根据元素的自然顺序，对指定List集合按升序进行排序；  
`static void sort(List list)`  
- 在指定List集合的指定位置处交换元素；  
`static void swap(List list,int i,int j)`


### 2，对集合查找的方法；
- 使用二分查找算法查找指定List集合，以获得指定对象的索引位置；
`static int binarySearch(List list,T key)`
- 根据元素的自然顺序，返回给定集合的最大元素；
`static Object max(Collection coll)`
- 根据元素的自然顺序，返回给定集合的最小元素；
`static Object min(Collection coll)`
- 使用另一个值替换集合中出现的所有某一指定值；
`static boolean replaceAll(List list,Object oldVal,Object newVal)`
- `binarySearch`方法表示使用二分查找算法查找出指定`List`集合中的指定元素，大家都知道二分查找算法是针对已排序的集合，所以在调用`binarySearch`方法时，我们要使用`sort`对集合进行升序排序。如果没有对集合进行排序，则结果是不确定的。如果集合包含多个等于指定对象的元素，也是无法保证要到的是哪一个；  

### 接下来看max和min方法:
- `Max`方法是返回指定集合中由自然顺序决定的最大元素，这个指定的集合是不需要排序的；
- `Min`方法相反，它返回指定集合中由自然顺序决定的最小元素，同样这个集合也不要经过排序；

## 泛型就是参数化类型，就是使用参数指定操作的数据类型；

- `Collection`接口下的格式和`ArrayList`类的泛型基本相同；

## 总结：

### ArrayList类的常用方法：
- boolean add(Object o)
- int size()
- Object get(int index)

### LinkedList类的特殊方法：
- void addFirst(Object o)
- Object getFirst()
- Object removeFirst()

### Iterator接口的常用方法：
- boolean haNext()
- Object next()

### Map接口的特殊方法：
- Object put(Object key,Object value)
- Object get(Object key)
- int size()
- Set keySet()

### 泛型集合：
- Collection接口泛型集合的使用；
- Map接口泛型集合的使用；


