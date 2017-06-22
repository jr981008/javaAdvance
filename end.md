# 总结
## 常用类java.lang包串讲：
了解java.lang包；  
##### 运用：
- 包装类；
- String和StringBuffer类； 
  
在java中，数据类型包括原始数据类型，和引用数据类型；而原始数据类型不被视为对象，意味着不能以面向对象的方式操作原始数据类型，所以在java中提供了包装类来解决原始数据类型不被作为对象的情况。   
在java中，共有8个包装类，分别对原始数据类型进行封装；      
|原始数据类型  |                   包装类|
|---|---|
|byte（字节） |                   Byte|
|char（字符）                   | Character|
|int（整型）   |                  Integer|
|long（长整型）|                  Long|
|float（浮点型）|                 Float|
|double（双精度）|                Double|
|boolean（布尔）    |             Boolean|
|short（短整型）         |        Short|

包装类的主要作用是进行原始数据类型和引用数据类型之间的装换；   
包装类另一个最主要的做法就是将字符串类型转换成原始数据类型；   
示例：   
```java
//原始数据类型与引用数据类型之间的转换；   
int i=5;
Integer objI = new Integer(i);
int j = objI.intValue();

double d = 3.5;
Double objD = new Double(d);
double e = objD.doubleValue();

//字符串类型向原始数据类型转换
String strI = "15";
int k = Integer.parseInt(strI);

String strD = "3.5";
double f = Double.parseDouble(strD);
```
String类是java当中操作字符串的类，在java当中，提供了多种方式来构造String类的对象；    

|构造方法 |                 说明|
|---|---|
|String() |   它将创建一个空字符串|
|String(String value)|  它将新建一个字符串作为指定字符串的副本；|
|String(char[] value)|它将根据字符串数组构造一个新字符串；|
|String(byte[] value)|它将通过转换指定的字节数组新建一个字符串；|

#### String类的方法：
字符串的长度：  
由length()方法确定，返回字符串中的字符数；  
语法：  
```
public int length();
```
字符串的比较：   
检查字符串是否指向同一个或不同的对象；   
用 == 运算符检查；   
检查组成字符串内容的字符；  
由 equals()方法确定；   

字符串比较运算符的用法；    
使用String类的方法，如equals()和==运算符；    
```java
String strOne = new String("字符串变量的值");
String strTwo = new String("字符串变量的值");
if(strOne == strTwo) {
  System.out.println("是同一个对象");
}else{
  System.out.println("不是同一个对象");
if(strOne.equals(strTwo)){
  System.out.println("字符串的值相同");
}else{
  System.out.println("字符串的值不相同");
}
```
##### 方法：
`boolean equalsIgnoreCase(String value)`  
此方法比较两个字符串，忽略大小写形式；   
`int compareTo(String value)`   
按字母顺序比较两个字符串。如果两个字符串相等，则返回0；如果字符串在该值之前，则返回值小于0；如果字符串在该值之后，则返回值大于0；   
`boolean startsWith(String value)`  
检查一个字符串是否以另一个字符串开始；    
`boolean endsWith(Stirng value)`
检查一个字符串是否以另一个字符串结束；   

比较不同的字符串；   
使用String类的方法，如  equalsIgnoreCase() compareTo() startsWith() endsWith()
```java
public static void main(String[] args) {
 String string1 = new String("Answer");
 String string2 = enw String("ANSWER");
 if(string1.equalsIgnoreCase(string2)){
     System.out.println("忽略大小写，字符串的内容相同");
}
if(string1.startsWith("A")){
   System.out.println("以A开始");
   }
}
```
##### 字符串的搜索：
indexOf(character)方法；   
情形1：  
返回找到的第一个匹配的位置的索引；
情形2：   
如果没有找到匹配，则返回-1；   
搜索字符串内有无指定的字符或字符串；   
使用String类的方法，如indexOf();   
```java
public static void main(String[] args) {
 String name="JohnSmith@123.com";
 System.out.println("Email ID 是："+name);
 System.out.println("@的索引是："+name.indexOf('@'));
 System.out.println(".的索引是："+name.indexOf('.'));
```
StringBuffer类是针对字符串的缓存类；   
StringBuffer类对字符串变量操作的性能高于String类；   
在字符串不经常改变时，优先使用String类；否则使用StringBuffer类；   
#### StringBuffer类的构造方法：    
|构造方法                     | 说明|
|---|---|
|public StringBuffer()|保留16个字符的空间；|
|public StringBuffer(int length)|设置缓冲器的大小；|
|public StringBuffer(Stringvalue)|接收字符串参数，用来设置初始内容，并在不重复分配的情况下保留16个字符的空间；|
##### 核心方法：
|方法 |                         说明|
|---|---|
|StringBuffer append(String s)|将制定的字符串追加到当前字符串序列中；|
|String toString()|转换为字符串形式；|
```java
public static void main(String[] args) {
 String strOne = "This is a";
 StringBuffer stringBuffer = new StringBuffer(strOne);
stringBuffer.append("StringBuffer");
String strTwo = stringBuffer.toString();
System.out.println(strTwo);
 }

```


#### 常用类java.util包串讲；
了解：  
1.了解java.util包；      
运用：    
1.使用Date、Calendar类操作日历；   
2.使用SimpleDateFormat格式化日期显示；    

#### Date类：   
Date类表示日期和时间；   
提供操纵日期和时间各组成部分的方法；   
Date类的最佳应用之一是获取系统当前时间；   

