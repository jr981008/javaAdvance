# 实用类
## 枚举类型：（是一个类）
- 枚举是指由一组固定的常量组成的类型；
- 简单的说，枚举就是使用一组常量值来表示特定的数据集合，只是在这个数据集合定义时，所有可能的值都是已知的，只要是固定的常量都可以定义成枚举类型；

-  类的定义：
```java
public class ClassName{
}
```

- 枚举类型的定义：
```java
public enum EnumName {
}
```

- 在定义枚举的时候需要一个关键字enum；
```java
publc enum Week {
   MON,TUE,WED,THU,FRI,SAT,SUN
}
```
- Week是枚举的名称，大括号里面定义枚举常量，枚举常量就是固定常量；根据惯例，枚举常量的名称总是大写；
- 其实枚举常量就是枚举的静态字段；枚举常量之间使用逗号隔开；
- 其实每一个枚举常量都引用枚举的一个对象，所以我们不需创建对象就可以直接使用，其实我们也不能够创建枚举对象；
- 其实我们定义的Week枚举只不过是个简单的常量集合；
- 而JAVA枚举实际上是功能十分齐全的一种特殊类型的类；
- 在定义枚举时 ，无论是形式上还是使用方式方面的限制都与普通的类不同；
## 定义枚举的语法：
```java
[Modifier] enum enumName {
   enumConstantName1[,enumConstantName2...[;]]
    //[field,method]
}
```

- 定义枚举需要使用`enum`关键字而不是`class`，枚举中能够定义枚举常量，多个枚举常量之间是以逗号隔开，除此之外，还可以定义普通类的成员，包括构造方法，只不过构造方法必须是私有访问级别的；

- 注意：在定义任何其他类成员之前，枚举类必须首先定义枚举常量，如果枚举中除了枚举常量还要定义其它成员，那么枚举常量的列表必须以`；`号结尾；

### 枚举的默认父类是Enum类，属于java.lang包下，
- `java.lang`包是自动导入到所有程序中的包，包含的是JAVA程序的基础类和接口，它包含能够把基本类型的值当成一个对象来表示的包装类；`Math`类提供了常用的数学函数；
- `String、StringBuffer 和StringBuilder`类提供了常用的字符串操作；
- `JAVA.lang`包还提供了用于管理类的动态加载、外部进程创建、主机环境查询和安全策略实施等“系统操作”的类。

- JAVA程序设计语言为每一种基本类型都提供了一个包装类，而这些包装类就在`java.lang`包中；
### 包装类：
是指，将基本数据类型封装到一个类中，也就是将基本类型包装成一个类类型；  
### java.lang包中包含了8个包装类；

* `boolean`类包装的是布尔类型，`Character`类包装的是字符，
包装所有数字类型的类都继承自`Number`类，`Number`类是一个抽象类，包装了 `Byte Short Int Long Float Double` 等数字类型的类都继承自它，并实现了它定义的方法，这些方法以不同数字格式返回对象的值；
### 包装类是如何构造基本类型的：
#### 每一个包装类都有两个构造方法，
- 第一个构造方法：`public Type (type value)`;首字母大写的`Type`表示包装类，小写的`type`代表基本类型；
	- 这个构造方法接收一个基本类型的值，并创建一个与之相应的包装类；
	- 针对每一个包装类，我们都可以用new关键字将一个基本类型值包装为一个对象；
	
	- 要创建一个Integer类型的包装类：
	`Integer intValue = new Integer(21);`
	- Long类型的：
	`Long longValue = new Long(21L);`
	- 字符类型：
	`Character charValue = new Character('x');`
	- 注意：传递给包装类构造方法的参数，要是该包装类所包装的基本类型的值。
	- 注意：每一个包装类都为它所包装的基本类型定义一个不可变的对象；即一旦创建了某个包装类对象，该对象所代表的值就不能改变了。
- 第二个构造方法：`public Type (String value)`
	- 是将一个字符串参数转换为包装类，但是`Character`类除外；
	- 注意：传入的字符串要符合基本类型的要求，
	- `Character`类：不能接受字符串；
