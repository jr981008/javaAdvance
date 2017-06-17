# JDK
- java.lang包是自动导入到所有程序中的包；

## java.util包下：


### 1，Java集合框架：

- 接口：  
`Collection；  
   List；
   Set；
   Map； `  
- 实现类：  
`ArrayList；
LinkedList；
HashSet；
HashMap；`

- 工具类：
- Collections类；


### 2，处理日期和时间的类：
`Date类；
Calendar类；
   GregorianCalendar类；`

### 3，迭代器接口：
`
Iterator接口；`

### 4，伪随机数生成器：
`Random类；`

### 5，Scanner类；

##java.lang包中包含的是Java程序的基础类和接口；
###在java.lang包下：
#### 1，枚举：
默认父类是Enum类；
#### 2，包装类（共8个）；
`boolean类；
Character类；
继承自抽象类Number类的：
Byte类；
Short类；
Int类；
Long类；
Float类；
Double类；`
#### 3，Math类；

#### 4，String StringBuffer 和 StringBuilder类；
#### 5，java.lang.System类；
`System.in   System.out  System.err 是  流；`

#### 6，线程类：
##### 接口：
java.lang.Runnable接口；
##### 实用类：
Thread类；

#### 7，反射机制：
```
java.lang.Class;
java.lang.reflect.Field;
java.lang.reflect.Method;
java.lang.reflect.Constructor;
```

#### 8.注解：
- java.lang.annotation包；
- 接口：Annotation；

#### 9.java.text包下：
##### DateFormat类；
	SimpleDateFormat类；
（对时间和日期模式的格式化和解析）


## java.io包下：
### 接口：
- Serializable;

### 抽象类：
`InputStream类；
OutputStream类；
Reader类；
Writer类；`


### 实用类：
`File类；`
```
FileInputStream；
FileOutputStream；

BufferedReader；
BufferedWriter；

DataInputStream；
DataOutputStream；

ObjectInputStream;
ObjectOutputStream;

```

## java.net包下：
- Socket类；
- ServerSocket类；

- DatagramPacket类；
- DatagramSocket类；