|构造方法                    |  说明|
|---|---|
|Date()|使用系统当前时间创建Date对象；|
|Date(long dt)|使用指定的时间创建Date对象，自1970年1月1日以来的指定毫秒值；|

|常用方法                     |  说明|
|--|--|
|String toString()|返回Date对象的字符串形式：|

形式：Dow mon dd hh:mm:ss ZZZ yyyy   
示例：   
```java
package util;

import java.util.Date;

public class DateTest {
 public static void main(Stirng[] args) {
   Date date = new Date();
   String dateString = date.toString();
   System.out.println(dateString);
  }
}
```
Calendar类可以根据给定的Date对象，以YEAR和MONTH等整型的形式检索信息；    
它是抽象的，因此不能像Date类一样实例化；   
|常用方法                   |   说明|
|---|---|
|Calendar getInstance()|创建一个Calendar类的实例；|
|Date getTime()|返回Calendar实例的Date形式；|
|int get(int field)|根据参数返回当前对象的部分时间；|
|void set(int field,int value)|根据参数设置当前对象的部分时间；|
|void add(int field,int value)|根据参数设置修改当前对象的部分时间；|

#### Calendar类的常量：
|static int YEAR|指示年的get和set的字段数字；|
|---|---| 
|static int MONTH|指示月份的get和set的字段数字。月份比实际月份少1；|
|static int DATE|get和set的字段数字，指示一个月中的某天；|
|static int HOUR|get和set的字段数字，指示上午或下午的小时；|
|static int MINUTE|get和set的字段数字，指示一小时中的分钟；|
|static int SECOND|get和set的字段数字，指示一分钟中的秒；|

示例：     
```java
public static void main(String[] args) {
 Calendar calendar = Calendar.getInstance();
 Date date = calendar.getTime();
 System.out.println(date);
 System.out.println(calendar.get(Calendar.YEAR));
 calendar.set(Calendar.YEAR,2000);
 System.out.println(calendar.get(Calendar.YEAR));
 calenar.add(Calendar.YEAR,10);
 System.out.println(calendar.get(Calendar.YEAR));
 }
```
#### SimpleDateFormat类：
是一个格式化和解析日期的具体类；    
它运行进行格式化（日期->文本）、解析（文本->日期）和规范化；    
它是java.text包下面的类；   

|构造方法|                          说明|
|----|---|
|SimpleDateFormat(String pattern)|用给定的模式的日期格式符号构造对象；|

|常用方法                        |  说明|
|---|---|
|String format(Date date)|将一个Date格式化为 日期/时间字符串|
|Date parse(String source) throws ParseException|从给定字符串的开始解析文本，以生成一个日期；|

日期格式符号：      
|字母                     |  日期或时间元素|
|---|---|
|y      |                    年|
|M     |                     年中的月份|
|d    |                      月份中的天数|
|H   |                       一天中的小时数（0-23）|
|m  |                       小时中的分钟数|
|s |                        分钟中的秒数|

示例：     
```java
public static void main(String[] args) {
 SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss");
String dateString = dateFormat.format(new Date());
System.out.println(dateString);
try {
 Date date = dateFormat.parse(dateString);
 System.out.println(date);
}catch(ParseException e) {
  e.printStackTrace();
 }


```
#### 集合框架与泛型串讲：
了解：   
1.了解集合框架的内容；   
2.泛型的概念；   
运用：   
1.ArrayList的使用；   
2.HashMap的使用；   
3.泛型集合的使用；   

#### Java集合框架的层次：   
* 接口                  Collection   
	* `List       Set                Map`
	
* 具体类
	* `ArrayList                 HashMap`
* 算法
	* `Collections`
提供了对集合进行排序、遍历等多种算法实现；

Java集合框架为我们提供了一套性能优良、使用方便的接口和类，它们位于java.lang包中，我们只需学会如何使用它们，就可以处理实际应用中的问题；     

List接口和Set接口继承于Collection接口；   
Collection接口存储一组不唯一，无序的对象；  
List接口存储一组不唯一，有序（插入顺序）的对象；  
Set接口存储一组唯一，无序的对象；   

Map接口存储一组键值对象，提供Key到value的映射；   

Collection接口存储一组不唯一，无序的对象；   
Collection接口用于表示任何对象或元素组。想要尽可能以常规方式处理一组元素时，就使用这一接口；  

|常用方法 |                       说明|
|---|---|
|boolean add(Object o)|将对象添加给集合；|
|boolean remove(Object o)|如果集合中有相匹配的对象，则删除对象；|
|int size()|返回当前集合中元素的数量；|
|boolean isEmpty()|判断集合中是否有任何元素；|
|boolean contains(Obejct o)|查找集合中是否含有对象；|
|void clear()|删除集合中所有元素；|

List接口存储一组不唯一，有序（插入顺序）的对象；   
List接口继承了Collection接口以定义一个允许重复项的有序集合；  
该接口不但能够对列表的一部分进行处理，还添加了面向位置的操作；  
最常用的实现类是ArrayList；   

|常用方法 |                     说明|
|--|---|
|void add(int index,Object o)|在指定的索引位置添加元素；|
|Object get(int index)|返回指定索引位置处的元素。取出的元素是Object类型，使用前需要进行强制类型转换；|
|Object remove(int index)|从列表中删除指定位置元素，起始索引位置从0开始；|

