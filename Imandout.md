# 输入和输出处理
## 什么是文件：
- 相关记录或放在一起的数据的集合；
- 在电脑中一个一个带有后缀名的文件；
## 文件的存放：
- 硬盘、U盘、光盘等等一系列的磁盘都可以用来存放文件数据；
### 在JAVA中，用来访问文件属性的类为java.io.File;
- JAVA的File类提供定位本地文件系统，描述文件和目录的一个功能。
- File类对象即可以表示文件，也可以表示一个目录。
- 也就是说，在程序中一个File对象，它可以用来代表一个文件也可以用来代表一个目录；
- 利用File对象可用来对文件或目录及其属性进行基本操作，
- File对象可以查出与文件相关的信息，如文件名称、文件最后修改日期、文件大小等等；还可以利用File对象来创建一些文件，删除文件等等；
### File类的构造方法：
|方法 |    说明|
|---|----|
|File(String pathname)|接收文件名作为字符串|

创建一个指向该文件的文件对象；如：  
```java
File f1 = new File("C:\\hello.txt");
File(String dir,String subpath)
```
dir参数指定目录路径，subpath参数指定文件名    如：  
```java
File f2 = new File("c:\\myDoc","temp.txt")`;
```
第一个参数是C盘的mayDoc文件夹，第二个参数是temp.txt文本文件；
```java
File(File parent,String subpath)
```
parent参数指定目录路径，subpath参数指定文件名； 
第一个参数用来指定根目录，第二个参数用来指定子目录或者文件；  
 如果程序只处理一个文件，那么使用第一种构造方法比较合适，  
 如果程序处理的是一个公共目录当中的若干子目录或文件，  
那么后两种方法比较合适；
File对象是java.io包当中引用磁盘文件的唯一对象，  
File类仅仅用来描述File对象的属性，它并不说明数据是如何存储的；  
File类旨在提供抽象化，以独立于机器的方式处理文件或者是路径名；  
### File类常用方法：
```java
boolean canRead()
boolean canWrite()
boolean equals(Object obj)
boolean exits()
String getAbsolutePath()
String getName()
String getParent()
boolean isAbsolute()
boolean isDirectory()
boolean isFile()
```
### File类的使用，获取文件属性信息：
在C盘根目录下有一个文件夹`myDoc，myDoc`当中存在文本文件`hello.txt`;
```java
File f = new File("c:\\myDoc","hello.txt");
System.out.println("文件名： " +f.getName());
System.out.println("路径： " +f.getPath());
System.out.println("绝对路径： " + f.getAbsolutePath());
System.out.println(f.exists() ? "文件存在" : "文件不存在");
System.out.println(f.isDirectory()　？　＂文件是目录＂　：　＂文件不是目录＂）；
System.out.println(f.isFile() ? "文件是普通文件" : "文可能是命名管道");
if(f.canRead) {
  System.out.println("可以读取此文件");
 } else {
  System.out.println("不能读取此文件");
}
if(f.canWriter()) {
  System.out.println("可以写入到此文件");
}else  {
  System.out.println("不能写入此文件");
}
```
File类不但可以用来查看文件或者是目录的属性信息，还可以用来创建或者删除文件和目录；  
|方法  |         说明|
|---|---|
|boolean delete()|删除此对象指定的文件|
|boolean createNewFile()|创建空文件|
|boolean isDirectory() |测试此File对象表示的文件是否是目录|
|boolean mkdir()|创建由该File对象表示的目录|
|boolean mkdirs()|创建包括父目录的目录|
```java
public void create(File file) {
  if(!file.exists()) {
  file.createNewFile();
   }
}

public void delete(File file) {
 if(file.exists()) {
  file.delete();
 }
}

FileMethods fm = new FileMethods();
//fm是类对象；
   File f1 = new File("c:\\myDoc\\test.txt");
   File f2 = new File("c:\\myDoc","hello.txt");
fm.create(f1);
fm.delete(f2);
```
File类不能访问文件的内容，即不能从文件中读取数据或者是往文件里写数据；  
#### 如何操作文件的内容，如何读取和写入文件；
- 读文件，是指把文件当中的数据读取到内存中来；
- 写文件就是把内存中的数据写到文件中去；
#### 通过什么去读写文件呢？ 答案是文件流；
- 流，stream，是指一连串流动的字符，以先进先出的方式发送或者接受数据的通道；
- 一个流是一个输入设备或者是输出设备的抽象表示；
- 可以写输入到流中，也可以从流中读数据；
- 可以把流想象为程序中流进或流出的一个字节序列；
#### 流特性：
- 流具有明确的方向性，当你向一个流写入数据时，这个流称为输出流，输出流可以将信息送往程序的外部；例如，硬盘上的文件、打印机上的文件等等；   
- 可以从一个输出流读取数据，原则上这些数据可以是任何串行的数据源；如磁盘文件，键盘或远程的计算机等；  
#### 流特性特点：
- 先进先出的方式传递信息；
- 一个字节序列；
- 具有方向性：输入流、输出流； 
```
在java的io包当中，封装了许多输入输出流的API.  
在程序当中，这些输入输出流的类的对象称为流对象；  
可以通过这些流对象将内存中的数据以流的方式写入文件。  
也可以通过流对象将文件中的数据以流的方式读取到内存；  
流对象构造的时候往往和数据源（比如文件）会联系起来；   
数据源分为源数据源和目标数据源；输入流联系的是源数据源；程序通过输入流读取文件中的信息；这时文件就称之为源数据源；输入流到达文件读取信息的时候称为输入流；  
输出流联系的则是目标数据源；程序通过输出流向目标数据源当中写入数据；  
程序向一个流当中写入数据。这个流是输出流； 
``` 
### 数据流的划分：
#### 按照流向划分：
- 输入流：只能从中读取信息，而不能向其中写入信息；
- 输出流：只能向其中写入数据，而不能从中读取数据；
- 所谓的按照方向主要都是按照程序的角度来进行观看的；
- 例如：数据从内存到硬盘，称为输出流；

##### 流的基类：
- JAVA的输出流主要由`OutputStream`和`Writer`作为基类，
- 而输入流则主要由`InputStream`和`Reader`作为基类；

#### 按照操作的数据单位的不同来划分：
- 字节流：字节流操作的最小数据单位为8位的字节，
- 字符流：而字符流操作的最小数据单元是16位的字符；
##### 字节流和字符流的区分：
一般情况下字节流建议用于二进制数据、而字符流用于文本；它们的用法几乎是完全一样的；
##### 流的基类：
#### 按照处理数据单元划分：
##### 字节流：
- 字节输入流`InputStream`基类；
- 字节输出流`OutputStream`基类；
##### 字符流：
- 字符输入流`Reader`作为基类；
- 字符输出流`Writer`作为基类；  
这四个基类都是抽象类，抽象类不能创建实例，所以这四个基类只用来实现更具体的输入或输出功能子类的基类；  
它们都定义了一组方法，这些方法来定义它们代表的流的操作的一个基本集；
一个被访问的流的基本特征都是通过实现这4个抽象类的方法来建立的；

#### InputStream：
字节输入流`InputStream`是所有输入流的基类，它是抽象类，本身不能创建实例来执行输入，所有的字节输入流都是`InputStream`类的直接或间接子类；  
#### InputStream提供的和读取数据有关的方法：
```java
int read()
int read(byte[] b)
int read(byte[] b,int off,int len)
void close()
int available()
skip(long n)
mark(int readlimit)
void result()
```
#### read方法：
在从文件或键盘读数据时，采用后两者方法可以减少读物理文件或键盘的时间，提高io操作效率；

#### OutputStream :
字节输出流`OutputStream`也是一个抽象类，它用来作为所有表示字节输出流的其他类的基类，也就是说所有的字节输出流都是`OutputStream`类的直接或间接子类，从`OutputStream`派生出的子类，都将基础下面的几个与写数据相关的方法:  
```java
void write(int c)
void write(byte[] buf)
void write(bhte[] b,int off,int len)
void close()
void flush()
```
**注意：**  
- 所有的这些方法在出现错误时都会抛出一个`IOExcepton`异常。在使用这些类或者方法操作数据的时候一定要注意抓取异常；
- `write`与`InputStream`的`read`方法一样，如果在向控制台或文件批量写数据时，选择后两种`write`方法将会提高`io`效率；

##### InputStream和OutputStream处理的是字节流；
但在许多的应用场合中，`java`程序需要读写文本文件中的字符，这就涉及到字符流的两个基类：`Reader`和`Writer`；

#### Reader类：
字符输入流`Reader`类与字节输入流`InputStream`类非常相似，它的方法用法，与字节输入流`InputStream`的方法非常的相似；
##### 常用方法:
```java
int read()
int read(byte[] c)
read(char[] c,int off,int len)
void close()
boolean ready()
skip(long n)
mark(int readlimit)
void reset()
```

#### Writer:
- 字符输出到流总要涉及到写数据，在数据被传输到流时，国际统一码将被自动地转换为本地计算使用的编码，与字节流相比，在字符流里字符是不进行自动转化的；  
- 当希望写文本到文件中或希望写字符串表示的数据时，就可以使用字符流。字符流`writer`与字节流`OutputStream`非常相似；
  
以下方法就是字符输出流的抽象类`writer`定义的需要被子类继承的方法。  
由于字符流直接以字符作为单位，因此在`writer`中字符数组以字符串来代替；
##### 方法：
```java
writer(String str)
writer(String str,int off,int len)
void close()
void flush()
```
**无论是输入流还是输出。处理完流对象后，都需要关闭流；**  
**抓异常时，最好将close方法放在finally中；**


### 读取/写入数据的步骤：

#### 读取：
1.打开流  
2.如有更多信息则读取信息  
3.关闭流  

#### 写入：
1.打开流  
2.如有更多信息则写入信息  
3.关闭流  



### 文本文件的读写：
#### 利用字节流`FileInputStream`读文本文件：
`FileInputStream`称为文件输入流，它的作用就是**将文件中的数据输入到内存中**，也就是读取文件的信息；`FileInputStream`是字节输入流`InputStream`类的一个子类；  
##### FileInputStream的构造方法：
- 参数都用来指定文件数据源；
|方法|     说明|
|---|---|
|FileInputStream(File file)|    file指定文件数据源|
FileInputStream(String name) | name指定文件数据源,包含路径信息；|

示例：  
```java
public static void main(String[] args) throws IOException {
FileInputStream fis = new FileInputStream("c:\\myDoc\\hello.txt");
int data;  //用来接收读取到的数据；
while((data=fis.read())!=-1) {
System.out.println(data+" ");
  }
//将字节整数转换为字符输出；
FileInputStream fis = new FileInputStream("c:\\myDoc\\hello.txt");
int data;  //用来接收读取到的数据；
while((data=fis.read())!=-1) {
char c =(char)data;
System.out.print(c);
  }

  fis.close();
}
```

运行结果：
97 98 99

- read方法是从输入流读取1个8位的字节，然后把它转换为0-255之间的整数返回；
- read（）方法是“单程”的；

##### 利用字节流FileOutputStream写文本文件：
- `FileOutputStream`文件输出流，它的作用   内存  中的数据输出到文件中去，也就是写文件；
- 它是字节输出流OutputStream抽象类的一个子类；
##### FileOutputStream的构造方法：
|方法|         说明|
|----|---|
|FileOutputStream(File file)|file指定文件目标数据源|
|FileOutputStream(String name)|name指定文件目标数据源，包含路径信息；|
|FileOutputStream(String name,boolean append)|append若true，则在文件末尾添加数据；|

**注意：在创建`FileOutputStream`实例时，如果相应的文件并不存在，就会自动创建一个空的文件；**

- 如果参数`file`或`name`表示的文件路径尽管存在，但是代表一个文件路径，一个目录，此时会抛出一个异常；
- 什么异常？`FilenotfoundException`就是文件没有找到的一个异常；
- 在默认情况下，向文件写数据时将覆盖文件中原有的内容；
- 第三个构造方法中的`append`为`true`，则可以避免覆盖文件中的原有的内容；
##### 示例： 
在文件末尾追加一句话：“好好学习JAVA”；
```java
try {
 String str = "好好学习JAVA";
 byte[] words = str.getBytes(); //将字符串转换成字                           节数组存放在words当中；
 FileOutputStream fos = new FileOutputStream("c:\\myDoc\\hello.txt",true);
fos.write(words,0,words.length);
System.out.println("hello文件已更新！");
fos.close();
} catch(IOException obj) {
  System.out.println("创建文件时出错！");
 }
```

#### 利用字符流BufferedReader读  文本文件：
- `BufferedReader`是`Reader`的子类；
- `BufferedReader`带有 ` 缓冲区`，它可以先把一批数据读到缓冲区中，接下来的读操作都是从缓冲区中读取数据；  
- 这样，可以避免每次都从数据源读取数据，进行字符编码转换，从而提高读操作的效率；
- 它有两种类型的构造方法，接收 Reader对象作为参数，并对其添加字符缓冲器；
##### BufferedReader的构造方法：
|方法| 说明|
|---|---|
|BufferedReader(Reader in)|参数in指定被装饰的Reader类|
|BufferedReader（Reader in,int sz)|参数sz指定缓冲区的大小，字符为单位；|

 他们都会触发向更底层的字符或字节流发出的相应的读取请求；

在通常情况下，对Reader发出的每个读取请求；这样，一层一层的发出请求，会导致产生多个读取步骤，而读取是计算机处理中最慢的动作之一；  
创建`BufferedReader`的实例便能为数据输入分配内存存储空间，使读取的过程更有效率；  
```java
InputStreamReader isr = new InputStreamReader(System.in);
BufferedReader br = new BufferedReader(isr);
```

示例：  
- 通过bufferedReader来读取文本文件hello中的内容；
```java
try {
//创建一个FileReader对象，它是Reader的一个子类，用来读取hello的内容；
FileReader fr = new FileReader("c:\\myDoc\\hello.txt");
//创建一个BufferedReader对象，将fr读取到的内容存放在缓冲区中；
BufferedReader br = new BufferedReader(fr);
String line = br.readLine();
while(line!=null) {
 System.out.println(line);
 line = br.readerLine();
 }
 br.close();
 fr.close();
}catch(IOException e) {
 System.out.println("文件不存在！");
}
```
#### 利用字符流BufferredWriter写文本文件：
- `BufferredWriter`是`Writer`的子类；
- `BufferredWriter`是把一批数据写到  缓冲区，当缓冲区满的时候，再把缓冲区中的数据写到字符输出流中；这样可以避免每次都执行物理写操作，从而提高`io`操作的效率；

##### BufferredWriter的构造方法：
|方法|                            说明|
|---|---|
|BufferredWriter（Writer out)|参数out指定被装饰的Writer类；|
|BufferredWriter(Writer out,int sz)|参数sz指定缓冲区的大小，字符为单位；|
- `newLine()`方法用来插入一个换行符，用来换行；  
示例：  
```java
//创建一个FileWriter对象
FileWriter fw = new FileWriter("c:\\myDoc\\hello.txt");
创建一个BufferredWriter对象；
BufferedWriter bw = new BufferedWriter(fw);
bw.write("大家好！");
bw.writer("我正在学习BufferedWriter。");
bw.newLine();
bw.writer("请多多指教！");
bw.newLine();
//清空缓冲区
bw.flush();
//关闭流
bw.close();
fw.close();
```

- `BufferredWriter`的`write()`方法写入的内容覆盖原来的内容；
- `BufferredWriter，BufferedReader`需要修饰到一个指定的输出流（FileWriter对象））；


#### 利用字节流类DataInputStream来读文件：
##### DataInputStream的继承关系：
它扩展自（直接继承）`FilterInputStream`。它是间接继承了`InputStream，
DataInputStream`与`DataoutputStream`搭配使用，可以按照与平台无关的方式从流中读取基本类型的数据，如：`int , float  long double `和` boolean` 等；  
此外，`DataInputStream`的`readUTF`方法还能读取`utf-8`字符编码的字符串；  

**注意：**`InputStream`类的所有读方法都是以`read`开头的；  

#### DataInputStream读方法：
```java
readByte()
readLong()
readFloat()
readUTF()
```

#### 使用DataInputStream操作方法的步骤：
1.引入相关的类  
- import java的io相关的一些类；  

2.构造数据输入流对象 如：
```java  
//创建FileInputStream fis对象指向二进制文件；
FileInputStream fis = new FileInputStream("HelloWorld.class");
//构造一个数据输入流对象，dis；
DataInputStream dis = new DataInputStream(fis);
```
3.读取二进制文件的数
- 利用数据输入流类的方法读取二进制文件；也就是一些read方法；
- 关闭数据输入流

#### DataOutputStream的继承关系：
- `DataOutputStream`扩展自`FilteOutputStream,DataOutputStream`，可以按照与平台无关的方式向流中写入基本类型的数据，如` int float long double`  和` boolean` 等；
- 此外，`DataOutputStream`的`writeUTR`方法还能写采用`utf-8`字符编码的字符串；
- `DataOutputStream`类的所有的写方法都是以`write`开头；
##### DataOutputStream写方法：
```java
writeByte()
writeLong()
writeFloat()
writeUTF()
```
#### 使用DataOutputStream操作文件的步骤：
（利用`DateOutputStream`写二进制文件，同样要用`FileOutputStream`）
1.引入相关的类；
2.构造数据输出流类对象；
3.利用数据输出流的方法写二进制文件的数据；
4.关闭数据输出流；
##### 示例：

（功能：从一个二进制文件FileMethods.class读取数据，然后复制到另一个二进制文件temp.class的过程)
```java
//创建输入流对象
FileInputStream fis = new FileInputStream("c:\\myDoc\\FileMethods.class");
DateInputStream dis = new DataInputStream(fis);
//创建输出流对象；
FileOutputStream outFile = new FileOutputStream("c:\\myDoc\\temp.class");
int temp;
//读取文件并写入文件；
while ((temp = dis.read()) !=-1) {
  out.write(temp);
}
//关闭数据流

```

#### 源数据源和目标数据源不变：
##### 在JDK的java.lang.System当中，提供了三个静态变量：
```java
System.in
System.out
System.err
```
- System.in为inputString类型，它代表着标准输入流；  
默认的数据源为键盘，程序可以通过System.in读取标准输入流的数据；  
- System.out为PrintStream类型，它代表的是标准输出流，  
 默认的数据源是控制台（显示器），程序可以通过System.out输出运行时的正常消息；  
- System.err为PrintStream类型，  它代表标准错误输出流；  

这以上三种流都是JAVA虚拟机创建的；  
它们存在于整个运行生命周期中，这些流始终处于打开状态；除非我们利用程序显式的来关闭它们。只要程序没有关闭这些流，那么在程序运行的任何时候都可以通过它们来输入或者输出数据。这些就是标准输入输出的含义；  

#### 重定向标准输入输出：
- System类里提供三个重定向标准输入和输出方法，
|方法 |                          说明|
|----|---|
|static void setErr(PrintStream err)|重定向标准错误输出流|
|static void setIn(InputStream in)|重定向表现输入流|
|static void setOut(PrintStream out)|重定向标准输出流|


##### 将标准输出重定向到文件：
```java
//创建PrintStream输出流
PrintStream ps = new PrintStream(new FileOutStream("c:\\myDoc\\hello.txt"));
//重定向到文件                                                                                      
System.setOut(ps);
//向文件print写内容，而不是控制台（屏幕）
System.out.print("我的测试，重定向到文件hello!");
System.out.println(new ReOut());
```
##### 重定向标准输出流：
1.初始化PrintStream对象  
2.调用System.setOut()方法将标准输出流重定向到PrintStream对象；  
3.对System.out流进行操作；  

##### 重定向标准输入：
```java
//创建输入流
FileInputStream fis = new FileInputStream("c:\\myDoc\\hello.txt");
//重定向到文件
System.setIn(fis);
Scanner sc = new Scanner(System.in);
System.out.print("从文件读取懂啊的内容为： " +sc.next());
```
#### 重定向标准输入流：
1.有一个已经初始化的`Inputstream`输出入流；  
2.调用`System.setIn()`方法，将标准输入流重定向到目的输入流；  

### 对象序列化：
所谓序列化是指将一个`JAVA`对象借助`I/0`流的形式，实现数据的  传输  或者  保存 ；
简单的说，序列化就是将对象的状态存储到特定存储介质中的过程；也可解释为：是将对象状态转换为可保持或可传输的格式的过程；  
序列化就是将各种对象状态，保存起来，并且在必要的时候方便的将对象状态再读取出来；

### 支持可序列化（serializable)
- 在`JAVA`当中，要求只有实现了`java.io.Serializable`这个接口的类的对象才能被序列化；
- 如果需要让某个对象可以被序列化，它必须是可序列化的，
- 即必须实现`java.io.Serializable`接口；
- JDK类库中有些类，如`String`类、包装类和`Date`类，都实现了这个接口；
实现这个接口不需要实现它的任何方法，
#### 对象序列化的步骤：
1.创建一个对象输出流-`ObjectOutputStream`，
它可以包含一个其他类型的输出流，比如文件输出流`FileOutputStream`。
如：  
```java
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("c:\\myDoc\\stu.txt"));
```
2.通过对象输出流的`writeObject()`方法写对象，也就是输出可序列化对象；
如：  
`oos.writeObject(stu); //stu为某类对象；`

