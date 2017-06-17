# 注解
为什么使用注解：  
注解可以提供用来完整地描述程序所需的信息，而这些信息是无法用JAVA来表达的；
所以，注解使得我们能够以将由编译器来测试和验证的格式，存储有关程序的额外信息；
注解还可以用来生成描述符文件，甚至是新的类定义；
并且有助于减轻编写样板代码的负担；
使用注解还可以使代码更加干净易读；
### 注解的产生：
#### 元数据：
元数据是用来描述数据的数据；  
JAVA在JDK5.0中增加了对元数据的支持，即注解；
#### 概念：
- Java注解（Annotation），是Java代码里的特殊标记。它为我们在代码中添加用Java程序无法表达的额外信息提供了一种形式化的方法，使我们可以在未来的某一个时刻方便的使用这些注解修饰的程序元素；  
- 程序元素包括 类、方法、成员变量等；  
- 注解，也就是Java中的元数据，是以标签的形式存在于Java代码中的；注解的存在并不影响程序代码的编译和执行，它只是用来生成其他的文件，或使我们在运行时知道运行代码的描述信息；
#### 注解和注释的不同：
注解和普通的代码注释有一定的区别，也有一定的联系。注解和注释都属于对代码的描述；注释的作用只是简单的描述程序的信息，它不会被程序所读取；而`注解是JAVA代码中的特殊标记，这些标记可以在编译、类加载、运行时别读取，并执行相应的处理`；


注解都继承了java.lang.annotation包下的Annotation接口。  
通过使用注解，程序开发人员可以在不改变原有逻辑的情况下，在源文件中嵌入一些补充的信息，代码分析工具、开发工具和部署工具可以通过这些补充信息进行验证或者进行部署；   
举例：
```java
/**
*这是注释
*/
public static void main(String[] args) {
//本行是注释，下一行是注解
@SuppressWarnings(value="unused")
String name;
}
```
示例中的`@SuppressWarnings`注解，它的作用就是在编译器有警告信息时，通过使用该注解就可以取消指定的警告信息。而使用这个注解，则不会对程序的运行有任何的影响；  
注解，提供了一条为程序元素关联任何元数据的途径。从某些方面来看，注解就像修饰符一样被使用，可用于修饰包、类、构造方法、方法、成员变量、参数以及局部变量的声明等；这些信息被存储在注解的`"name = value"`结构对中；

##### 注解的类型是一种接口；
- 所有的注解都继承了java.lang.annotation包下的Annotation接口。
- 程序可以通过反射来获取指定程序元素的注解对象，
- 注解被用来描述程序元素，如：类、方法、成员变量等，
- 注解能被用来为程序元素（类、方法、成员变量等）设置元数据。值得指出的是，注解不能影响程序代码的执行，无论增加、删除注解，代码都始终如一的执行。
- 如果希望程序中的注解能在运行时起一定的作用，则需要通过反射得到相应的注解，然后再对其进行处理；


##### 使用注解的语法：
- 使用注解时要在其前面加一个“@”符号，同时将注解作为修饰符使用,用于修饰它所支持的程序元素；  
`"@+AnnotationName+(..逗号分隔的多个name = value结构对..)"`  
- 其中`value`必须为编译时常量、内嵌的`Annotation`或数组。如果注解类型定义了某个`NAME`的默认值，则这个结构对参数可以被省略。

##### 不带参数的注解使用语法：
`@Annotation`  
在@符号后面直接加上注解的类型名称Override，  `@Override`  
这样，我们便成功的使用了指定方法重写的注解。  
##### 带一个参数的注解使用语法：
`@Annotation("参数")`
- 示例：  
`@SuppressWarnings(value = "unused")`  
带多个参数的注解使用语法：
`@Annotation({"参数一","参数二",..."参数n"})`  
其中参数为name=value结构对，并且可以按照任何的顺序排列；
- 示例：  
`@MyTag(name = "Jack",age = 20)`