#### List接口的实现类：   
List接口的两个常用的实现类：ArrayList和LinkedList    
ArrayList实现了长度可变的数组，在内存中分配连续的空间。遍历元素和随机访问元素的效率比较高；    
LinkedList采用链表存储方式。插入、删除元素时效率比较高；   
示例：   
```java
import java.util.ArrayList;
import java.util.List;
public class ArrayListTest {
 public static void main(String[] args) {
   List list = new ArrayList();
   list.add("aaa");
   list.add("bbb");
   list.add("ccc");
 for(int i=0;i<list.size();i++) {
   String string = (String)list.get(i);
   System.out.println(string);
     }
   }
}
```
Set接口继承Collection接口；   
它不允许集合中存在重复项，每个具体的Set实现类依赖添加的对象的equals()方法来检查独一性；   
Set接口没有引入新方法，所以Set就是一个Collection；   

|常用方法                      |  说明|
|----|---|
|boolean add(Object o)|将对象添加给集合；|
|boolean remove(Object o)|如果集合中有相匹配的对象，则删除对象；|
|int size()|返回当前集合中元素的数量；|
|boolean isEmpty()|判断集合中是否有任何元素；|
|boolean contains(Obejct o)|查找集合中是否含有对象；|
|void clear()|删除集合中所有元素；|

#### Map接口：
Map接口存储一组键值对象，提供Key到value的映射；   
Map接口不是Collection接口的继承。Map接口用于维护键/值对（Key/value）。该接口描述了从不重复的键到值的映射；        

|常用方法                   |  说明| 
|----|---|
|Object put(Object key,Object val)|以“键-值对”的方式进行存储；|
|Obejct get(Object key)|根据键返回相关联的值，如果不存在指定的键，返回null;|
|Object remove(Object key)|删除由指定的键映射的“键-值对”|
|int size()|返回元素个数|
|boolean containsKey(Object key)|如果存在由指定的键映射的“键-值对”，返回true；|
|boolean isEmpty()|判断映射中是否有任何映射；|

HashMap的使用示例：   
```java
import java.util.HashMap;
import java.util.Map;
public class HashMapTest {
 public static main(String[] args) {
  
     Map map = new HashMap();
     map.put("学习委员","张三");
     map.put("班长","李四");

    String string=(String)map.get("班长");
      }
}
```

泛型是对Java语言的类型系统的一种扩展，以支持创建可以按类型进行参数化的类；    
泛型又称为参数化类型，也就是说所操作的数据类型被指定为一个参数，使代码可以应用于多种类型；   
#### 引用泛型的语法：  
```
类/接口<类型参数> 对象 = new 类<类型参数>();
```
引用泛型的示例：   
```
List<String> list = new ArrayList<String>();
```
表示当前的list集合对象只能放String类型；     


Java语言中引入泛型是一个较大的功能增强。不仅语言、类型系统和编译器有了较大的变化，以支持泛型，而且类库也进行了大翻修，所以许多重要的类，比如集合框架，都已经成为泛型化的了。这带来了很多好处：

- 类型安全: 泛型的主要目标是提高Java程序的类型安全。通过知道使用泛型定义的变量的类型限制，编译器可以在一个高得多的程度上验证类型假设；

- 消除强制类型转换: 泛型的一个附带好处是，消除源代码中的许多强制类型转换。这使得代码更加可读，并且减少了出错机会。

- 潜在的性能收益: 泛型为较大的优化带来可能。更多类型信息可用于编译器这一事实，为JVM的优化带来可能。

List泛型示例：   
```java
import java.util.ArrayList;
import java.util.List;
public class ArrayListTest {
 public static void main(String[] args) {
   List<String> list = new ArrayList<String>();
   list.add("aaa");
   list.add("bbb");
   list.add(1,"ccc");
   for(String string:list) {
          System.out.println(string);
        }
      }
    }
```
Map泛型示例：   
```java
import java.util.HashMap;
import java.util.Map;
public class HashMapTest {
 public static main(String[] args) {
  
     Map<String,String> map = new HashMap<String,String>();
     map.put("学习委员","张三");
     map.put("班长","李四");

    String string=map.get("班长");
      }
}

```
#### 输入和输出处理串讲：
了解：   
1.了解流的分类；  
2.理解流的模型和处理方式；  
运用：    
1.使用File类操作本地文件；  
2.使用文件过滤器；  
3.使用流执行输入。输出操作；   
4.实现Serializable接口实现序列化；  

### File类：
File直接管理文件，目录，File对象代表一个文件，一个目录；   
File对象主要用来获取文件本身的一些信息，不涉及对文件的读写操作；  

|构造方法 |                         说明|
|---|---|
|File(File parent,String child)|根据parent抽象路径名和child路径名字符串创建一个新File实例；|
|File(String pathname)|通过将给定路径名字符串转换为抽象路径名来创建一个新File实例；|
|File(String parent,String child)|根据parent路径名字符串和child路径名字符串创建一个新File实例；|

#### File类的方法：
|方法   |                           说明|
|----|---|
|String getName()|获取文件的名字；|
|boolean exits()|判断文件是否存在；|
|long length()|获取文件的长度（单位是字节）|
|String getAbsolutePath()|获取文件的绝对路径；|
|boolean isFile()|判断文件是否是一个普通文件，而不是目录；|
|boolean isDirectory()|判断文件是否是一个目录|
|String[] list()|用字符串形式返回目录下的全部文件；|
|File[] listFiles()|用File对象形式返回目录下的全部文件；|
|String[] list(FilenameFilter obj)|用字符串形式返回目录下的指定类型的所有文件；|
|File[] listFiles(FilenameFilter obj)|用File对象形式返回目录下的指定类型所有文件；|

