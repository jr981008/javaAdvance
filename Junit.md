# 使用Junit
## 软件开发周期：
- 项目调研
- 需求分析
- 软件设计
- 程序编码
- 软件测试
- 运行维护

## 软件测试：
- 定义：  
利用测试工具按照测试方案和流程对产品进行功能和性能测试，使用人工或自动手段来运行或测试某个系统的过程。目的在于检验是否满足规定的需求确认预期结果与实际结果之间的差别。

## 软件测试：
- 通常用到的软件测试包括黑盒测试，白盒测试、回归测试、单元测试这几种方式。
### 黑盒测试：
- 注重于测试软件的功能性需求。
- 测试者完全不考虑程序的内部结构和特性，只需要知道程序输入和输出之间的关系或程序功能，
### 白盒测试：
- 白盒测试人员需要对被测试程序的内部结构非常清楚，从程序的内部逻辑结构入手，来判定实际情况是否和预期的状态一致。
### 回归测试：
- 回归测试是指当程序代码被修改后，重新进行测试，以确认修改没有引发新的错误或导致其他代码产生错误。
### 单元测试：
- 单元测试是软件开发过程中最低级别的测试，也是最小粒度的测试，主要测试程序中的某个功能或代码块。
- 单元测试的工作一般由程序员来承担。


## JUnit：
- JUnit诞生于1997年，它是一个开放源代码的Java测试框架，用于编写和运行可重复的测试。
- JUnit设计的虽然很小巧，但是功能却非常强大。
- 评价：在软件开发领域，从来就没有如此少的代码起到了如此重要的作用。它大大简化了开发人员执行单元测试的难度。
- JUnit提倡单元测试的简单化和自动化。而Junit本身的设计也是遵循这个前提；
- 整个框架的骨干仅有三个类组成：
- JUnit正是依赖这三个类进行单元测试，最终呈现一个测试结果：TestResult。
### TestCase类
- 负责测试时对客户类的初始化以及测试方法的调用，
- TestCase类继承自Assert类；
### TestSuite类
- 负责包装和运行所有的测试类；
### TestRunner类
- 运行测试代码的运行器。


## Assert类：
断言：
- 断言就是一个包含布尔表达式的语句。在执行这个语句的时候，如果语句的结果是False，那么系统会提示错误。
- 它主要用于调试程序，反之，就是成功的；
- 因此，说白了，断言就是判断期望值和实际值是否相等。
- Assert类提供了JUnit使用的一整套断言，是一系列断言方法的集合；常用的静态断言方法如下：
`assertEquals(Object expected,Object actual)`
- 用来判断期望值与实际值是否相等。
- 比如：  
`Assert.assertEquals(3,3);`
断言成功；  
`Assert.assertEquals("骑白马的男人","王子");`
断言失败；



`assertNotNull() / assertNull()`  
这俩个方法来判断一个对象是否非空或为空，
比如：   
```
String s = null;
Assert.assertNull(s);
```
断言成功；

`assertTrue()   assertFalse()`  
这两个方法用来判断一个条件是True还是False，  
比如： `Assert.assertTrue(1==3);`
断言失败；
`Assert.assertFalse(1==3);`
断言成功；

## TestCase类：
- TestCase类是Assert类的一个子类，因此，Assert类中的整套断言方法都被TestCase类继承了下来。而且，TestCase类中还提供了对客户类初始化以及运行测试的方法，比如：
	- setUp() :
可以完成测试类运行前的初始化工作。


	- runTest():
测试类运行时调用的方法；
一般这个方法不用我们自己去实现。

	- tearDown():
测试类运行结束后需要调用的方法；


- 借助MyEclipse可以很方便的搭建一个测试框架。
而且，并没有把测试代码和被测试代码放在一起，因为单元测试代码是不会出现在最终产品中的；
搭建测试框架的操作技巧：
- 在搭建测试框架的时候，建议分别为单元测试代码和被测试代码创建单独的目录，并保证测试代码和被测试代码使用相同的包名。即，两者使用一样的包，不同的目录。
- 这样既保证了代码的分离，同时还保证了查找的方便。

##TestRunner：
- TestRunner类是运行测试代码的运行器。
- JUnit中的所有的测试方法都是由一个叫“Runner测试运行器”的东西负责执行的，JUnit为单元测试提供了默认的一个Runner，所以才能执行测试。
- 测试的结果就是TestResult，我们会发现有两种测试结果：
	- Errors和Failures，  
#### 两种结果的区别：
- Failures是当期望值和断言不匹配时的异常，它表示在测试点发现了问题。 测试失败；
- 而Errors是不曾预料到的代码异常，它是测试目的之外的一个发现。代码本身的错误；
- 换句话说，Errors代表程序本身错误，
Failures代表测试失败；

### 目前常用的JUnit版本是：JUnit3和JUnit4 。
- JUnit的不同版本，使用了不同的Java语言特性来辅助单元测试的进行。

### JUnit3搭建测试框架的特点：
- 第一，测试类继承于TestCase类。
- 第二，所有的测试方法是以test开头的。

#### 测试类的源代码：
```java
public class CalculatorTest extends TestCase {
Calculator calc = new Calculator();

//测试前
protected void setUp() throws Exception {
 //省略代码.....
}

//测试后
protected void trearDown() throws Exception {
   //省略代码.....
}

 //测试加法
public  void testAdd() {
   //省略代码.....
}

//测试减法
public void testSub() {
   //省略代码.....
}

//测试乘法
publlic void testMult() {
  //省略代码.....
}

//测试除法
public void testDiv() {
   //省略代码.....
}
//省略代码.....
}
```