##### 注解语法的规范：
- 将注解置于所有修饰符之前。
- 通常将注解单独放置在一行。
- 默认情况下，注解可用于修饰任何程序元素，包括类、方法、成员变量等。  
- 此外，在使用注解语法时，需要注意：一个程序元素，不能被多个同一个注解的实例同时修饰；

#### 注解分类：

- 内建注解（也称为基本注解），定义于`Java.lang`包下；
- 限定重写父类方法：`@Override`
- 标示已过时：`@Deprecated`
- 抑制编译器警告： `@SuppressWarnings`

源注解`(Meta Annotation)`定义于`java.lang.annotation`包下，这四个源注解都用于修饰其他的注解定义；
- @Retention
- @Target
- @Documented
- @Inherited

##### 自定义注解：
使用`@interface`自定义注解；

在`JDK5.0`的`java.lang`包下提供了三种标准的注解类型，我们称之为内建注解，  
 分别是：  
- 限定重写父类方法：`@Override`  
- 标示已过时：`@Deprecated`  
- 抑制编译器警告： `@SuppressWarnings`  
##### @Override:
- @Override用来指定方法重写；
- @Override被用作标注方法，它说明了被标注的方法重写了父类的方法，起到了断言的作用。
- 它可以强制一个子类必须要重写父类的方法；
- 如果我们对一个没有覆盖父类方法的方法使用`@Override`，那么`JAVA`编译器将以一个编译错误来警告，提示我们此方法没有重写任何方法；
- @Override常常在我们试图覆盖父类方法，却又怕写错父类方法的方法名时发挥作用，

##### 使用@Override：
在要重写父类方法的子类方法前加上`@Override`即可；   
举例：  
```java
public class Fruit {
public void getObjectInfo() {
 System.out.println("水果的getObjectInfo方法");
  }
}

public class Apple extends  Fruit {
//使用@Override指定下面的方法必须重写父类方法
@Override
public void getObjectInfo() {
 System.out.println("苹果重写水果的getObjectInfo方法");
  }
}
```

**注意：@Override只能用于修饰方法，而不能用于修饰其他
程序元素，如：类和成员变量等；**

#### @Deprecated注解：
- 用于表示某个程序元素（类、方法、成员变量等）已过时。
- 如果一个程序元素被`@Deprecated`修饰的话，则表示此程序元素已过时，编译器将不再鼓励使用这个被标注的程序元素，如果在程序中包括子类继续使用这个过时的程序元素的话，那么编译器则会在该程序元素上画一条线，表示此程序元素已过时，建议不要再使用。

**注意：**
- `@Deprecated`与文档注释中的`@deprecated`标记不同；
- `@Deprecated`的作用与文档注释中的`@deprecated`标记的作用基本相同，但他们的用法不相同。
- `@Deprecated`是`JDK5.0`才支持的，可以被编译器所识别，无须放在文档注释语法`（/**...*/)`中，而是直接用于修饰程序中的程序元素，如：类，方法，成员变量等；
- 而文档注释中的`@deprecated`标记是被`JavaDoc`工具所识别的用来生成文档的。
- 在JDK5.0中，Java编译器仍然像从前版本一样寻找文档注释中的`@deprecated`标记，并使用它们产生警告信息，但这种情况将在后续版本中做出改变，我们应从现在开始，使用`@Deprecated`来修饰已过时的方法，而不是使用文档注释中的`@deprecated`标记；
```java
public class Apple extends Fruit {
//使用@Deprecated指定下面的方法已过时
@Deprecated
public void getObjectInfo() {
 System.out.println("苹果重写水果的getObjectInfo方法");
  }

public static void main(String[] args) {
 Apple a = new Apple();
 a.getObjectInfo();
 }
}
```
`(注：在程序中，getObjectInfo上被画上一条直线）`