在File的list方法中可以接收一个FilenameFilter参数，通过该参数可以只列出符号条件的文件；   
FilenameFilter接口里包含了一个accept(File dir,String name)方法，通过该方法依次对指定File内的所有目录、文件进行测试，如果返回true，则list方法会列出该目录或文件；   

示例：   
输出D盘下的Data文件夹中的所有以.java为后缀的文件；   
```java
public static void main(String[] args) {
  File file = new File("D://Data");
  String[] filenames = file.list(new FilenameFilter(){
  public boolean accept(File dir,String name) {
      return name.endsWith(".java");
  }
});
for(String string:filenames){
  System.out.println(string);
 }

```
#### 流：
所谓的流，是指一连串流动的字符，以先进先出的方式发送和接收数据的通道，在程序当中，所有的数据都是以流的方式进行传输或者是保存。   

按照不同的分类方式，可以将流分为不同的类型，从不同的角度来对流进行分类，它们在概念上可能存在重叠的地方；    
#### 输入流和输出流：
按照流的流向来分，可以将流分为输入流和输出流；   
- 输入流：只能从中（磁盘）读取数据（到内存），而不能向（磁盘）其写入数据；
- 输出流：只能向其（磁盘）写入数据，而不能从中（磁盘）读取数据；

Java的输入流主要由InputStream和Reader作为基类，而输出流则主要由OutputStream和Writer作为基类；   

#### 字节流和字符流：
按照操作的数据单位来分，可以分为字节流和字符流；   
- 字节流：字节流操作的最小数据单元是8位的字节；
- 字符流：字符流操作的最小数据单元是16位的字符；

Java的字节流由InputStream和OutputStream作为基类，而字符流则主要由Reader和Writer作为基类；   
- 分类    `字节输入流    字节输出流    字符输入流      字符输出流`

- 抽象基类   `InputStream   OutputStream    reader      Writer`
- 访问文件 `FileInputStream FileOutputStream  FileReader    FileWriter`
- 访问字符串                `                StringReader  StringWriter`
- 缓冲流 `BufferedInputStream  BufferedOutputStream  BufferedReader  BufferedWriter`
- 转换流     `InputStreamReader   OutputStreamWriter`
- 特殊流  `  DataInputStream  DataOutputStream`
- 对象流    `ObjectInputStream  ObjectOutputStream`

##### 转换流：
InputStreamReader和OutputStreamReader是一组字符/字节的转换流；   
简单的说，InputStreamReader就是字节流通向字符流的桥梁，它使用指定的字符集读取字节，并将它解码为字符；   
而OutputStreamWriter则是字符通向字节流的桥梁，可以使用指定的字符集将要写入流中的字符编码成为字节；   
一般的情况下，为了获得更高的操作效率，在使用当中，通常将转换类包装到缓冲类当中，以避免进行频繁的调用转换器的操作；      

示例1：   
```java
FileReader fr = new FileReader(new File("source.txt"));
BufferedReader bfr = new BufferedReader(fr);
FileWriter fw = new FileWriter(new File("target.txt"));
BufferedWriter bfw = new BufferedWriter(fw);
while(bfr.ready()){
  bfw.write(bfw.readLine()+"\n");
 }
bfw.flush();
bfw.close();
fw.close();
bfr.close();
fr.close();
```
示例2：   
```java
File file = new File("source.jpg");
DataInputStream dis = new DataInputStream(new FileInputStream(file));
DataOutputStream dos = new DataOutputStream(new FileOutputStream("target.jpg"));
byte[] bytes = new byte[1024];
int get = -1;
while((get = dis.read(bytes))!= -1){
  dos.write(bytes,0,get);
}
dos.close();
dis.close();
```
序列化示例：    
```java
public class Sample implements Serializable {
 public String s;
 public static void main(String[] args)throws IOException {
 Sample sample = new Sample();
 sample.s = "This is a entity!";
ObjectOutputStream oos = new ObjectOutputStream(fos);
oos.writeObject(sample);
oos.flush();
oos.close();
fos.close();
  }
 }
```
反序列化示例：   
```java
FileInputStream fis = new FileInputStream(new File("test.txt"));
ObjectInputStream ois = new ObjectInputStream(fis);
Sample sample = (Sample)ois.readObject();
ois.close();
fis.close();
System.out.println("sample.s="+sample.s);
```

### JUnit串讲；
理解：   
1.软件测试和单元测试；   
2.JUnit中重要的类和接口；   
3.JUnit生命周期；   
运用：   
1. 使用JUnit进行单元测试；

### 什么是软件测试：   
利用测试工具，按照测试方案和流程，对产品进行功能和性能测试，使用人工或自动手段，来进行或测试某个系统的过程；     
目的：检验是否满足规定的需求，确认预期结果和实际结果之间的差别；   

#### 软件开发生命周期：
- 项目调研；
- 需求分析；
- 软件分析；
- 程序编码；
- 软件测试；
- 运行维护；

#### 软件测试分类：
- 黑盒测试：
 功能测试、数据驱动测试；  
不考虑程序的内部结果和特征，只需知道程序输入和输出间的关系或程序功能；

- 白盒测试：
结构测试、逻辑驱动测试；   
需要对被测程序的内部逻辑非常清楚。从程序内部逻辑入手，按照一定原则设计测试用例；