- 每一个包装类中都包含 静态 的重载的`valueOf`方法，与构造方法相同，`alueOf`方法也可以接收  基本类型数据和字符串  作为参数，并返回    包装类的对象；
#### 参数为基本类型的valueOf方法：
`public static Type valueOf(type value)`
- 对参数为基本类型的`valueOf`方法，我们可以用要转换的包装类（valueOf方法是静态方法，可以直接使用类来调用）调用`valueOf`方法，括号中传入相应的正确的基本类型；  
示例：
```java
Short shortValue = Short.value（short) 21);
Integer intValue = Integer.valueOf(21);
Character charValue = Character.valueOf('x');
Boolean booleanValue = Boolean.valueOf(true);
```
#### 参数为字符串类型的valueOf方法：
`public static Type valueOf(String s)`
- 对于参数为字符串类型的`valueOf`方法，需要强调一下，`Character`
注意：传给`valueOf`方法的字符串限制，和传给包装类构造方法的字符串限制是相同的；  
示例：:smile:
```java
Byte byteValue = Byte.valueOf("21");
Integer invalue = Integer.valueOf("21");
Boolean booleanValue = Boolean.valueOf("true");
Float floatValue = Float.valueOf("21.21");
Double doubleValue = Double.valueOf("abc");
```
#### 在Character类中有两个常用的静态方法：
`public static boolean isDigit(char ch)`
确定指定字符是否为数字；  
`public static boolean isLetter(char ch)`
确定指定字符是否为字母；

### 包装类中的类型转换，常用的有三种，有：
- 包装类型转换成基本类型；
- 字符串转换成基本类型；
- 基本类型转换成字符串；



### 包装类型转换成基本类型采用的方法：
`public type typeValue();`  
基本类型 变量名 = 包装类型变量名.typeValue();  
- typeValue中的type，指的是基本数据类型，  
- 比如：`byteValue charValue`等等；  
- 使用：
```  
	Integer类型的integerId，转换成int类型；
	Integer integerId = new Integer(25);
	int intId = integerId.intvalue();
	Boolean包装类型bl转换成基本类型boolean：
	Boolean bl = Boolean.valueOf(true);
	boolean bool = bl.booleanValue();
```
其它的包装类转换也是一样的；

### 字符串转换成基本类型：
它采用的是静态的方法，  
`public static type parseType(String type)`  
`parseType：`
- `parseType`可以是`parseByte  parseDouble` 等等；
- 注意：`Character`类没有此静态方法；  
- 举例：
```
字符串“36”转换成int类型：
int num = Integer.parseInt("36");
字符串“false”转换成boolean类型，
boolean bool = Boolean.parseBoolean("false");
注意：这里的参数也得是相应类型的正确字符串表示形式；
```
### 基本类型转换成字符串：
`public static String toString(type value);`
也是一个静态方法；
- 举例：
```
String sex = Character.toString('男');
String id = Integer.toString(25);
```
- 在开发中，为了省事通常在基本类型后面用加号连接一个空字符串来进行转换；
- 举例：
```
String sex = '男’+"";
String id = 25 + "";
```

### 包装类和基本类型之间的转换，叫做自动装箱和拆箱；
- 装箱：基本类型转换为包装类的对象；
- 拆箱：包装类对象转换为基本类型的值；
- 在`JAVA SE 5.0` 之后，不需要用编码来实现它们之间的转换了，`JDK`会自动帮助我们完成；
- 比如：
```
声明一个Integer类型的变量为intObject，赋值为int类型的5，这就是自动装箱；
将Integer类型的intObject，赋值为一个int类型的intValue，就实现了拆箱的过程；
```
- `list`在调用`add`方法时，传入基本类型不报错：
- 当传入基本类型时 ，都会自动包装成一个相应的包装类，而所有的包装类又是`Object`的子类；当然不会报错了；
- 注意：包装对象只有在基本类型需要用对象表示时才使用，包装类并不是用来取代基本类型的；