JUnit3之所以拥有这样的特点，是因为它依赖于反射机制。
- 而Junit4则依赖于jdk1.5的一个新特性----注解；
- 使用JUnit4可以大大简化测试的过程。
#### JUnit4中的几种常用的注解：
|标注名称|                        标注描述|
|---|---|
|@Before|用于标注每一个测试方法执行前都要执行的方法|
|@After|用于标注每一个测试方法执行后都要执行的方法|
|@Test|用于标注一个测试方法|
|@Ignore|用于标注暂不参与测试的方法|
|@BeforeClass|标注的方法在整个类的所有测试方法运行之前运行一次|
|@AfterClass| 标注的方法在整个类的所有测试方法运行结束之后运行一次；|

JUnit4测试方法的特点：
必须使用注解@Test

测试方法必须使用public void修饰，并且不能带有任何参数；

#### 忽略测试方法（@Ignore)
```java
@Ignore
public void testMult() {
//省略代码.....
}
```
- 如果你在写程序前已经做了很好的规划，那么哪些方法是什么功能都应该定下来了，即使方法尚未完成，它的具体功能也应该是确定的，但是在测试类中，对于尚未完成的方法测试结果肯定是失败的。为此，对于某些尚未完成，暂不参加此次测试的方法，可以使用@Ignore标注。
- 这样，只是忽略该方法的测试，而不是失败。
- 一旦完成了相应的方法，把@Ignore这个标注去掉，就可以进行正常的测试了。

##### jdk1.5的新特性，叫静态导入。
`import static org.junit.Assert.*;`
- 它的意思是导入Assert类中的所有静态方法。
- 目的就是方便对类方法的调用，这样再调用Assert类中的静态断言方法时，就不用通过Assert.去调用了，比如：
`Assert.assertEquals(3,3);`

- 而直接写你要调用的方法名字就可以了。比如：
`assertEquals(3,3);`
- 测试类中为了保证每个测试都是独立的，相互之间没有任何耦合度，我们在每个测试前对计算结果都进行了一个“复原清零”的操作，比如：
```java
@Before
public void setUp() throws Exception {
  System.out.println("测试前.......");
  calc.clear();
 }
```

#### 固定代码段（Fixture):
##### @Before 
- 在任何一个测试执行前必须执行的代码，就是一个固定代码段：Fixture,
#### @After 也是固定代码段；
- @After代表在任何测试之后都要进行的收尾工作。

#### 另两个Fixture:
##### @BeforeClass
- 代表在所有测试工作之前必须执行的代码；
##### @AfterClass
- 所有测试工作完成以后来执行的代码。

### 阅读资料；

#### 异常测试（expected)
- 异常测试是JUnit4中的最大改进；
- 在JUnit4中现在可以编写抛出异常的代码，并且使用注解来声明该异常是预期的。
- 比如：计数器中的除法测试：
```java
@Test
public void testDiv() {
 calc.add(3);
 calc.div(0);
}

```

`calc.div(0);`的意思是将0作为除数，这个肯定会抛出除数为零的异常：`ArithmeticException` 
这样测试结果显示为`Errors`。

而实际上，`JUnit4@Test`提供了一个非常有用的参数：`expected`,它可以声明测试方法期望抛出指定的异常，将代码修改如下：

```java
@Test (expected = ArithmeticException.class)
public void testDiv() throws ArithmeticException {
  calc.add(3);
  calc.div(0);
}
```

- 这段修改后的代码表示我们期望抛出`Arithmetic`异常，
- 而代码`calc.div(0)`正好抛出这个异常，这和我们的期望一致，因此断言成功；
而测试结果就肯定不再是`Errors`了。
- 反之，`calc.div(1)`;运行测试并没有抛出这个异常，则JUnit会认为这个测试没有通过。
- 这就为验证被测试方法在错误的情况下是否会抛出预定的异常提供了便利。

#### 时间测试（timeOut):
- JUnit@Test的另一个非常有用的参数。
- 用来指定被测试方法被允许运行的最长时间应该是多少。
- 比如：计算器中的开方方法：
```java
//开方 死循环
public void squareRoot(int n) {
for(; ;) {}
}
```

在测试方法中可以限制此方法被允许运行的最长时间。
代码修改如下：
```java
@Test(timeout = 1000)
public void testSquareRoot(int n) {
 //省略代码
 }
```

- timeout的单位为毫秒，这段代码代表：只要测试方法运行时间超过1000毫秒，即1秒，则JUnit就认为测试失败，
- 这个参数对于性能测试有一定的帮助；

#### 测试套件：
测试套件就是把几个测试类打包组成一套数组进行测试。


##### 测试套件遵循以下规则：
- 创建一个空类作为测试套件的入口，保证这个空类使用public修饰，而且存在公开的不带有任何参数的构造函数。

- 使用注解`org.junit.runner.RunWith`和`org.junit.runners.Suite.SuiteClasses`修饰这个空类；

- 将`org.junit.runners.Suite`作为参数传入注解`RunWith`;

- 将需要放入此测试套件的测试类组成数组作为注解SuiteClasses的参数。


## 总结：
### 搭建测试框架：
- 单元测试代码和被测试代码使用一样的包，不同的目录。

### JUnit4常用注解：
```
@Before
@After
@Test
@Ignore
@BeforeClass
@AfterClass
```
### JUnit4测试方法：
1.必须使用注解@Test  
2.测试方法必须使用public void修饰，而且不能带有任何参数。

### 编写测试套件：
1.创建一个空类作为测试套件的入口，保证这个空类使用public修饰，而且存在公开的不带有任何参数的构造函数  
2.使用注解RunWith和SuiteClasses修饰这个空类  
3.将Suite作为参数传入注解RunWith  
4.将需要放入此测试套件的测试类组成数组作为注解SuiteClasses的参数。