- 回归测试：
程序代码修改后，重写进行测试，以确认修改没有引起新的错误等；

- 单元测试：
最低级别的测试，最小粒度的测试；   
测试程序的某个功能或代码块，一般由程序员完成；   


##### 什么是单元测试：
通常在编码阶段进行；   
对程序模块进行测试：类、方法、功能规格定义、接口定义；  
主要采用白盒测试；   
主要由开发人员实施；   

##### 单元测试的优势：
- 提高开发速度；
- 提高软件质量；
- 提升系统的可信赖度；

##### 单元测试的过程：
`计划 设计 执行  评审`

##### 单元测试的内容：
- 功能点测试：是否实现了功能，有无遗漏功能；
- 覆盖率测试：语句覆盖率和分支覆盖率，测试所有关键路径
- 模块接口测试：对通过被测模块的数据流进行测试；
- 内部数据流测试：检查数据类型说明、初始化、缺省值等；


##### 单元测试工具和框架：
```
Silk   JUnit   StrutsTestCase
JUnitEE    SpringUnit
```
### 什么是JUnit： 
开源的Java测试驱动程序框架；   
单元测试框架体系xUnit的一个分支；   

#### JUnit特性：
- 用于测试期望结果的断言（Assertion）
- 用于共享测试数据的测试工具；
- 用于方便的组织和运行测试的测试套件；
- 提供图形和文本的测试界面；


#### JUnit版本：
- JUnit3 依赖反射机制，继承TestCase类，遵循测试方法命名规范；
- JUnit4使用注解（Annotation）方式；

#### JUnit中的重要的类和接口：
- Test接口：TestCase类和TestSuite类的公共接口；
- run()：运行测试类，测试接口保存到TestResult中；

##### TestCase类：测试用例类，实现了Test接口，继承了Assert类；
setUp():完成测试开始前的初始化工作；  
runTest():进行测试；  
tearDown():完成测试结束后的扫尾工作；  

##### TestSuite类：测试套件类；
addTestSuite():将指定类的所有测试方法添加到测试组；  
addTest():将指定类的指定测试方法添加到测试组；  

##### TestResult类：
测试结果类；

##### Assert类：断言类；
assertEquals():判断期望值和实际值是否相等；  
assertNotNull():判断一个对象是否非空；  
assertNull():判断一个对象是否为空；  
assertTrue():判断条件是否为True；  
assertFalse():判断条件是否为False；  

##### TestListener接口：测试监听接口；

示例1：   
被测试类：    
```java
public class AddSub {
 public static int add(int m,int n) {
  int num = m+n;
  return num;
}
public static int sub(int m,int n) {
int num = m-n;
return num;
}
public static void main(String[] args) {
if(add(4,6) == 10) {
  System.out.println("测试成功");
}else{
   System.out.println("测试失败");
}
if(sub(6,4) == 2){
  System.out.println("测试成功");
}else{
  System.out.println("测试失败");
   }
  }
 }
```
`注：不使用JUnit，手动编写测试逻辑和提示内容；这是个典型的自定义测试类；`

JUnit3测试类：   
```java
import junit.framework.TestCase;
public class TestAddSub extends TestCase{
 public void setUp() throws Exception {
  System.out.println("初始化");
}
public void testAdd(){
 assertEquals(3,new AddSub().add(2,1));
 System.out.println("加法运算");
}
public void testSub() {
 assertEquals(1,new AddSub().sub(2,1));
 System.out.println("减法运算");
}
public void tearDown() throws Exception {
  System.out.println("测试结束");
  }
}
```
`注：使用JUnit，由框架给出断言；`


示例2：    
被测试类：    
```java
public class AddSub {
 public static int add(int m,int n) {
  int num = m+n;
   return num;
}

  public static int sub(int m,int n) {
    int num = m-n;
    return num;
   }
}
```
Junit4测试类：     
```java
import static org.junit.Assert.*;
import org.junit.*;
 @Before 
public void init() {
 System.out.println("初始化");
}
@Test
public void test1() {
 assertEquals(3,new AddSub.add(2,1));
 System.out.println("加法运算");
}
@Ignore
@Test
public void test2() {
 assertEquals(1,new AddSub().sub(2,1));
 System.out.println("减法运算");
}
@After
public void end() {
 System.out.println("测试结束");
   }
}
```
## 反射
了解：   
1.反射机制；     
2.Java反射的API;   
运用：   
1.使用反射实例化对象；  
2.使用反射执行类的方法；   

在Java运行时环境中    
对于任意一个类，能否知道这个类有哪些属性和方法？   
对于任意一个对象，能否调用它的任意一个方法？   

使用Java中的反射机制可以轻松的解决这些问题；  

这种动态获取类的信息，以及动态调用对象的方法的功能来自于Java语言的反射机制；    
#### Java反射机制主要提供了以下功能：
- 在运行时判断任意一个对象所属的类；
- 在运行时构造任意一个类的对象；
- 在运行时判断任意一个类所具有的成员变量和方法；
- 运行时调用任意一个对象的方法；

#### 在JDK中，主要由以下类来实现Java反射机制：
- Class类：代表一个类；（java.lang包中）
- Field类：代表类的成员变量（成员变量也称为类的属性）；
- Method类：代表类的方法；
- Constructor类：代表类的构造方法；
`（Field类，Method类，Constructor类在java.long.reflect包中）；`