##### @SuppressWarnings：
- @SuppressWarnings指示被注解标识的程序元素及其子元素取消显示指定的编译器警告。
- @SuppressWarnings被用于有选择的关闭编译器对类、方法以及成员变量等程序元素及其子元素的警告，
- @SuppressWarnings会一直作用于该程序元素的所有子元素，
例如：  
```java
@SuppressWarnings(value = "unchecked")
public class Apple extends Fruit {
 public static void main(String[] args) {
  Apple a = new Apple（）；
 @SuppressWarnings(value = "unused")
 List<Apple> list = new ArrayList();
//   list.add(a);
  }
}

```

使用`@SuppressWarnings(Warning(value = "unchecked")`,来标识Apple类来取消类型检查的编译器警告，同时，又标识该Apple类里的创建List语句取消显示;   
未被使用的编译器警告;那么这条创建List的语句将同时取消显示类型检查和未被使用这样两个编译器警告。

##### 使用@SuppressWarnings：
如果编译器对代码提出警告，那么我们就要检查一下，看看代码是不是真的有错误，如果此代码真的表示有错误，那么我们就要纠正它；  
如果我们有时无法避免编译器提出的警告，此时`@SuppressWarnings`就派上用场了，在程序前增加`@SuppressWarnings(Warning(value = "unchecked")`，这个注解就可以告诉编译器，停止对此处代码的警告。

##### @SuppressWarnings需要一些参数才能发挥作用：
当我们使用`@SuppressWarnings`来关闭编译器警告时，一定需要在括号里使用`name=value`这个结构对，来为该注解类型的成员变量设置值;  
注解后面括号中的`name=value`这个结构对，它是用来为注解类型的成员变量赋值的。

当`@SuppressWarnings`后面的括号中的`value`值为如下参数时，编译器将取消相应的警告：

- deprecation:编译器将取消使用了过时程序元素的警告；
- unchecked：编译器将取消执行了未检查的转换的警告；
- unused：编译器将取消某程序元素未被使用的警告；
- fallthrough:编译器将取消当switch程序块直接通往下一种情况而没有break时的警告；
- path：编译器将取消在类路径、源文件路径等中有不存在的路径时的警告；
- serial：编译器将取消当在可序列化的类上缺少serialVersionUID定义时的警告；
- finally：编译器将取消当有finally子句不能正常完成时的警告；
- all：编译器将取消所有情况的警告；

#### 使用@SuppressWarnings的参数：
- `@SuppressWarnings`注解类型只定义了一个单一的成员变量，所以，只需要一个`name=value`结构对为其赋值就可以了；
- 如果成员变量值是一个数组，则要使用大括号来声明数组值，如：
`@SuppressWarnings（value={"unchecked","fallthrough"});`

- 当注解类型里只有一个`value`成员变量，那么使用该注解时则可以直接在注解后的括号里指定`value`成员变量的值，而无需再使用`name=value`这样的结构对形式，
- 在`@SuppressWarnings`注解类型中只有一个`value`成员变量，所以我们可以把`"value="`省略掉，如：  
`@SuppressWarnings（{"unchecked","fallthrough"});`
- 如果`@SuppressWarnings`所声明的被禁止的警告个数只有一个时，则可不用大括号，如：  
`@SuppressWarnings（"unchecked");`


`JDK5.0`及其后续版本，在`java.lang.annotation`包下提供了四个元注解，它们用来修饰**其他的注解定义**；
#### @Target：
- `@Target`用于指定被其修饰的注解能用于修饰哪些程序元素；
- `@Target`注解类型有唯一的`value`作为成员变量，这个成员变量`value`的类型为`java.lang.annotation.ElementType[]`类型。
- `ElementType`类型是可以被标注的程序元素的枚举类型；
`@Target`的成员变量`value`为如下值时， 
- 则可指定被修饰的注解只能按如下声明进行标注：   
```
ElementType.ANNOTATION_TYPE:则被修饰的注解只能用来修饰注解；     
ElementType.CONSTRUCTOR:被修饰的注解只能修饰构造方法；
ElementType.FIELD:被修饰的注解只能用来修饰成员变量；
ElementType.LOCAL_VARIABE:被修饰的注解只能修饰局部变量；
ElementType.METHOD:被修饰的注解只能修饰方法定义；
ElementType.PACKAFE：被修饰的注解只能修饰包定义；
ElementType.PARAMETER：被修饰的注解可以修饰参数；
ElementType.TYPE:被修饰的注解则可以用来修饰类、接口或枚举定义；
```
#### 使用@Target：