### Math类：
提供了常用的数学运算方法和两个静态常量E（自然对数的底数）和PI（圆周率）；
- Math类中定义的方法都是公有的静态方法，不需要创建Math的对象就可以直接调用；
- Math类中定义的方法非常多，看几个常用的方法：
	- max方法：
	`public static type max(type a, type b)`返回两个参数中最大的一个；  
	- 比如：
	`int num1 = Math.max(20,25); num1 = 25;`
	- 当然，max方法还有多个重载的方法，用来比较float、double等数据类型；
	- pow方法，（求幂运算）：
	`public static double pow(double a,double b)`返回a的b次幂的值；  
	- 比如： `double powNum = Math.pow(3,2); powNum = 9;`
	- 得到0到1之间的double类型的随机数的方法：random方法；
	`public static double random()`返回值大于等于0.0且小于1.0；  
	- 如果我们想得到一个1到10的随机整数；则： `int random  = (int)( Math.random()*10+1);`
 

	- 求绝对值的`abs()`方法，返回两个数较小的`min()`方法，
	- 求正平方根的`sqrt()`方法和返回最接近参数（double或float）的（long或int）的`round`方法；

	- Math类中还定义了完备的三角函数方法，
如：sin() cos() tan() asin() 等；

### 字符串的操作类
#### String类：
- 特点：  一个String对象所包含的字符串内容永远不会改变；
- String类中定义了许多处理字符串的方法，
	#### equals()方法；  
	```
	public boolean equals(Object anObject)
	boolean bl = "tom".equals(uesrName);  //true
	boolean bl = "  tom".equals(uesrName);
	//false;这是不合情理的；
	```
	
	#### trim方法；
	`public String trim()`返回一个去掉前后空格的字符串副本，先用输入的用户名调用trim（）方法去掉前后的空格，`String newName = "  tom".trim();`- 再用equals()方法来比较：
	```
	boolean bl = newName.equals(userName); //true
	```
	也可以一行：
`boolean bl = "  tom".trim().equals(userName);`
- equals方法在比较时区别大小写；
- equalsIgnoreCase方法，不区别大小写；
```java
public boolean equalsIgnoreCase(String anotherString)
boolean bl = "eYHa".equalsIgnoreCase("EyhA") 
//true;

```

#### substring 方法：  
`public String substring(int beginIndex,int endIndex)`
- 此方法是返回一个从指定的`beginIndex`处开始，直到索引endIndex-1处的字符；
- 第一个参数表示从这个字符开始，包括此字符，第二个参数表示到此位置，但不包括该字符；
```java
String s1 = "我是中国人";
String newS1 = s1.substring(2,4);
//截取 中国；
```
- 如果我们要截取从某处索引开始到结尾，可以调用substring的重载方法；  
`String newS2 = s1.substring(2);`截取 中国人；

### 查找功能的方法：indexOf方法；
`public int indexOf(String str)`返回指定子字符串在此字符串中第一次出现的索引位置；
`int index = s1.indexOf("国");`返回结果就是3;
- 当所要查找的字符串不存在的时候，则返回-1；
- 获得字符串长度的`length`方法：

- 字符串转换大小写的`toLowerCase`和`toUpperCase`方法，

- 拆分字符串的`split`方法：




### StringBuffer类，
对于经常修改的字符串，可采用字符串操作类
- `StringBuffer`的特点是可变长的，`StringBuffer`对象可以将一些字符和字符串插在原字符串中间或末尾，它经常预先分配比实际需要更多一些的字符空间，即预先分配一定长度的缓冲区，来满足增长的需要。
- 创建一个`StringBuffer`的对象：常用的构造方法：
	- 一种是不带参数的，它是创建一个不带字符，但具有指定初始容量的`StringBuffer`对象；
```
public StringBuffer(); //构造方法
StringBuffer sbf = new StringBuffer(); //创建对象
```
- 一种是带`String`类型参数的，它是将其内容初始化为指定的字符串内容。
```
public StringBuffer(String str); //构造方法
StringBuffer sbf = new StringBuffer("我会变长的");
```
- 该字符串的初始容量为16加上字符串参数的长度；
- `StringBuffer`中有些方法和`String`类中的方法用法相同，比如 `substring`方法，`charAt（）`方法等等；
### StringBuffer类常用的方法：
- 对`StringBuffer`对象进行修改的方法，  `append`方法：  
`public StringBuffer append(Type value)`
- append方法有很多重载方法，能够把任何类型数据的字符串表示形式添到StringBuffer对象的末尾。
- 举例：
```java
StringBuffer sbf = new StringBuffer("变！");
sbf.append("变形金刚");
sbf.append(3);
//最终sbf变成了： "变！变形金刚3"。
```
它使用的始终是一块空间；这充分体现了StringBuffer的可变性；