##### 获取一个Class对象（metadata）：
1.从对象的实例获取。   
`Class c = myInfo.getClass();`
2.从子类的实例获取；   
```
TextField t = new TextFild();
Class c = t.getClass();
Class s = c.getSuperclass();
```
3.知道类名，则可以把.class加入到名字之后来获取；   
`Class c = java.awt.Button.class;`
4.如果类名在编译时是未知的，则可以使用Class.forName()方法来获取。   
`Class c = Class.forName(classString);`   
传入的字符串是类的全名；   
示例1：   
```java
Class c = Object.class;
Consturctor[] constructors = c.getConstructors();
System.out.println("所有构造器如下：");
for(Constructor constructor:constructors)
  System.out.println(constructor);
Field[] fields = c.getFields();
System.out.println("所有属性如下：");
for(Field field:fields)
 System.out.println(field);
Method[] methods = c.getMethods();
System.out.println("所方法如下：");
for(Method method:methods)
 System.out.prinln(method);
System.out.println("object类的父类是："+c.getSuperclass());
```
示例2：    
```java
try {
 List<String> list = (ArrayList<String>)
Class.forName("java.util.ArrayList").newInstance();
list.add("test");
list.add("b");
System.out.println("集合的大小："+list.size());
System.out.println("集合的内容：")；
for(String s:list) {
  System.out.println(s);
 }
}catch(InstantiationException e) {
 e.printStackTrace();
}catch(IllegalAccessException e) {
 e.printStackTrace();
}catch(ClassNotFoundException e) {
 e.printStackTrace();
 }
```
示例3：   
```java
public class ClassTest {
 public void dis() {
  System.out.println("这是dis方法");
  }

public static void main(String[] args) {
 Class c = ClassTest.class;
 try {
  Mehtod method = c.getMethod("dis");
  method.invoke(c.newInstance());
}catch(Exception e) {
  e.printStackTrace();
   }
  }
}

```
## 多线程串讲：
理解：   
1.进程和线程；    
2.多线程的创建和启动；  
3.多线程的调度；   
运用：    
1.进行线程同步；  

### 程序：
程序是一段静态的代码，它是应用程序执行的蓝本；   
#### 进程：  
进程是指一种正在运行的程序，有自己的地址空间；   
##### 进程的特点：
- 动态性；
- 并发性；
- 独立性；
#### 线程：
进程内部的一个执行单元，是程序中一个单一的顺序控制流程；  
一个进程中同时运行多个线程，完成不同的工作，称为多线程；   

##### 进程和线程的比较：
进程是系统资源分配的单位，可包括多个线程；线程是独立调度和分配的基本单位，共享进程资源；    
引入进程是为了多个程序并发执行，提供资源利用率和系统吞吐量；引入线程是为了减少程序在并发执行时付出的时空开销；   

##### 多线程的优势：
- 多线程使系统空转时间减少，提高CPU利用率；   
- 进程间不能共享内存，但线程之间共享内存非常容易；   
- 使用多线程实现多任务并发比多进程的效率高；    
- Java语言内置多线程功能支持，简化了Java的多线程编程；    

创建线程：       
继承Java.lang.Thread类，并覆盖run()方法；   
```java
class MyThread extends Thread {
 public void run() {
/*覆盖该方法*/
  }
}
```

实现Java.lang.Runnable接口，并实现run()方法；   
```java
class MyThread implements Runnable {
 public void run() {
 /*实现该方法*/
  }
}
```
启动线程：   
新建的线程不会自动开始运行，必须通过start()方法启动；   

启动继承Thread的线程：   
```java
MyThread t = new MyThread();
t.start();

```
启动实现Runnable接口的线程：    
```java
MyThread mt = new MyThread();
Thread t = new Thread(mt);
t.start();
```
继承Java.lang.Thread类：    
```java
public class ThreadDemo1 {
 public static void main(String[] args) {
  MyThread1 t = new MyThread1();
 t.start();
 while(true) {
  System.out.println("兔子领先了，别骄傲");
   }
  }
}

class MyThread1 extends Thread {
 public void run() {
  while(true) {
    System.out.println("乌龟领先了，加油");
    }
  }
}
```
注：   
优势：编写简单；  
劣势：无法继承其它父类；

实现Java.lang.Runnable接口：    
```java
public class ThreadDemo2 {
public static void main(String[] args) {
MyThread2 mt = new MyThread2();
Thread t = new Thread(mt);
t.start();
while(true) {
 System.out.println("兔子领先了，加油");
   }
  }
}

class MyThread2 implements Runnable {
 public void run() {
  while(true) {
    System.out.println("乌龟超过了，再接再厉");
     }
   }
}
```
优势:   
可继续其它类，多线程可共享同一个Thread；  
劣势：   
编程方式稍微复杂；

线程状态：   
新生：   
使用new关键字创建一个线程后，尚未调用其start方法之前；   
可运行：     
调用该线程对象的start方法之后；  
这个状态当中，线程对象可能正在运行，也可能等待运行；   
阻塞：   
一种“不可运行”的状态，在得到一个特定的事件之后会返回可运行状态；  
死亡：   
线程的run方法运行完毕或者在运行中出现未捕获的异常时。   