如下代码指定了`@SuppressWarnings`可以修饰的元素，这代码中，我们给`value`成员变量赋值，它的值是一个数组，数组中的内容，分别是`TYPE FIELD METHOD RARAMETER`以及`CANSTRUCTOR`等，通过对`value`赋值，我们指定了`@SuppressWarnings`可以修饰`value`数组中的内容，
```java
@Target(value={TYPE,FIELD,METHOD,PARAMETER,CONSTRUCTOR,LOCAL_VARIABLE})
public @interface SuppressWarnings{}
```
当注解类型里只有一个`value`成员变量，则使用该注解时可以直接在注解后面的括号里指定`value`成员变量的值，而无需使用`name=value`结构对的形式。所以，这段代码也可以简写成`@Target`，然后，后面没有`value=`,而是直接在大括号中写入数组的值，
```java
@Target({TYPE,FIELD,METHOD,PARAMETER,CONSTRUCTOR,LOCAL_VARIABLE})
public @interface SuppressWarnings{}
```
同样，假如只允许`@SuppressWarnings`只能用来修饰类、接口或枚举定义，则可去掉大括号，只是指定一个`value`值。
如`@Target`，然后括号中只有一个`TYPE`,这时，`@Target`就指定了`@SuppressWarnings`只能用来修饰类、接口或枚举定义；
```java
@Target(TYPE)
pulic @interface SuppressWarnings{}
```
#### @Retention:
- @Retention用于指定被修饰的注解可以保留多长时间；
- @Retention描述了被其修饰的注解是否能被编译器丢弃或者保存在`class`文件中。如果保存在`class`文件中，是否在`class`文件被装载时被虚拟机所读取。默认情况下，注解被保存在`class`文件中，但在运行时并不能被反射访问。
- @Retention包含一个`RetentionPolicy`类型的`value`成员变量，使用`@Retention`时必须为该`value`成员变量指定值。
- 通过指定`@Retention`的`value`值，就可以指定被修饰的注解可以保留多长时间。

- @Retention中唯一的value成员变量的取值，来自于java.lang.annotation.RetentionPolicy的枚举类型值，
它只能有如下三个取值，分别是：  
- RetentionPolicy.CLASS(默认值)  
表示编译器会把修饰的注解记录在class文件中，但当Java程序运行时，Java虚拟机将不再保留注解，从而无法通过反射对注解进行访问；

- RetentionPolicy.RUNTIME  
表示编译器将把注解记录在class文件中，当运行Java程序时，Java虚拟机也会保留注解，程序则可以通过反射来获取该注解；

- RetentionPolicy.SOUREC  
则表示编译器将直接丢弃被修饰的注解；

使用@Retention的例子：  
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Retention {
 RetentionPolicy value();
}
```
这是定义`@Retention`注解类型的代码，在代码中，通过将`value`成员变量的值设为`RetentionPolicy.RUNTIME`，指定了`@Retention`在运行时，可以通过反射进行访问.  
从这个例子中可以看到，`@Retention`修饰了自己的注解类型定义，说明注解可以修饰自身的类型定义；
而由于`@SuppressWarnings`的作用是取消指定的编译器警告，所以不需要保存`@SuppressWarnings`。也就是说，我们不需要用反射来获取`@SuppressWarnings`。  
所以，在定义`@SuppressWarnings`注解类型的代码中，通过将`@Retention`的`value`成员变量设为`RetentionPolicy.SOURCE`,从而指定编译器直接丢弃`@SuppressWarnings`，而不在`class`文件中对其进行保存；
```java
@Target({TYPE,FIELD,METHOD,PARAMETER,CONSTRUCTOR,LOCAL_VARIABLE})
@Retention(RetentionPolicy.SOURCE)
public @interface SuppressWarnings{
  String[] value;
}
```
#### @Documented:
- @Documented用于指定被其修饰的注解将被`javadoc`工具提取成文档；
如果定义注解时使用了`@Documented`修饰，则所有使用该注解修饰的程序元素的`API`文档中都将包含该注解说明；  
```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Documented {
}
```
另外，`@Documented`与之前讲的`@Target`以及`@Retention`不同；
`@Document`注解类型没有成员变量；

#### @Target定义：
 在定义@Target的时候，使用了@Documented对其进行修饰。
```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Target {
 ElementType[] value();
}