##### 示例：  
```java
public class Student implements java.io.Serializable {
 private String name;
 private int age;
 private String gender;
 public Student(String name,int age,String gender) {
 this.name = name;
 this.age =age;
 this.gender = gender;
System.out.println("带参数的构造方法");
}
public String getName() {
 return name;
 }
....//省略其他的get/set方法
 
}
```
定义类`SerizlizableObj`,代码片段；
```java
ObjectOutputStream oos = null;
try {
  //创建ObjectOutputStream输出流
oos = new ObjectOutputStream(new FileOutputStream("c:\\myDoc\\stu.txt"));
Student stu = new Student("安娜",30,"女");
 //对象序列化，写入输出流
oos.writeObject(stu);
}catch(IOException ex) {
 ex.printStackTrace();
}finally {
 if(oos!=null) {
   oos.close();
   }
}
```
### 反序列化：
 如果希望从二进制流中恢复JAVA对象，则需要用到反序列化；
#### 反序列化的步骤：
1.创建一个对象输入流-`ObjectInputStream`,
它可以包含一个其他类型的输入流，比如文件输入流`FileInputStream`。  
2.通过对象输入流的`readObject()`方法读取对象，该对象返回一个`object`类型的对象，如果程序知道该`JAVA`对象的类型，则可以使用该对象强制类型转换成其真实的类型；
##### 反序列化示例：
```java
ObjectInputStream ois = null;
try {
 //创建objectOutStream输出流
ois = new ObjectInputStream(new FileInputStream("c:\\myDoc\\stu.txt"));
//反序列化，强制类型转换
Student stu = (Student)ois.readObject();
//输出生成后的对象信息
System.out.println("姓名为： " +stu.getName());
System.out.println("年龄为： " +stu.getAge());
System.out.println("性别为： "+stu.getGender());
}catch(IOException ex) {
 ex.printStackTrace();
}finally{
    if(ois!=null) {
             ois.close();
            }
 }
```
##### 实现对象序列化和反序列化，强调内容：
- 反序列化机制无需通过构造器来初始化JAVA对象；
- 反序列化机制并不是通过构造器来初始化对象的；
- 如果向文件中使用序列化机制写入多个对象，那么反序列化恢复对象时，必须按照写入的顺序读取；
- 如果一个可序列化的类，有多个父类，包括直接或间接父类，则这些父类要么也是可序列化的，要么有无参数的构造方法，否则会抛出异常；