- StringBuffer类的reverse方法，
它是将字符串用其反转形式取代，
```java
StringBuffer name = new StringBuffer("万千一");
name.reverse();
//name变为"一千万";
```
### toString方法：
- 它能将`StringBuffer以String`的类型返回；
`public String toString();`

- 另外StringBuffer还有删除、增加功能；
替换功能与`String`的用法不太一样；



## java.util包：
`java.util`包包含了常用的工具类和接口，比如：JAVA集合框架和用于处理日期和时间的类、能够产生伪随机数等等；

### 处理日期时间的类：
- Date类封装了当前的日期和时间，以毫秒来表示特定的日期；
- 抽象类Calendar提供了一组方法，可以获取一个时间的年、月、日的整型值；
- 另外还有一个处理日期时间的类，DateFormat类，它在java.text包下，是一个抽象类，提供了多种格式化和解析时间的方法。

### Date类：
- 它是记录从基准时间开始至今的毫秒数，最常用的就是Date类的构造方法，用来获得当前系统时间；
- 对于其它处理日期和时间的一些操作推荐使用Calendar类和DateFormat类；
### Calendar：
- Calender可以看做是Date的一个增强版，它提供了一组方法，允许把一个以毫秒为单位的时间转换成年、月、日、时、分、秒。可以把Calender类当做是万年历；
- 默认显示的是当前时间；当然也可以查看其他的时间；
- Calendar类是抽象类，可以通过静态方法getInstance获得Calendar类的对象；
```java
public static Calendar getInstance() {
 Calendar calendar = Calendar.getInstance();
```
其实这个获得的对象应该是它的子类的对象；

- Calendar类中定义了许多int型的日历字段，它们都是常量，在方法中可以使用它们来操作时间的各个部分；
- 需要强调下日历字段是用来表示时间、日期的各个部分的数字，并不是时间、日期的各个部分，需要将它们作为参数传给Calendar对象，我们才能操作时间、日期的各部分；
#### 常用的几个日历字段：
- MILLISECOND 表示的是毫秒的数字；
- SECOND 表示时间中秒的数字；
- MINUTE 表示分钟的数字；
- HOUR 表示上午或下午的小时的数字。用于表示12小时制的数字，它的范围是1到11，中午12点和午夜0点都是用0来表示；
- HOUR_OF_DAY 表示一天中的小时的数字。它表示的时间部分是24小时制的时钟；
- AM_PM 表示时间是在中午之前还是中午之后的数字；

#### 有关日期的字段：

- YEAR 表示年的数字；
- MONTH 表示月份的数字；
- DATE表示月中的某天的数字；
- DAY_OF_MONTH表示月中的某天的数字。它与DATE是同义词。它们表示的时间部分是相同的。  
`注意：一个月中的第一天的值应该是1；`
- 将日历字段作为参数传给Calendar对象我们可以操作它们所表示的时间、日期的各个部分，日历字段总是作为方法的第一个参数；
#### Calendar对象的常用方法：
##### get方法：
`public int get(int field) `: 返回给定日历字段表示的日历部分的值；

- 示例，获取当前时间的年、月、日、时、分、秒：
```java
Calendar calendar = Calendar.getInstance();
int year = calendar.get(Calendar.YEAR);
int month = calendar.get(Calendar.MONTH)+1;
int date = calendar.get(Calendar.DAY_OF_MONTH);
int hour = calendar.get(Calendar.HOUR_OF_DAY);
int minute = calendar.get(Calendar.MINUTE);
int seconde = calendar.get(Calendar.SECOND);
System.out.println("今天是： "+year+"年"+month+"月"+date+"日");
System.out.println("现在是； " +hour+"："+minute+"："+second);
```
- 我们将日历字段作为参数传给calendar对象获得日历字段所表示的日历部分的值，get方法返回的值是整型；  
`注意：返回的月份的取值范围是0到11，所以在返回值的基础上加1.这段代码只获取时间和日期，并未对它进行操作；`