```
#### 同样，@Retention的定义：
在定义@Retention时同样使用了@Documented对其进行了修饰。
```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Retention {
 RetentionPolicy value();
}
```
#### @SuppressWarnings的定义：
在定义@SuppressWarnings时，使用了@Target以及@Retention对其进行了修饰；
```java
@Target({TYPE,FIELD,METHOD,PARAMETER,CONSTRUCTOR,LOCAL_VARIABLE})
@Retention(RetentionPolicy.SOURCE)
public @interface SuppressWarnings{
  String[] value;
}
```
我们来看`@SuppressWarnings`的部分`API`文档，`@SuppressWarnings`中包含`@Target`以及`@Retention`，而之所以会在这里显示`@Target`以及`@Retention`，就是因为这两个注解是被`@Documented`所修饰的。   
如果去掉定义`@Target`以及`@Retention`时的`@Documented`，则在`@SuppressWarnings`的`API`文档中，将不会再出现没有被`@Documented`所修饰的`@Target`以及`@Retention`，即使在定义`@SuppressWarnings`时使用了`@Target`以及`@Retention`，那么在它的文档中也不会出现这两个注解；

#### @Inherited：
- @Inherited，用于指定被其修饰的注解将具有继承性，如果一个使用了`@Inherited`修饰的注解被用于某个类，则这个注解也将被用于该类的子类。
**注意：**
- 被@Inherited注解所修饰的注解是被标注过的类的子类所继承。类并不从它所实现的接口继承该类型的注解，方法也不能从它所重载的方法中继承这种注解；
##### 值得思考的是：
- 当被`@Inherited`修饰的注的`Retention`是`RetentionPolicy.RUNTIME`时，反射`API`会增强这种继承性。因为如果我们使用`java.lang.reflect`去查询一个`Inherited`类型的注解时，反射将展开代码检查工作：检查类及其父类，直到发现指定的注解被发现，或者到达类继承结果的顶层。
#### @Inherited的具体应用：
```java
@Inherited
public @interface InheriTest{}
//@InheriTest注解将具有继承性；

@InheriTest
public class Base {
}