#### Thread类的常用方法：
|方法                          | 功能|
|----|---|
|t.setPriority(p)|改变t线程的优先级为p;|
|t.join()|阻塞当前线程，执行t线程，t线程执行完再执行当前线程；|
|Thread.sleep(m)|当前线程阻塞m毫秒，m毫秒钟后由阻塞状态转变为可运行状态；|
|Thread.yield()|当前线程停止运行，但仍处于可运行状态。可以和其他的等待执行的线程竞争处理器资源；|
|t.setDaemon(true)|将t线程设置成后台线程；|


#### sleep()和yield()对比：

|   状态| sleep()   |    yield()|
|---|---|--|
|暂停后的状态 |  进入被阻塞的状态，直到经过指定时间后，才进入可运行状态；|直接将当前转入可运行状态|
|没有其他等待运行的线程 |当前线程会等待指定的时间| 当前线程会马上恢复执行|
|等待线程的优先级别|不考虑，机会均等；|将优先级相同  或更高的线程运行|


当多个线程访问同一个数据时，容易出现线程安全问题，需要让线程同步，保证数据安全；   
让多个用户同时操作一个银行账户就可能出现线程安全问题   

#### 线程同步：   
当两个或两个以上线程访问同一个资源时，需要某种方式来确保资源在某一时刻只被一个线程使用；   

#### 线程同步的实现方案：
- 同步代码块；   
- 同步方法；    

##### 同步代码块：
语法：   
```
synchronized(obj) {
//此处代码为同步代码块
 }
```
注：obj可以是任何存在的对象；   

##### 同步方法：
语法：   
```
访问修饰符  synchronized 返回类型 方法名 {
 }
```
##### 线程同步的好处：    
解决了线程安全问题；  
##### 线程同步的缺点：  
性能下降；  
会带来死锁；   

##### 死锁：
当两个线程相互等待对方是否“锁”时就会发生死锁；   
出现死锁后，不会出现异常，不会出现提示，只是所有的线程都处于阻塞状态，无法继续；   
多线程编程时应该注意避免死锁的发生；   

##### 线程间通信的必要性：
生产者和消费者问题：  
假设仓库中只能存放一件产品，生产者将生产出来的产品放入仓库，消费者将仓库中产品取走消费；  
如果仓库中没有产品，则生产者将产品放入仓库，否则停止生产并等待，直到仓库中的产品被消费者取走为止；   
如果仓库中放有产品，则消费者可以将产品取走消费，否则停止消费并等待，直到仓库中再次放入产品为止。   

这是一个线程同步问题，生产者和消费者共享同一个资源，并且生产者和消费者之间相互依赖，互为条件；   

对于生产者，没有生产产品之前，要通知消费者等待。而生产了产品之后，有需要马上通知消费者消费；   

对于消费者，在消费之后，要通知生产者已经消费结束，需要继续生产新产品以供消费；   

在生产者消费者问题中，仅有synchronized是不够的。    
synchronized可阻止并发更新同一个共享资源，实现了同步。  
synchronized不能用来实现不同线程之间的消息传递（通信）    

Java提供了3个方法解决线程之间的通信问题；    
|方法名                  | 作用|
|---|---|
|final void wait()|表示线程一直等待，直到其他线程通知；|
|void wait(long timeout)|线程等待指定毫秒参数的时间；|
|final void wait(long timeout,int nanos)|线程等待指定毫秒、微妙的时间；|
|final void motifyAll()|唤醒同一个对象上所有调用wait()方法的线程，优先级别高的线程优先运行；|

均是java.lang.Object类的方法，都只能在同步方法或者同步代码块中使用，否则会抛出异常；




## 网络编程串讲：
了解：  
- 通信协议：TCP/IP协议、UDP协议
- 基于TCP协议的类：InetAddress
- Web相关类：URL URLConnection

运用：   
- 基于TCP协议的类：Socket、ServerSocket
- 基于UDP协议的类：DatagramSocket、DatagramPacket

IP地址;32位，由4个8位二进制数组成；   
IP表示方法：点分十进制；   
IP地址 = 网络ID + 主机ID   
网络ID：标示计算机或网络设备所在的网段；   
主机ID：标示特定主机或网络设备；   
##### IP地址包括：   
```
A类；
B类；
C类；
D类：用于组播通信；
E类：用于科研；
```
##### TCP协议和UDP协议的差别：
|  ##   |           TCP     |             UDP|
|----|---|--|
|是否连接|        面向连接          |  面向非连接|
|传输可靠性|      可靠的 |             不可靠的|
|应用场合|     传输大量的数据|         少量数据|
|速度 |           慢 |                 快|

### java.net.InetAddress类：
- InetAddress对象主要用于区分计算机网络中不同的主机，并对其进行寻址；
- InetAddress的构造函数不是公开的（public），所以需要通过它提供的静态方法来获取，有如下的方法：

|方法|解释|
|---|----|   
|InetAddress[] getAllByName(String host)|返回给定的主机名所对应的Inetaddress对象所组成的数组；|
|InetAddress getByAddress(byte[] addr)|在给定原始IP地址的情况下，返回InetAddress对象。Ip地址表现为byte数组；|      
|InetAddress getLocalHost()|返回代表本地主机的InetAddress对象|
|static InetAddress getByName(String host)|返回代表给定主机名对应的InetAddress对象；|

示例：   
```java
public class Test {
 public static void main(String[] args) throws Exception {
 InetAddress addr = InedtAddress.getbyName("www.baidu.com");
System.out.println(address);
   }
}
```
运行结果如下：  
`www.baidu.com/119.75.213.61`


### 基于TCP/IP协议的类：