#### set方法：用来设置日历字段；
`public void set(int field,int value);`
- 将给定的日历字段表示的日历部分设置为给定值，field代表日历字段，value代表设置的新值，
- 示例：将当前时间的月份设置为9月：
```java
Calendar calendar = Calendar.getInstance();
calendar.set(Calendar.MOTH,8);
```
还有多个方法重载，具体使用可以查看API;


#### add方法：
它是根据日历的规则，为给定的日历字段添加或减去指定的时间量；
- 示例：在当前时间上加10天；
```java
Calendar calendar = Calendar.getInstance();
calendar.add(calendar.DAY_OF_MONTH,10);
```
- 说明：add方法是个抽象方法，在Calendar类的子类GregorianCalendar类中有add方法具体实现，实际上子啊调用Calendar类的add方法时，使用的就是GregorianCalendar类的add方法；

#### isLeapYear方法：

`public boolean isLeapYear(int year) `: 确定给定的年份是否为闰年；
- 示例：判断今年是否是闰年；
```java
GregorianCalendar  grc = new GregorianCalendar();
boolean isY = grc.isLeapYear(grc.get(grc.YEAR));
```

- DateFormat类提供了多种格式化和解析时间的方法；
- 格式化是指将日期转换成文本；解析是指文本转换成日期格式；常用的是DateFormat类的子类SimpleDateFormat类；
- SimpleDateFormat类可以通过用户定义的日期-时间格式的模式完成格式化和解析的操作；
- 所谓的日期和时间模式其实就是，由日期和时间模式字符串指定，而日期和时间模式字符串是由具有特定含义的字母组成的。这些字母称为模式字母；
- 先认识一下模式字母所表示的时间和日期元素，
|字母|   日期或时间元素|  字母|        示例|
|---|----|----|----|
|G  |    Era标识符 |       H |  一天中的小时数（0-23）|
|y  |     年              |k |  一天中的小时数（1-24）|
|M  |    年中的月份    |  K|   am/pm中的小时数（0-11）|
|w  |     年中的周数    | h |  am/pm中的小时数（1-12）|
|W  |   月份中的周数    |m   |  小时中分钟数|
|D  |  年中的天数      |s   |     分钟中的秒数|
|d  |   月份中的天数  |  S |       毫秒数|
|F  |    月份中的星期  |  z |         时区|
|E  |     星期中的天数  | Z  |          时区|
|a  |      am/pm标记|  |  |

`注意：模式字母的大小代表不同的时间和日期元素，`

- 如何用表示一个日期和时间模式字符串来表示一个日期和时间：  
- 以年月日时分秒的格式显示当前时间：内存日期和时间模式：  
```
"yyyy年MM月dd日    HH:mm:ss"
显示的结果就是：2011年10月19日 11:48:18
```
- 这样看来，模式字母通常是重复的，而且除了模式字母，其它字符都不解释，而是直接当字符串显示出来了。
- 如果想显示结果：2011y,怎么办？
- 可以用单引号引起来，相当于转义符，可以写成:"yyyy'y'"

- SimpleDateFormat类对时间和日期模式的格式化和解析的操作，其实就是通过父类DateFormat类的format方法和parse方法来实现的；
- 如何创建一个SimpleDateFormat类的对象：
#### 常用的构造方法：
- 第一个构造方法是用默认的模式和默认语言环境的日期格式符号构造一个SimpleDateFormat对象，
```java
public SimpleDateFormat() //构造方法
SimpleDateFormat sdf = new SimpleDateFormat();
//创建对象
```
- 第二个构造方法是用给定的模式和默认语言环境的日期格式符号构造SimpleDateFormat对象；
```java
public SimpleDateFormat(String pattern) 
//构造方法
SimpleDateFormat sdr = new SimpleDateFormat(
"yyyy-MM-dd hh:mm:ss");
```
#### 常用的方法：
- format方法；它是将一个Date对象格式化为日期/时间字符串  
`public final String format(Date date)`
- parse方法：从给定字符串的开始解析文本，来生成一个日期对象；  
`public Date parse(String source)`