##### 禁止序列化某属性信息：
- 使用transient修饰来禁止序列化某些信息；

##### 包含引用类型属性的对象序列化：
引用类必须也为可序列化的；  
如：  
- Teacher类中包含有Student类，Teacher类要求可序列化，则Student类必须可序列化；
- 补充：在Teacher类中，有一个构造方法，构造方法是传递参数、姓名和它所引用的对象；
##### 序列化算法：
- 所有保存到磁盘中的对象都有一个序列号；
- 当程序试图徐哭过序列化一个对象时，将会检查是否已经被序列化，只有序列化后的对象才能被转换成字节序列输出；
- 如果对象已经被序列化，则程序直接输出一个序列化编号，而不再重新序列化；


#### 序列化算法：
1.序列化时候，会查找当前对象的序列化编号是否存在，如果不存在，则保存该对象；  
2.写入操作时，当对象序列化编号存在的时候，会输出一个当前对象的序列化编号，而不是当前对象；  
3.反序列化对象时，程序会自动查找当前对象的序列化编号，如果发现当前对象的序列化编号被其它对象引用，则返回同一个对象；  

## 总结：
- File类访问文件或目录的属性；

### Java的数据流：

### 按照处理数据单元划分：
#### 字节流：
- 字节输入流InputStream基类；
- 字节输出流OutputStream基类；
#### 字符流：
- 字符输入流Reader作为基类；
- 字符输出流Writer作为基类；

`FileInputStream`和`FileOutputStream`以字节流的方式读写文本文件。

`BufferedReader`和`BufferedWriter`以字符流的方式读写文本文件。

字节流类`DataInputStream`读二进制文件

字节流类`DataOutputStream`写二进制文件

序列化`ObjectInputStream`类和反序列化`ObjectOutputStream`类；