//Sub类只是继承Base类，并未使用@InheriTest修饰
public class Sub extends Base {
 public static void main(String[] args) {
  //输出Sub是否具有@InheriTest
 System.out.println(Sub.class.isAnnotationPresent(InheriTest.class));
    }
}
```
`运行程序，结果为true；`  

`JAVA`使用 `Annotation`接口来代表程序元素前面的注解，`Annotation`接口是所有注解类型的父接口；  
`java.lang.reflect.AnnotatedElement`指定了程序中可以接受注解的程序元素；  
 除此之外，`JAVA`在`java.lang.reflet`包下新增了`AnnotatedElement`接口，该接口代表程序中可以接受注解的程序元素，该接口有如下几个实现类，分别是：  
- Class：类定义；
- Constructor：构造方法定义；
- Field：类的成员变量定义；
- Method：类的方法定义；
- Package：类的包定义；
`java.lang.reflect`包下主要包含一些实现反射功能的工具类，而`java.lang.reflect`包下的反射`API`也提供了读取运行时注解的支持；  
要把`Retention`注解的`value`成员变量的值设为`RetentionPolicy.RUNTIME`  
当一个注解类型被定义为运行时注解后，该注解才是运行时可见的，当`class`文件被装载时被保存在`class`文件中的注解才会被`JAVA`虚拟机所读取。  
这样才能通过反射读取到注解的信息。  
`java.lang.reflect.AnnotatedElement`接口是所有程序元素的父接口，所以，程序通过反射获得了某个类的`AnnotationedElement`对象，如：**类、方法和成员变量之后**，程序就可以调用该对象的三个方法来访问注解信息了。   
##### 通过AnnotatedElement对象的三个方法来获取注解信息：
- `getAnnotation(Class<T> annotationClass)`
返回该程序元素上存在的、指定类型的注解，如果该类型的注解不存在，则返回NULL;
- `Annotation[] getAnnotations()`
返回该程序元素上存在的所有注解；
- `boolean isAnnotationPresent(Class<?  extends Annotation> annotationClass)`
判断该程序元素上是否包含指定类型的注解，如果存在则返回`TRUE`,否则返回`FALSE`;  
##### 使用AnnotatedElement（类、方法、成员变量）对象的方法：
```java
public class MyAnnotation {
//获取MyAnnotation类的getObjectInfo()方法的所有注解
Annotation[] arr = Class.forName("MyAnnotation").getMethod("getObjectInfo").getAnnotations();
//遍历所有注解
for(Annotation an:arr) {
System.out.println(an);
  }
}
```
- 首先，获得`MyAnnotation`类的`Class`对象，
- 然后，通过对象的`getMethod()`方法来得到`getObjectInfo()`方法的对象，之后，我们再调用它的`getAnnotations()`方法，得到`getObjectInfo()`方法里的所有注解，最后，遍历所有注解，对其进行输出；
在这里有一点需要注意，就是：  
- 获取某个注解里的元数据：
可以将!!!注解强制类型装换!!!成所需的注解类型，然后通过注解对象的抽象方法来访问这些元数据；  
示例：  

##### 先自定义一个运行时注解@AnnotationTest：
```java
@Target({TYPE,FIELD,METHOD,PPARAMETER,CONSTRUCTOR,LOCAL_VARIABLE})
@Retention(RetentionPolicy.RUNTIME)
public @interface AnnotationTest {
//定义两个成员变量name和age 
//用default关键字为两个成员变量赋初始值
String name() default "Jack";
int age() default 20;
 }
```
##### 接下来就来得到修饰getObjectInfo()方法的@AnnotationTest以及它的成员变量：
```java
public static void main(String[] args)throws SecurityException,NoSuchMethodException { 
MyAnnotation ma = new MyAnnotation();
//获取MyAnnotation对象的getObjectInfo()方法所包含的所有注解
Annotation[] arr = ma.getClass().getMethod("getObjectInfo").getAnnoatations();
//遍历每个注解对象
for(Annoatation an:arr) {
 //如果an注解是AnnotationTest类型
if(an instanceof AnnotationTest) {
 System.out.println("an is " + an);
            //将an强制类型转换成AnnotationTest
System.out.println("an.name():"+((AnnotationTest)an).name());
System.out.println("an.age():"+((AnnotationTest)an).age());
        }
   }
}
```
**注意：这里得到的注解都是运行时注解，如果@AnnotationTest注解不是运行时注解，那么运行程序将不会得到它的信息。**
## 总结：
### 内建注解：
- 限制重写父类方法：`@Override`(只能用于方法）
- 标示已过时： `@Deprecated`
- 用于表示某个程序元素（类、方法、成员变量等）已过时
- 抑制编译器警告： `@SuppressWarnings`(可以修饰类、方法、语句)

### 元注解：
- @Target
- @Retention
- @Documented
- @Inherited
### 自定义注解：
- 使用`@interface`关键字；
当一个注解类型被定义为运行时注解后，该注解才是运行时可见的，当`CLASS`文件被装载时被保存在`CLASS`文件中的注解才会被`JAVA`虚拟机所读取；

- 使用`AnnotatedElement`对象的三个方法读取注解信息；

```
getAnnotation(Class<T> annotationClass)

Annotation[] getAnnotations()

boolean isAnnotationPresent(Class<? extends Annotation> annotationClass)
```