- 用SimpleDateFormat对象来进行格式化和解析：
```java
public class Test {
 public static void main(String[] args) {
  //以给定的时间和日期模式字符串创建一个SimpleDateFormat对象；
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
//获取当前的时间
Date date = new Date();
//时间格式化为指定的模式的字符串
String dateStr = sdf.format(date);
System.out.println(dateStr);
//定义日期-时间的字符串
String newStr = "2011-08-25 14:07:26";
//解析文本生成日期对象
try  {
  Date newDate = sdf.parse(newStr);
} catch(ParseException e) {
   e.printStackTrace();
  }
}
}
```
在调用parse方法时会产生ParseException异常，要进行日常处理；


#### util包下的常用类---Random类；
- Random类是一个伪随机数生成器；
- Math类的random方法也可以产生伪随机数；
- 其实，Math类的random方法底层就是使用Random类实现的；
##### Random类定义了两个构造方法：
- 第一个构造方法是创建一个新的伪随机数生成器，它使用当前时间为初始值，也就是种子值；
种子数：
- 在进行随机时，随机算法起源数字称为种子数，在种子数的基础上进行一定的变换，从而产生需要的随机数字；
```java
public Random() //构造方法
Random random = new Random();
```
- 第二个构造方法是允许定义一个long类型的种子来创建一个新的伪随机数生成器。
```java
public Random(long seed)  //构造方法
Random random = new Random(25);
```
##### Random类还定义了很多方法用于获取伪随机数。
- 常用的方法：
- nextInt方法；它返回下一个伪随机数，返回值类型是整型。
```java
public int nextInt();  //方法声明
int num = random.nextInt();  
```
还有一个重载的nextInt方法，它接收一个int类型的参数，
它也是返回下一个伪随机数；但是它是取自于0到指定的整数值；
（在0（包括0）和指定值（不包括）之间均匀分别的int值)
```java
public int nextInt(int n)
int num = random.nextInt(10);
```
- 在这里指定了10，它返回的下一个伪随机数就是0到10之间；
- 说明：如果用同样的一个种子值来初始化两个Random对象，然后用每个对象调用相同的方法，那么得到的伪随机数也是相同的；
```java
Random random1 == new Random(100);
int n1 = random1.nextInt(20);
Random random2 = new Random(100);
int n2 = random2.nextInt(20);
n1 = 15
n2 = 15
```
另外Random类还定义了得到长整型、boolean型、浮点型等伪随机数的方法；


## 总结：

- 枚举的语法：
```java
[Modifier] enum enumName{
   enumContantName1[,enumConstantName2...[;]]
   //[field,method]
 }
```
### java.lang包下的一些常用类：

### 包装类：
- 构造方法：
```java
public Type (type value)
public Type (String value)
```
- 常用方法：
```java
public static Type valueOf(type value)
public static Type valueOf(String s)
```
- 常用的类型转换：
```java
public type typeValue()
public static type parseType(String type)
public static String toString(type value)
```

- Math类常用的数学运算方法：  
max方法、
min方法、
random方法、
pow方法、
sqrt方法、

- String类的常用方法：  
equals方法、
equalsIgnore方法、
substring方法、
indexOf方法、
replace方法、
trim方法、
length方法；

- StringBuffer类：  
append方法、
reverse方法、
toString方法、
replace方法；

- 时间和日期处理类：  
`Date date = new Date();`
- Calendar类提供的方法将毫秒为单位的时间转换成年、月、日、小时、分、秒；
- SimpleDateFormat类常用构造方法：
```java
public SimpleDateFormat()
public SimpleDateFormat(String pattern)
```
- SimpleDateFormat类常用方法：
```java
public final String format(Date date)
public Date parse(String source)
```
- Random类：
`Random`类是一个伪随机数生成器，定义了可以得到`int`型，长整型、`boolean`型、浮点型等伪随机数的方法。
:snaik:
