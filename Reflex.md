# 反射机制
`Class`类在`java.lang`包下；  
`Field`类，`Method`类，`Constructor`类等都定义在`java.lang.reflect`包下；



## 反射的概念：
- 在`JAVA`中的反射机制是指在运行状态中，对于任意一个类，都能够知道这个类 的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法；这种动态获取信息以及动态调用对象方法的功能称`JAVA`语言的反射机制；
- `JAVA`的反射机制是在编译时并不确定是哪个类被加载了，而是在程序运行的时候才加载、探知、使用在编译时并不知道的类；这样的特点就是反射；反射是指一类应用，它们能够自描述和子控制；
- `JAVA`的反射机制能够知道类的基本结构，这种对`JAVA`类结构探知的能力，我们称为`JAVA`类的“自审”；  
### JAVA反射有三个动态性质：
1.运行时生成对象实例；  
2.运行期间调用方法；  
3.运行时更改属性；    
通过这些动态性质，JAVA反射可以在程序运行时获取对象和类的真实信息；
### JAVA反射可以实现的功能：
- 在运行时判断任意一个对象所属的类；
- 在运行时构造任意一个类的对象；
- 在运行时判断任意一个类所具有的方法和属性；
- 在运行时调用任意一个对象的方法；
- 生成动态代理；

### JAVA反射应用场合:

- `JAVA`程序中许多对象在运行时都会出现两种类型：编译时类型和运行时类型；编译时的类型由声明该对象时使用的类型决定，运行时类型由实际赋给该对象的类型决定；
如：  
`Person p = new Student();`  

- 此时p的编译时类型是Person，运行时类型为Student；  
- 因为对象p是引用类型，在编译时其类型由Person来确定，而在程序运行后发现p引用的内容实际是Student，因为只有在程序运行时才能知道p引用的内容改为了Student，所以称为运行时类型；   
- 除此之外，程序在运行时还可能接收到外部传入的一个对象，该对象的编译时类型是`Object`，但程序又需要调用该对象运行时类型的方法；为了解决这些问题，程序需要在运行时发现对象和类的真实信息；然而，如果编译时根本无法预知该对象和类可能属于哪些类，程序只依靠运行时信息来发现该对象和类的真实信息，此时就必须使用反射；  

- 反射API用来生成在当前JAVA虚拟机中的类，接口或者对象的信息；  


### Class类：
- `Class`类是反射的核心类；
- 反射所有的操作都是围绕该类来生成的；
- 通过`Class`类，可以获取类的属性、方法等内容信息；
- 而`Field`类、`Method`类、`Constructor`类都定义于`Java.lang.reflect`;

##### Field类：表示类的属性，可以获取和设置类中属性的值；
##### Method类：表示类的方法，它可以用来获取类中方法的信息，或者执行方法；
##### Constrctor类：表示类的构造方法；

### 利用反射API获取类的方法和属性信息：
- 获取访问类的Class对象；
- 调用Class对象返回访问类的方法和属性信息；
```java
public class ReflcetionDemo {
//通过用户输入类的全路径，来获取该类的成员方法和成员属性；
  public Reflcetion() {
//  用户输入类的全路径；
   String classpath = JOptionPane.showInputDialog(null,"输入类全路径");
try {
// 根据类的全路径进行类加载，返回该类的class对象；
  Class cla = Class.forName(classpath);
//利用class对象cla的自审，返回方法对象集合；
 Method[] method = cla.getDeclaredMethods();
//遍历method数组，并输出方法信息；
 for(Method meth : method) {
  System.out.println(meth.toString();
 }
} catch(ClassNotFoundException e) {
 e.printStackTrace();
   }
  }
}
```

### 要使用`JAVA`反射机制，需要遵循三个步骤：
- 第一步：获得想操纵的类的`Java.lang.Class`对象；
- 第二步：调用`Class`类的诸如`get***Methods`这样的方法，用来得到对象的方法和属性等信息；
- 第三步：使用反射`API`来操作这些信息；
- 在这些步骤之前，首先当然要导入`java.lang.reflect` 这个包下要用到的类；

### 如何获得某个类的Class对象：

我们已经知道，每个类被加载后，系统就会为该类生成一个对应的`Class`对象，通过该`Class`对象就可以访问到`JAVA`虚拟机中的这个类。
#### Java程序中获得Class对象通常有如下三种方式：
- 调用某个对象的`getClass()`方法，该方法是`java.lang.Object`类中的一个方法，所以所有的`Java`对象都可以调用该方法，该方法将返回该对象所属类对应的`Class`对象。  
如：  
```java
Person p = new Person();
Class cla = p.getClass();
```
- 调用某个类的`class`属性来获取该类对应的`Class`对象，
如Person.class将会返回Person类对应的Class对象；
不过这种方式需要在编译期就知道给定类的名字；  
`Class cla = Person.class;`
- 使用Class类的`forName()`静态方法；
该方法需要传入字符串参数，该字符串参数的值是某个类的全名；
**注意：**这里必须是类的全名，即要在类名前添加完整的包名；否则会抛出一个`ClassNotFoundException`异常；
```java
Class cla = Class.forName("com.pb.jadv.reflction.Person");
```
### 后两种方式都是直接根据类来取得该类的Class对象：
#### 类名.class的两种优势：
1.代码更安全，程序在编译阶段就可以检查需要访问的Class对象是否存在，  
2.程序性能更高，因为这种方式无须调用方法，所以程序的性能更好；  
大多数情况下使用类名.class这种方式；
但如果只有一个表示类的全名的字符串，而不知道这个字符串的具体内容，此时只能使用Class类的`forName()`方法，
**注意**：该方法可能会抛出一个`ClassNotFoundException`异常；