Socket和ServerSocket类库位于java.net包中。  
ServerSocket用于服务器端，Socket是建立网络连接时使用的。在连接成功时，应用程序两端都会产生一个Socket实例，操作这个实例，完成所需的会话。对于一个网络连接来说，套接字是平等的，并没有差别，不因为在服务器端或在客户端而产生不同级别；

#### java.net.Socket类（用于客户端）
构造函数：   
```java
Socket(String hostName,int port)
Socket(InetAddress a,int port)
```
常用方法：
```java
InetAddress getInetAddress()
int getPort()
int getLocalPort()
InputStream geInputStream()
OutputStream getOutputStream()
void close()
```
#### java.net.ServerSocket类（用于服务器端）
构造函数：   
```java
ServerSocket()
ServerSocket(int port)
```
常用方法：
```java
Socket accept()
InetAddress getInetAddress()
int getLocalPort()
void close()
```
#### 基于UDP协议的类：
DatagramSocket类用于服务器端，用来发送和接收数据报包的套接字，DatagramPacket类用于客户端，用来封闭数据报包；

### java.net.Datagram.Socket类（用于服务器端）
构造函数:
```java
DatagramSocket()
DatagramSocket(int port)
```
常用方法：
```java
void send(DatagramPacket d)
void reveive(DatagramPacket p)
void close()
```
#### java.net.DatagramPacket类（用于客户端）
构造函数：
```java
DatagramPacket(byte[] data,int size)
DatagramPacket(byte[] date,int size,InetAddress I,int port)
```
常用方法：
```java
byte[] getData()
int getLength()
InetAddress getInetAddress()
int getPort()
```
### Web相关类：
URL表示统一资源定位器，它指向Internet上的资源文件；  
#### java.net.URL类：
构造函数：
```java
URL(String urlname)
URL(String protocol,String hostname,int port,String path)
```
常用方法：
```java
Object getContent()
URLConnection openConnection()
InputStream openStream()
String getHost()
String getPath()
Int getPort()
String getProtocol()
```

URLConnection类代表应用程序和URL之间的通信连接。此类的实例可以通过调用URL对象的openConnection()方法获得。用于读取和写入此URL引用的资源。
常用方法：
```java
URLConnection openConnection()
String getContentType()
long getLastModified()
int getContentLength()
```
示例：   
```java
public class URLConnectionExample {
  public static void main(String[] args) throws MalformedURLException,IOException {
 URL url = new URL("http://www.baidu.com");
URLConnection con = url.openConnection();
System.out.println("使用的URL是："+con.getURL().toExternalForm());
 System.out.println("内容长度是："+con.getContentLength());
   }
}
```
### XML简介：   
理解：  
- XML文档基础知识；
- DTD文档的定义和使用；
运用：  
- 编写格式良好的XML文档；
- 通过开发工具编写DTD文档；

XML(eXtensible Markup Language,可扩展标记语言）可以定义自己的一组标签；  
使人们或程序能够理解这些标签；  
##### 标记语言的层次结构：  
`SGML    HTML    XML`

- XML是用来存放数据的；
- XML不是HTML的替代品，XML和HTML是两种不同用途的语言；
- XML是被设计用来描述数据的，重点是：什么是数据，如何存放数据；
- HTML是被设计用来显示数据的，重点是：显示数据以及如何更好的显示数据；
- HTML是与显示信息相关的，XML则是与描述信息相关的。

#### 编写XML时应注意：
必须有XML声明语句；
```  
<?xml version="1.0" encoding = "gb2312"?>
```
必须有且仅有一个根元素；  
标记大小写敏感；  
属性值用引号；   
标记成对；   
空标记关闭；   
元素正确嵌套；   

如何生成DTD文的；    

#### DTD文档语法：
元素的定义；   
属性的定义；   
修饰符号；   
实体的定义；   

#### DTD作用：
定义允许或不允许什么在文档中出现；  
预先规定文档的元素结构，属性类型，实体和引用等；  
使用DTD校检XML数据的合法性   
DTD不是必需的；   

#### DTD文档类型：

##### DTD文档的声明及引用：
内部DTD文档：  
```
<!DOCTYPE 根元素[定义内容]>
```
外部DTD文档：
```
<!DOCTYPE 根元素 SYSTEM "DTD文件路径">
```
内外部DTD文档结合：
```
<!DOCTYPE 根元素 SYSTEM "DTD文件路径"[定义内容]>
```
**注意：定义关键字一定要大写，如DOCTYPE,ELEMENT,#PCDATA,且元素名称与数据类型之间也要有空格。**

#### 使用场合：
一个XML文档需要一个DTD文档时，使用内部DTD文档；  
多个XML文档需要的是同一个DTD文档时，使用外部DTD文档；  
多个XML文档需要的DTD文档有相同部分，且对某些或每个XML文档有特殊的要求时，使用内外部DTD文档；   

#### 元素的定义：
指明元素的名称和元素的类型；  
元素的类型常用的有 EMPTY  #PCDATA 纯元素类型 ANY   
##### 定义内容：  
文档中允许什么元素和不允许什么元素；    
元素出现的顺序；   
元素出现的次数；   
没有明确声明的就是禁止的；   

##### 属性的定义：
指明属性名称、属性类型、属性特点：  
属性类型：   
```
CDATA
ID
IDREF / IDREFS
Enumerated
```
属性特点：
```
#REQUIRED
#IMPLIED
FIXED value
DEFAULT value
```