### 访问Class对应的类所包含的构造方法：
#### 方法1：
- getConstructor方法：
```java
Constructor getConstructor(Class[] params)
```
该方法返回此Class对象所表示的类的指定的`public`构造方法，`params`参数是按声明顺序标识该参数类型的`Class`对象的一个数组；构造方法的参数类型与`params`所指定的参数类型所匹配；  
##### 示例：
```java
Constructor co = c.getConstructor(String.class,List.class);
```
(c为某Class对象）
这个方法将返回此`Class`对象所表示的类所指定的`public`构造方法；

#### 方法2：
- getConstructors()方法：
```java
Constructor[] getConstructors();
```
这个方法将返回此Class对象所表示的类的所有public构造方法；

#### 方法3：
- getDeclaredConstructor()方法：
```java
Constructor getDeclaredConstructor(Class[] params);
```
这个方法与`getConstructor()`方法非常相似，
`Declared`在英文中是公开的意思；  
加入`Declared`表示这个方法不会考虑访问级别，而`getDeclaredConstructor()`方法，将返回此Class对象所表示的类的指定构造方法，但是与构造方法的访问级别无关，而`getConstructor()`方法，将只会返回`public`构造方法；  
#### 方法4：
- getDeclaredConstructors()方法：
```java
Constructor[] getDeclaredConstructors();
```
这个方法与`getConstructors()`方法类似，而它将返回此Class对象所表示的类的所有构造方法，而不只是`public`方法，与构造方法的访问级别无关；

### 如何访问Class对应的类所包含的方法：
#### 方法1：
- getMethod方法：
```java
Method getMethod(String name,Class[] params);
```
返回此Class对象所表示的类的指定的`public`方法，name参数用于指定方法名称，`params`参数是按声明顺序标识该方法参数类型的Class对象的一个数组；
##### 示例：
```java
c.getMethod("info",String.class);
c.getMethod("info",String.class,Integer.class);
```
#### 方法2：
- getMethods()方法：
```java
Method[] getMethods();
```
`getMethods`方法将返回class对象所表示的类的所有`public`方法，而返回类型，是`Method`数组；
#### 方法3：
- getDeclaredMethod方法：
```java
Method getDeclaredMethod(String name,Class[] params);
```
返回此Class对象所表示的类的指定的方法，与方法的访问级别无关；
#### 方法4：
- getDeclaredMethods()方法：
```java
Method[] getDeclaredMethods();
```
返回此Class对象所表示的类的全部方法，与方法的访问级别无关；

### 访问Class对应的类所包含的属性：
#### 方法1：
- getField()方法：
```java
Field getField(String name);
```
返回此Class对象所表示的类的指定的`public`属性，name参数用于指定属性名称；
##### 示例：
`c.getField("age");`
#### 方法2：
- getFields方法：
`Field[] getFields();`
返回此Class对象所表示的类的所有public属性；

#### 方法3：
- getDeclaredField方法：
`Field getDeclaredField(String name);`
返回此Class对象所表示的类的指定属性，与属性的访问级别无关；

#### 方法4：
- getDeclaredFields方法：
`Field[] getDeclaredFields();`
返回此Class对象所表示的类的全部属性，与属性的访问级别无关；

### 访问Class对应的类所包含的注释：
```java
<A extends Annotation>A getAnnotation(Class<A> annotationClass)
```
试图获取该Class对象所表示类上指定类型的注释；如果该类型的注释不存在则返回null。其中`annotationClass`参数对应于注释类型的Class对象；

`Annotation[] getAnnotations();`
返回此元素桑存在的所有注释；  
`Annotation[] getDeclaredAnnotations[];`
返回直接存在于此元素上的所有注释； 


##### 访问Class对应的类所包含的内部类：
`Class[] getDeclaredClasses();`
返回该Class对象所对应类里包含的全部内部类；

##### 访问Class对应的类所在的外部类：
`Class[] getDeclaringClass();`
返回该Class对象所在的外部类；

##### 访问该Class对象所对应类所继承的父类、所实现的接口等：
`int getModifiers();`	
返回此类或接口的所有修饰符；

`getModifiers()`方法返回的修饰符由`public ,protected,private,final,static,abstract`等对应的常量组成，返回的整数应使用`Modifer`工具类的方法来解码，才可以获取真实的修饰符；  
`Class[] getInterfaces();`
返回该Class对象对应类所实现的全部接口；  
`Package getPackage();`
获取此类的包；  
`String getName();`
以字符串形式返回此Class对象所表示的类的名称；  
`String getSimpleName();`
以字符串形式返回此Class对象所表示的类的简称；  
`Class getSuperclass():`
返回该Class所表示的类的超类对应的Class对象；  

Class对象可以获得该类里的成分包括方法、构造方法及属性；其中方法由`Method`对象表示，构造方法由`Constructor`对象表示，属性由`Field`对象表示；  
`Method、Constructor、Filed`这三个类，都定义在`java.lang.reflect`包下，并实现了`java.lang.refect.Member`接口；  
程序可以通过`Method`对象来执行对应的方法，通过`Constructor`对象来调用相应的构造方法创建对象，通过`Field`对象直接访问并修改对象的属性值；


### 通过反射来生成对象有如下两种方式：
#### 使用`newInstance()`来创建对象：  
使用Class对象的`newInstance()`方法来创建Class对象对应类的实例，这种方式要求该Class对象的对应类有默认构造方法，而执行`newInstance（）`方法时实际上是利用默认构造方法来创建该类的实例；  
##### 举例：
```java
import java.util.Date;
public class Test {
 public static void main(String[] args)throws Exception {
Class cla = Date.class;
Date d = (Date)cla.newInstance();
System.out.println(d.toString());
 }
}
```
我们通过使用`Date`类的class对象的`newInstance（）`方法，创建了Date类的对象实例；此时，我们知道是要创建Date类的对象，通常在这种情况下我们不需要使用反射来创建对象，毕竟在通过反射创建对象时性能要稍微低一些 .  
实际上，只有当程序需要动态创建某个类的对象时才会考虑使用反射，通常在开发通用性比较广的框架、基础平台时可能会大量使用反射；  
#### 使用`Constructor`对象创建对象(Constructor中的newInstance方法)：
要先使用Class对象获取指定的`Constructor`对象，再调用`Constructor`对象的`newInstance（）`方法来创建该Class对象对应类的实例。通过这种方式可以选择使用某个类的指定构造方法来创建实例； 

如果我们不想利用默认构造方法来创建`JAVA`对象，而想利用指定的构造方法来创建`JAVA`对象，则需要利用`Constructor`对象了，每个`Constructor`对应一个构造方法
#### 利用指定构造方法来创建JAVA对象需要三个步骤：
- 获取该类的Class对象；
- 利用Class对象的getConstructor()方法来获取指定构造方法；
- 调用Constructor的newInstance()方法来创建JAVA对象；

##### 举例：
```java
import java.lang.reflect.Constructor;
import java.util.Date;

public class Test {
 public staic void main(String[] args) throws Exception {
//获取Date对应的Class对象
Class cla = Date.class;
//获取Date中带一个长整型参数的构造方法
//要唯一的确定某类中的构造方法，只有指定构造方法的参数列表就可以了；
Constructor cu = cla.getConstructor(long.class);
//调用Constructor的newInstance（）方法创建对象
cu是构造方法对象，cu.newInstacn()相当于调用了cla对应类的对应构造方法；
通常需要传入参数，因为调用Constructor对象的newinstance（）方法，实际上等于调用它的构造方法，传给newInstance（）方法的参数，实际将作为对应构造方法的参数；
Date d = (Date) cu.newInstance(1987);
System.out.println(d.toString());
  }
}
```
在`Method`里有一个`invoke`方法，通过`invoke()`方法来调用`Method`对象对应的方法；
#### invoke(Method类中的invoke()方法):
`Object invoke(Object obj,Object   ...args);`  
该方法中的obj是执行该方法的对象，后面的args是执行该方法时传入该方法的参数；

### 通过Class对象来调用方法：
#### 定义Person类：
```java
public class Person {
     
	private String name;
	private int age;
	private  String getName() {
		return name;
	}
	private  void setName(String name) {
		this.name = name;
	}
	
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	 public String toString() {
		 return "姓名是： " + name + ",年龄是： " + age;
	 }
}
```
#### 定义Test类：
```java
public static void main(String[] args) throws Exception {
//获取Person对应的Class对象
Class cla = Person.class;
//创建Person对象
Person p = new Person();

//得到setName方法
Method metl = cla.getMethod("setName",String.class);
//调用setName，为name赋值；
metl.invoke(p,"Jack");

//得到getName方法
Method met = cla.getMethod("getName",null);
//调用getName，获取name的值
Object o = met.invoke(p,null);
System.out.println(o);
 }
}
```
#### 调用私有方法：
`setAccessible(Boolean flag)`  
将`Method`对象的`accessible`标志设置为指示的布尔值，值为`true`则表示该`Method`在使用时应该取消Java语言访问权限检查。值为`false`则表示该`Method` 在使用时应该实施Java语言访问权限检查；


#### 如何通过Class对象来访问对应类的属性：

##### Field类用于获取类中的属性：
##### Field类提供了如下两种方法来访问属性：
```java
get***(Object obj),
set***(Object ,*** val);
```
##### 得到属性值：
`get***(Object obj);`

获取obj对象该属性的属性值，其中参数obj为该属性所在的对象。此处的`***`对应8个基本类型，如果该属性的类型是引用类型则取消`get`后面的`***`；
##### 示例：
```java
Person p = new Person();
//nameField为Field对象
nameField.get(p);
nameField.getInt(p);
```
##### 为属性赋值：
`set***(Object obj,*** val);`  
将obj对象的该属性设置成val值，此处的`***`对应8个基本类型，如果该属性的类型是引用类型，则取消`set`后面的`***`；

对获取到的私有属性调用方法`setAccessible（true）`；  
便可以使用这两个方法随意的访问指定对象的所有属性，包括`private`访问控制属性；  
`Field.setAccessible(true);`  
##### 示例：
定义一个Person类，同上；
```java
public static void main(String[] args) throws Exception {
//创建一个Person对象
Person p = new Person();
//获取Person对应的Class对象
Class cla = Person.class;

//获取Person类的name属性，使用getDeclaredField（）方法，表明可获取各种访问级别的属性；
Field nameField = cla.getDeclaredField("name");
//设置通过反射访问该Field时取消权限检查
nameField.setAccessible(true);
//调用set方法为p对象的指定Field设置值；
nameField.set(p,"Jack"）；


//获取Person类的age属性，使用getDeclaredField（）方法，表明可获取各种访问级别的属性；
Field ageField = cla.getDeclaredField("age");
//设置通过反射访问该Field时取消权限检查
ageField.setAccessible(true);
//调用setInt方法为p对象的指定Field设置值；
ageField.setInt(p,20）；
System.out.println(p);
}
}
```
事实上在实际开发中，我们没有必要使用反射，来访问已知类的方法和属性，只有当程序需要动态创建某个类的对象的时候我们才会考虑使用反射；  

在`java.lang.reflect`包下提供了一个`Array`类；
### Array:
`Array`对象可以代表所有的数组。程序可以通过使用`Array`来动态的创建数组，并且操作数组的元素。
#### Array类提供了如下几种方法：

##### 创建数组：
- `newInstance()`方法：
```java
static Object newInstance(Class componentType,int ...length)
```
创建一个具有指定的元素类型、指定维度的新数组；

##### 返回元素：
- `get***()`方法：
```java
static *** get***(Object array,int index);
```
返回`array`数组中第`index`个元素。其中`***`是各种基本数据类型，如果数组元素是引用类型，则去掉`***`，方法变为：  
`static get(Object array,int index);`

##### 为数组元素赋值：
- set方法：
```java
static void set***(Object array,int index,*** val);
```
将`array`数组中第`index`元素的值设为val。其中`***`是各种基本数据类型，如果数组元素是引用类型，则去掉`***`，方法变为：  
`static void set(Object array,int index,*** val);`
##### 示例：
```java
public static void main(String[] args) {
try {
  //创建一个元素类型为String，长度为10的数组
Object arr= Array.newInstance(String.class,10);
//依次为arr数组中index为5,6的元素赋值
Array.set(arr,5,"Jack");
Array.set(arr,6,"John");
//依次取出arr数组中index为5,6的元素的值
Object o1 = Array.get(arr,5);
Object o2 = Array.get(arr,6);
//输出arr数组中index为5,6的元素
 System.out.println(o1);
 System.out.println(o2);
}catch(Throwable e) {
 System.err.println(e);
  }
}
```
#### 使用Array类创建数组的步骤：
1.通过Array类创建多为数组；  
2.获取指定的维度；  
3.插入数据；  
4.操作动态创建出来的数组；  


## 总结：
### 反射API介绍：
Class类

Field类

Method类

Constructor类


### 获取类信息：
#### 获取Class对象的方法：
1.调用某个对象的getClass()方法；  

2.调用某个类的class属性来获取该类对应的Class对象，

3.使用Class类的forName()静态方法；


#### 获取构造方法：
```java
getConstructor()
getConstructors()
getDeclaredConstructor()
getDeclaredConstructors()
```
#### 获取属性：
```java
getField()
getFields()
getDeclaredField()
getDeclaredFields()
```
#### 获取方法：
```
getMethod()
getMethods()
getDeclaredMethod()
getDaclaredMethods()
```
首先，获取对应类的Class对象；  
利用Class类里的对应方法来获取Class对象对应类的构造方法对象，属性对象，方法对象；  
利用构造方法对象（newInstance()方法)，属性对象`（get***(Object obj),set***(Object ,*** val);）`，方法对象(invoke()方法)的各自的方法来获取Class对象对应类的构造方法，方法，属性；  
使用获取到的构造方法，方法，属性； 


使用反射创建对象

使用反射访问方法和属性

动态创建和访问数组
