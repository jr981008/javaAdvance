# XML

## XML的特点：
- XML和操作系统以及编程语言的开发平台没有任何关系。
- XML实现了不同系统之间的数据交互。
## XML的作用：
- XML可以配置应用程序和网站，
- XML可以跨平台进行数据交互，XML可以跨操作系统，也可以跨编程语言的平台。
- XML是Ajax的基石。

`XML(EXtensible Markup Language)`是可扩展标记语言，
提到标记就要追溯到活字印刷书，在后来计算机领域出现之后发展为`GML`就是通用标记语言，然后规范称为`SGML`就是标准通用标记语言。在1998年的时候就出现了XML，另外还有一个分支就是`HTML`，它也是一种标记语言使用的是HTML的语法，网站的网页就是使用HTML语言来编写的。


一个XML文档必须要有第一行的声明和它的文档元素的描述信息。

## XML文档声明：
##### 实例：
`<?xml version="1.0" encoding="UTF-8"?>`
- XML声明一般是XML文档的第一行；
- XML文档声明以"<?"开始，以"?>"结束。
#### XML声明由以下几个部分组成：
- 在前面的是   xml；
- 中间加空格；
- 然后跟上   `version="1.0"`
它是符合文档规范xml1.0版本的，
- 后面有一个` encoding`,
文档字符编码，可以不写，默认为 `"UTF-8"`  
#### 最简化的必须的格式：
`<?xml version="1.0"?>`


### 根元素：
#### 示例：
```xml
<books>
  <book>C语言</book>
  <book>网络编程</book>
</books>
```
在声明的下面，就可以去写根元素了，
为什么称之为根元素，其实`xml`文档最终在内存里面是以树形结构来保存的。
对于根元素，每一个`xml`文档必须有且只能有一个。
像示例当中的`books`就是根元素。这个根元素的写法比较特殊；

对于元素来讲，它分成是开始标签和结束标签。

第一行的`books`就是开始标签，最后一行的`books`就是结束标签。结束标签的前面有一个`"/"`,是写在`"<>"`内部的。  
元素的名称可以随意来定义。  
根元素，是一个完全包含文档当中其他元素的元素。  
对于根元素，它的起始标签要放在其他元素的前面，像books。  
结束标签要放在内部所有元素的最后，也就是</books>,这就是根元素。  


### XML文档的内容：

#### 元素的写法：
```
元素title
<title>XML编程</title>
<title>:开始标签。
XML编程：其中的内容，也就是xml文档里面要携带的数据。
</title>：结束标签。
所有的XML元素都必须有结束标签。
```
在xml文档当中，标签的大小写是有区别的，也就是所谓的大小写敏感。  
示例：
```  
<Title>XML编程</title>
这个xml文档里面的内容是错误的。
<title>XML编程</title>
这个xml文档里面的内容是正确的。
```
XML必须正确地嵌套。   
示例：  
```
<title><name>XML编程</name></title>
```
在有嵌套关系的时候，首先要将内层的元素关闭，也就是先写name的结束标签，然后再写title的结束标签，这才是正确的xml的嵌套。

### 元素的名称需要遵循以下的规则：
在名称当中可以包含字母、数字或者其他的字符。  
在名称当中不能以数字或标点符号开始。  
名称当中不能包含有空格。   


如果命名不规范，将会影响将来的解析。

如果元素当中没有携带数字，也就是没有携带内容，该如何表示：
方法：     
- 在title元素的内容中间加上一个空格。
示例：   
`<title> </title>`
- 没有加入空格，直接写上结束的标签。
示例：  
`<title></title>`
- 在title的后面加了一个`"/"`，直接结束。
示例：  
`<title/>`

建议使用第三种写法；   
第一：它比较简单。第二：它是规范的写法。  

元素携带数据的方式不仅仅是内容还可以是属性。   
属性的语法：    
就是在元素名后面加上属性名和属性值。   

`<元素名 属性名="属性值"/>`
示例：    
```xml
<Student ID="S100">
  <Name>TOM</Name>
</Student>
```
在这个示例中，ID就是属性名，"S100"就是属性值。

注意事项：
属性值用双引号来包裹。

在一个元素里面可以包含多个属性值，属性和属性之间用空格隔开。     
基本格式：   
```
<元素名 属性名="属性值" 属性名="属性值"/>
```
属性值当中不能直接包含 `<  " &`

##### XML中5个预定义实体：
|实体                      | 符号|
|---|---|
|& lt; |                      <|
|& gt;                      | >|
|& amp;                     | &|
|& quot;                     |"|
|& apos;                    | '|

在属性值里面包含特殊字符时，可以使用预定义实体来替换。  
同样在元素内容里面包含这些特殊字符，也是需要用预定义实体来进行替换。  
但是，如果在元素的内容里面包含很多的特殊字符的话，那我们逐个替换就显得非常复杂，在这里，提供一种新的解决思路，就是用`CDATA`节。  
`CDATA`节，注意是将`XML`文档中的一些特殊内容给它转换成为是不需要我们XML文档区解析的内容，也就是，在`CDATA`当中的所有的字符都被当成是元素字符的数据，而不是xml文档里面的标签。  



#####  语法：
```
<![CDATA[
  要显示的字符
]]>
```

在要显示的内容里面，不能够出现`CATAT`节的结束的内容，也就是显示内容里面不能够去写  `]]>` 。

#### CDATA节：
用于把整段文本解释为纯字符数据而不是标签的情况。包含大量 `< > &`或者 `"`字符。 `CDATA`节中的所有字符都会被当作元素字符数据的常量部分，而不是`XML`标签。


#### 注释：
注释一般是在xml文档进行附加的解释；   
##### 语法：
```
<!--注释内容-->
```
注意：   
注释内容中不要出现`--`，可以出现一个`-`；    
不要把注释放在标签的中间；  
注释不能嵌套；  


#### 遵循如下规则的XML文档称为格式正规的XML文档：
- 必须有XML声明语句；
- 必须有且仅有一个根元素；
- 标签的大小写是敏感的，也就是开始标签和结束标签要保持一致；
- 属性值要用双引号括起来；
- 标签要成对出现，当然空标签除外；
- 空标签的关闭是使用`/`的方式来关闭；
- 元素要正确的嵌套；


为什么浏览器和`spy`工具能够检验我们的`xml`文档是否是格式良好的？    
在他们其中已经集成了解析器。    
##### 解析器类型：
解析器分成两类，一类是非验证解析器，另外一类是验证解析器。   
非验证解析器主要是验证`xml`文档是否为格式良好，    
而验证解析器主要是验证`xml`文档是否为有效的。    


`xml`文档主要是在网络上面传输数据用的。   
在两个文档当中都有同名的元素。   
要将这两个文档合并为同一个文件。   
如何来区分两个文档中的同名元素；用 命名空间；   
#### 命名空间：
示例：   
```xml
<cameras xmlns:canon="http://www.canon.com"
xmlns:nikon="http://www.nikon.com">
<canon:camera prodId="P663" name="Camera傻瓜相机/>
<nikon:camera productID="K29B3" name="Camera超级 35 毫米相机"/>
</cameras>
```

xmlns(ns是namespace的缩写）

属性也可以有自己的命名空间，

##### 前缀：
所谓前缀就是在元素的前面加上了一个"名称："，这就是前缀。

属性除非带有前缀，那否则属性是属于它们`元素`所在的命名空间的。   
示例:  
```xml
<batchCompany
xmlns="http://www.Aptech_edu.ac"
xmlns:tea="http://www.tea.org">
<batch-list>
  <batch type="thirdbatch">第三批次</batch>
  <batch tea:type="thirdbatch">第三批茶</batch>
  <batch>午班批次</batch>
 ...
```
1.默认命名空间的定义方法，
`xmlns="http://www.Aptech_edu.ac"`    
它的使用是非常简单的，就是不用加任何前缀，所有不加前缀的元素或属性都是属于这个默认命名空间的；    
2.属性如何加命名空间？   
用法和元素的一样，就是在属性名前面加上前缀名就可以。   
#### 定义命名空间的写法：
在元素的后面加上`xmlns:命名空间的名称`  
后面的一个唯一的地址，使用来区分其他命名空间的地址。  

即便是格式良好的xml文档也是可以随意定义的，   
那如何验证这个xml文档是否符合我们的要求？  
这里就需要DTD技术；   

#### DTD：
文档类型定义 ，英文全名是`Document Type Definition`.

DTD 是用来描述xml文档结构的。  
##### 一个DTD文档包含：
第一：   
元素的定义规则    
所谓的元素定义规则就是我在DTD里面去定义我要验证的xml文档里面能够包含哪些元素；    
这些元素的名是什么，我们都可以定义。     
第二：    
元素之间的关系规则；   
所谓的关系规则就是这个元素的父元素是谁？   
那这两个元素之间到底是上下层的关系还是平行的关系，这也可以表示。   
第三：   
属性的定义规则；   
在DTD里面，我们可以规定最终的xml文档里它的属性名是什么，属性值可以是什么类型。    

这些都是DTD可以做到的事情，所以有了DTD之后，我们的xml文档就可以遵循一定的规则，我们也可以验证这个xml是否符合这个规则了。

##### 为什么要学习DTD？
有了DTD每一个xml文档都可以携带一个自身的格式的描述。

所谓的格式描述就是我的xml文档里面可以写哪些东西，比如：元素，属性。   
有了DTD之后，不同组织的人可以通过一个通用DTD来交换数据。   
写xml文档时，xml文档时可以随意定义的。   
那如果有了DTD，我们可以限制多个公司之间按照这种DTD的规则来编写xml文档。那这个时候，由于xml文档都是统一格式，那所以不同的组织之间，不同的公司之间就可以用这种通用的xml文档格式进行交换数据了，这样就不会乱。   
应用程序可以使用一个标准DTD校验从外表接受的xml数据是否有效。   
应用程序?之间来交换xml数据的时候，必须得规定一条DTD来验证你提交给我的xml文档是否符合要求。   

#### DTD的语法规则：
DTD的整体架构：   
语法：   
DTD文档的声明及引用；  
`内部DTD文档（Students.xml)`  
DTD的定义和我们原来的XML文档，也就是我们想去验证的那个xml文档是在一个文件里头，就是都保存在这个xml文档当中，这个xml文档里面既包含xml定义，又包含DTD的定义。      
语法：在根元素的上面写上：   
```
<!DOCTYPE 根元素 [定义内容]>
```
`外部DTD文档（Students.xml Students.dtd)`   
所谓的外部就是DTD的定义和我们的xml文档是在不同的文件里面；   
可以看到students.dtd就是外部DTD的名字以及它的后缀，这个后缀很简单就叫dtd。   
#### 如何使用外部DTD：
那就需要在前面的xml文档的根元素的上面这个位置跟内部的DTD一样，要写上：语法：   
```
<!DOCTYPE 根元素 SYSTEM"DTD文件路径">
```
内外部DTD文档；   
语法结构：   
```
<!DOCTYPE 根元素 SYSTEM "DTD文件路径"[定义内容]>
```
#### 内部DTD文档的语法结构：   
```xml
<?xml version="1.0"?>
<!DOCTYPE poem [
   <!ELEMENT poem (author,title,content)>
   <!ELEMENT author(#PCDATA)>
   <!ELEMENT title (#PCDATA)>
   <!ELEMENT content (#PCDATA)>
]>
<poem>
  <author>王维</author>
  <title>鹿柴</title>
  <content>空山不见人，但闻人语声。返景入深林，复照青苔上。</content>
</poem>
```
#### 外部DTD文档的语法结构：
xml文档：   
```xml
<?xml version="1.0"?>
<!DOCTYPE poem SYSTEM "poem.dtd">
<poem>
  <author>王维</author>
  <title>鹿柴</title>
  <content>空山不见人，但闻人语声。返景入深林，复照青苔上。</content>
</poem>
```
注释：这时没有写上路径名，这时就要求DTD和xml文档在同一个文件夹下面；这是相对路径；   
#### DTD文档:(这个文档保存在一个文件当中就是poem.dtd)
```
<!ELEMENT poem (author,title,content)>
   <!ELEMENT author(#PCDATA)>
   <!ELEMENT title (#PCDATA)>
   <!ELEMENT content (#PCDATA)>
```
##### 为什么要用外部DTD文档：
因为，内部的DTD，只能验证当前的这个xml文档。  
而需要验证多个xml文档时，只需要一个外部DTD文档；  

#### 内外部DTD：
所谓内外部DTD就是首先在外部定义一个DTD，放在一个文件当中。然后，在xml文档当中首先去使用这个外部DTD来进行验证。后面跟上一个 [, 里面又加上了2个DTD的约束然后是 ]> 结束。这个是内部DTD。
xml文档：   
```xml
<?xml version="1.0"?>
<!DOCTYPE poem SYSTEM "poem.dtd" [
   
   <!ELEMENT title (#PCDATA)>
   <!ELEMENT content (#PCDATA)>
]>
<poem>
  <author>王维</author>
  <title>鹿柴</title>
  <content>空山不见人，但闻人语声。返景入深林，复照青苔上。</content>
</poem>
```
外部DTD文档：
```
<!ELEMENT poem (author,title,content)>
<!ELEMENT author(#PCDATA)>
```
为什么要学习内外部DTD文档的语法结构：    
外部DTD文档对多个xml文档，内部DTD文档是这个xml文档的特殊验证。

#### DTD具体的定义：

元素的定义：   
所谓的元素就是在DTD里面如何限制xml文档的元素该如何编写，简称为元素的定义；

语法：    
```
<!ELEMENT 元素名称  元素类型> 
```
(注意ELEMENT关键字的大小写）   
元素名称是xml文档里面的元素名称；
  
元素类型：   
```
EMPTY
```
该元素不能包含子元素和文本，但可以有属性（空元素）
`#PCDATA`
可以包含任何字符数据，但是不能在其中包含任何子元素；  
纯元素类型   
只包含子元素，并且这些子元素外没有文本；   
`ANY`   
该元素可以包含任何在DTD中定义的元素内容；  


#### EMPTY :
EMPTY是指将来在xml文档里面的元素是不能够有元素内容的。     

写法：    
```
<!ELEMENT 元素名称 EMPTY>
```
示例：    
DTD文档：    
```
<!ELEMENT 人 EMPTY>
```
xml文档1：   
```   
<家庭>
  <人 名字="皮皮鲁" 性别="男" 年龄="6"/>
</家庭>
```
(这个xml文档是正确的）

xml文档2：   
```
<家庭>
  <人>皮皮鲁</人>
  <人><大人>皮皮鲁爸爸</大人></人>
</家庭>
```
（这个xml文档是错误的）


####  #PCDATA ：
PCDATA是指在元素里面可以包含文本，   
我们使用#PCDATA对xml文档实施约束的时候，在元素的里面只能够包含元素的内容，不能包含其他的元素。    
写法：   
```
<!ELEMENT 元素名称 (#PCDATA)>
```
（注意里面有个圆括号，PCDATA是大写的）

示例：   
DTD文档：   
```
<!ELEMENT 人 (#PCDATA)>
```
xml文档1：   
```
<家庭>
 <人 性别="男"  年龄="6">皮皮鲁</人>
</家庭>
```
(这个xml文档是正确的）

xml文档2：   
```
<家庭>
 <人><大人>皮皮鲁</大人></人>
</家庭>
```
（这个xml文档是错误的）

##### 纯元素类型的限制：   
示例：   
DTD文档：   
```
<!ELEMENT 家庭 (人+,家电*)>
```
xml文档：    
```
<家庭>
 <人 名字="郭大路" 性别="男" 年龄="25"/>
 <人 名字="李寻欢" 性别="男" 年龄="38" 爱好="做个教育家和伟人"/>
 <家电 名称="彩电" 数量="3"/>
</家庭>
```
|符号 |            用途 |                  示例|
|---|---|---|
|( ) | 用来给元素分组|      (古龙),(王朔),毛毛|
|丨 | 在列出的对象中选择一个|     (男人丨女人)|
|, |    对象必须按指定的顺序出现  | (西瓜,苹果,香蕉)|
| &#42; |该对象允许出现零次到任意多次 （0到多次） |(爱好&#42;)|
|? |    该对象可以出现，但只能出现一次（0到1次）   |(菜鸟?)|
| + |     该对象最少出现一次，可以出现多次（1或多次）|(成员+)|

注意： `+ * ? `为基数操作符，若没有基数操作符，则表示必须有且仅有一个子元素；  

ANY类型：    
ANY类型比较少用，

示例：   
DTD文档：   
```
<!ELEMENT 人 ANY>
```
这就表示在“人”的下面，可以包含任意的东西。   
所谓的任意就是可以是元素也可以是文本。   
xml文档：   
```
<家庭>
  <人>匹诺曹</人>
  <人><大人>匹诺曹爸爸</大人></人>
</家庭>
```
注意：   
ANY如果放在根元素的话，那么这个xml文档里面出现的内容将不受限制了。   
不建议将ANY写在根元素里面。      
否则，就和没有DTD是一样的。    


xml文档携带数据的方式，不仅仅是xml的元素的内容，还可以是元素的属性。所以说在DTD里面有必要对属性进行限制。

写属性的语法：     
```
<ATTLIST 元素名称
 属性名称  属性类型 属性特点
 .....
>
```
(ATT是attribute的缩写，这里表示属性列表了，就是ATTLIST.)  
为什么要写元素名称？  
因为属性是要定义在元素里边的，    

在语法上，因为在元素里面，可以包含多个属性，所以在写的时候，可以在属性名称下面再去写一行另外一个属性的类型和特点。所以，底下用省略号给它省略掉了。    

#####  属性类型：
CDATA   
表示属性值可以是任何字符，（包括数字和中文）；   
示例：   
```xml
<!ATTLIST  木偶
 姓名 CDATA  #REQUIRED
>

<木偶 姓名="匹诺曹"/>
<木偶 姓名="Pi Luocao"/>
<木偶 姓名="123"/>
```
属性的CDATA与元素的CDATA节有何区别？   
属性的CDATA表示属性值是任何的字符。   
元素里面的CDATA节是表示在CDATA节里面的内容不被xml文档进行解析。也就是不把里面的一些特殊字符当成是一些元素或者是其它的内容。    

##### #PCDATA与CDATA的区别：
- #PCDATA是限制元素里面的内容是字符类型的，而这个CDATA是限制属性里面的内容是字符类型。


#### ID:
ID表示该属性的值必须是唯一的；   
示例：   
```xml
<!ELEMENT 公司职员 ANY>
<!ATTLIST 公司职员
 编号 ID #REQUIRED
 姓名 CDATA #REQUIRED
>

<公司职员 编号="Z001" 姓名="张三"/>
<公司职员 编号="Z002" 姓名="李四"/>
```

#### IDREF和IDREFS :
`IDREF`属性的值指向文档中其他地方声明的ID类型的值。 
`IDREFS`同`IDREF`，但是可以具有由空格分开的多个引用。 
可以这样来理解，ID是数据库里边的主键，而`IDREF`是外键。所以这个外键首先它的前提就是我一定要去引用主表里的主键，在这里ID就表示主键，`IDREF`就是外键。    
 
在属性里边一定要先有ID，然后才能定义`IDREF`或`IDREFS `     
示例：   
```xml
<!ELEMENT 家庭(人+)>
<!ELEMENT 人 EMPTY>
<!ATTLIST 人
   relID ID #REQUIRED
   parentID IDREFS #IMPLIED
   name CDATA #REQUIRED
>

<家庭>
<人 relID="P_1" name="爸爸"/>
<人 relID="P_2" name="妈妈"/>
<人 relID="P_3" parentID="P_1 P_2" name="儿子"/>
</家庭>
```

### 枚举类型：
枚举是指我们事先定义好一些值。属性的值必须在所列出的值的范围内，就可以。
枚举一般是用括号括起来，然后用`|`的符号隔开就可以。  
示例：   
```xml
<!ATTLIST person
婚姻状态 (未婚|结婚|离婚) IMPLIED#>
<!ATTLIST person 性别(男|女) #REQUIRED>
```

#### 属性类型有：
```
CDATA
ID
IDREF IDREFS
Enumerated （用设计好的一些列表来表示）；
```

##### 属性的特点：
```
#REQUIRED
#IMPLIED
#FIXED value
Default value
```

##### #REQUIRED :
表示元素的所有实例都必须有该属性的值（NOT NULL)   
即，元素里面的这些文本，它必须要填写。   
语法：   
```
<!ATTLIST 元素名 属性名 属性类型 #REQUIRED>
```
（注意大小写）


示例：   
```
<!ATTLIST person number CDATA #REQUIRED>
```
要求“person”里边的这个“number”属性首先是CDATA类型；要求这个number必须要填写，就是要写上#REQUIRED.   
```
<person number="5677"/>
```
 number="5677"必须要填写。


##### #IMPLIED :
表示该属性的值是可以被忽略的。  
语法：  
```
<!ATTLIST 元素名 属性名 属性类型 #IMPLIED>
```
示例：   
```
<!ATTLIST contact fax CDATA #IMPLIEC>
```
要求“fax”是CDATA类型，然后是IMPLIED.  
这个时候可以写上“fax”的值也可以不写“fax”的值。  
也就是说这个“fax”属性名还有这个后面的这个值都是可以省略掉的。可以不用再编写；   
```
<contact fax="555-667788"/>
<contact/>
```
##### FIXED :
表示元素中该属性的值必须为指定的固定值。  
这个固定值是之前指定的。   
语法：   
```
<!ATTLIST 元素名 属性名 属性类型 #FIXED "value">
```
(value是指定的固定值）

示例：   
```
<!ATTLIST sender company CDATA #FIXED "Microsoft">

<sender company="Microsoft"/>
```
(company必须等于Microsoft）

为属性提供一个默认值：  
没有固定的英文单词，   
语法：   
```
<!ATTLIST 元素名 属性名 属性类型 "value">
```
（value 是默认值）
示例：   
```
<!ATTLIST payment type CDATA  "check">
```
**注意：这个CDATA跟check之间并没有单词default。**
所以说default不是说固定的关键字，而是指后面所提供的这个值。
示例：   
```
<payment type="check"/>
```
当然如果说是默认值的话，我们不需要写它，默认值就是check，只不过在这里表示出来。   


## 实体：(自定义实体）
这个实体简单理解，就是C#中的常量，我们在DTD里面可以定义实体。然后这个常量是在xml文档中去使用的；   
不是说在DTD里去定义和使用，而是在DTD里面定义，在xml文档里面去使用。  

### 实体语法：
`<!ENTITY 实体名 "实体值">`

示例：   
```
<!ENTITY writer "DonaId Duck.">
<!ENTITY copyright "Copyright W3Schools.">
```
### 实体的使用：
在使用的时候就是： &实体名称;  这样的话就可以使用这个实体了。
示例：   
`<author>&writer;&copyright;</author>`  

根据自己的业务需求来定义实体，这样的话就可以很方便的进行定义并且在xml文档里面任意的去使用。   
将来在修改的时候也非常简单，只需要将实体里的实体名称所对应的实体值改掉。那xml文档里面这些对应的数值都发生了变化。

##### 什么是schema？
`schema`是微软定义的一套用来验证xml文档的技术。它试图代替DTD，但是目前并没有成为w3c组织通用的标准。    
对于`schema`来讲，可以将`schema`比喻成表结构。  
在表结构里，定义一些数据的限制要求；   
然后我们xml文档就相当于是数据表将来要存储的数据，也就是数据库里面的数据表数据了。   
所以整体来讲的话，`schema`就是用来验证xml文档的。

`XML Schema`是用一套预先规定的  XML元素  和 属性 创建的，这些元素和属性定义了XML文档的结构和内容模式；      

`XML Schema`规定XML文档示例的结构和每个元素/属性的数据类型；
XML文档：    
```xml
<书本>
<名称>书剑恩仇录</名称>
<作者>金庸</作者>
</书本>
```
DTD文档：   
```xml
<!ELEMENT 书本 (名称,作者)>
<!ELEMENT 名称 (#PCDATA)>
<!ELEMENT 作者 (#PCDATA)>
```
Schema文档：    
```xml
<element name="书本" type ="书本类型"/>
<complexType name="书本类型">
 <element name="名称" type="string"/>
 <element name="作者" type="string"/>
</complexType>
```
（schema的语法结构非常像xml，其实schema本身就是一个xml文档。这样书写起来就更容易一些。）

为什么要去使用schema来验证xml文档：   
DTD的局限性：  
DTD不遵循XML语法（写XML文档时用一种语法，写DTD时候用另外一种语法）
DTD的数据类型非常有限，它不像数据库的那种结构，可以验证像字符串，整型或其它类型。（与数据库类型不一致）    
DTD不可以扩展，但schema是可以自定义数据类型的。   
DTD不支持命名空间。   

而这些问题在schema里面都能够解决。

##### Schema的新特性：
Schema基于xml语法；   
Schema的数据类型本身有一些是我们常用的，还有一些是可以我们自己去定义的，也就是自己去扩充的。   
即，Schema大大扩充了数据类型，可以自定义数据类型。   
Schema支持属性组。   

示例：     
```xml
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="http://mynamespace/myschema"
elementFormDefaut="unqualified">
  
<!--放入实际内容-->
</xs:schema>
```
（xs:schema：所有Schema文档都使用schema作为其根元素；   
##### xmlns:xs="http://www.w3.org/2001/XMLSchema"  ：   
用于构造`schema`的元素和数据类型来自`http://www.w3.org/2001/XMLSchema`命名空间；   
##### targetNamespace="http://mynamespace/myschema" ：
本`schema`自定义的元素和数据类型属于`http://mynamespace/myschema`命名空间；
##### elementFormDefaut="unqualified"    ：
目标命名空间不一定遵循本Schema（若是qualified则必须遵循）；

schema是一个xml文档。那对于一个格式良好的xml文档，它必须满足哪些要求？   
第一个就是需要有声明，这个上面已经有了    
          `<?xml version="1.0"?>`   
第二个就是它一定要有根元素。对于一个schema文档，它的根元素，就是 ：`xs:schema `    
这里面加上了一个命名空间，  `xmlns:xs`   
后面这些值，包括下面这两个属性值都是将来在编译器里自动生成的。不需要记得这些值，只需要知道它是什么意思就可以了。   
在根元素里面，除了这个命名空间，还有两个属性。   
第一个是 `targetNamespace` ，这个是指将来我要验证的xml文档的命名空间是什么。    
第二个是` elementFormDefaut` ，是指这些元素是否必须要遵循我的命名空间，这里，是指不一定去遵循。   
这个 `targetNamespace` ，另外一种说法就叫“目标命名空间”，
这个东西是用编译器自动生成的；   
我们在使用的时候基本很少修改这个地方。  
所以只需要记得xml文档当中有一个根元素，这个根元素的名称是  ` xs:schema `   就可以了。    




#### Schema的数据类型：
简单类型：   
- 内置的数据类型
	- 基本的数据类型
	- 扩展的数据类型
	
- 用户自定义的简单类型（通过simpleType定义）
- 复合类型（通过complexType定义）

##### schema的基本数据类型：
|数据类型|               描述|
|---|---|
|string   |           表示字符串|
|boolean   |          布尔型|
|decimal    |         代表特定精度的数字|
|float       |        表示单精度32位浮点数|
|double       |       表示双精度64位浮点数|
|duration      |      表示持续时间/日期格式|
|dateTime       |     代表特定的时间|
|time            |    代表特定的时间，但是是每天重复|
|date             |   代表日期|

##### schema的扩展数据类型：
|数据类型                 | 描述|
|----|----|
|ID                |  用于唯一标识元素|
|IDREF               |参考ID类型的元素或属性|
|ENTITY              |实体类型|

long表示整型数，大小介于 -922337203654775808 和922337203654775807之间      
int表示整型数，大小介于 -2147483648和 2147483647之间  
short表示整型数，大小介于 -32768和32767之间；  
byte表示整型数， 大小介于  -128和127之间  


##### schema数据类型的特征：
|特性 |                     描述|
|---|---|
|enumeration|   在指定的数据集中选择，限制用户的选值|
|length      |  指定数据的长度|
|maxExclusive | 指定数据的最大值（小于）|
|maxInclusive | 指定数据的最大值（小于等于）|
|maxLength    | 指定长度的最大值|
|minExclusive | 指定最小值（大于）|
|minInclusive | 指定最小值（大于等于）|
|minLength    | 指定最小长度|

#### schema的元素类型：
根元素：schema    

##### 用于定义元素和属性的元素：   
限制元素，用element ；    
限制属性，用attribute；    
group元素组；    
attributeGroup属性组；     

##### 用于定义简单类型：   
simpleType；     

##### 用于定义复杂类型：
complexType；  

##### 用于进行类型约束：
`choice list sequence restriction`   

其中，`element，attribute，simpleType，complexType`是重点；


##### schema的根元素：
作用：    
包含已经定义的schema。   
包含其他schema元素的元素；   
用法：    
`<xs:schema>`   
属性：  
xmlns ： 命名空间；   
targetNamespace ： 是指xml文档的命名空间，也就是说目标文档的命名空间；   
elementFormDefault : 是指我的目标文档是否一定遵循这个命名空间，这里面可以不遵循；   


这些东西是通过编译器自动生成的。只需要知道它是什么意思就可以了；
```xml
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="http://mynamespace/myschema"
elementFormDefault="unqualified">
.....
</xs:schema>
```

在xml文档当中，元素占到了大量的比例。所以在schema里面，我们要学会如何去限制xml文档里面的元素。  
##### element：    
作用：声明一个元素；   
属性：    
```
name;   
type;   
ref;
minOccurs;
maxOccurs;
```
首先，使用到的关键字是`element`,然后是`name`,这个name是指将来你要限制xml文档的元素的名字。在这里我们可以设置`name=dog`,也就是xml文档里元素名就叫dog。   
后面是元素类型，这个类型是指元素里面它的内容包含的类型，`type="xs:string"` 。   
注意：由于我们使用的是schema里面的类型，所以在string的前面要加上"xs:" 。      
然后是`minOccurs,maxOccurs`,这个是指这个元素在文档里面最小出现次数是0，最大出现次数是3。这里比DTD要更为强大一些，因为在DTD面只能用"*"或"+",而在这里可以限制更精确一些。      
还有ref,比较复杂；   
```
<xs:element name="dog" type="xs:string"
 minOccurs="0"  maxOccurs="3"/>
```
##### group  ：
作用：  
把一组元素声明组合在一起；    
在xml文档里面要求将几个元素捆绑在一起同时出现；   
属性：   
```
name;    
```

示例：      
"xs:group"首先是组的名字，name="bookData",这个name是设置组名的。
然后底下是一个"xs:sequence";用于限制组里面的出现次数的。也就是下面包含3个元素,是："code,title,price",
那么它将来的出现的顺序就是 "code,title,price" 
```xml
<xs:group name="bookData">
   <xs:sequence>
      <xs:element name="code" type="xs:string"/>
      <xs:element name="title" type="xs:string"/>
      <xs:element name="price" type="xs:string"/>
   </xs:sequence>
</xs:group>
```
##### attribute :
作用：  
声明一个属性；  
属性：  
```
name type use default fixed
```
示例：   
```
<xs:attribute name="mybaseattribute"
     type="xs:string" use="required"/>
```
对于属性的写法，采用的是"xs:attribute"后面是"name=" ,这里面设置的是，将来在xml文档里面要出现的属性名称，type是设置属性值的类型，这里是"xs:string"表示字符串类型。还有一个是"use="required""，这就表示本属性为必填项。  
use="option",表示本属性为可选项；   


还有，default是设置默认值，fixed是设置固定值。  
default和fixed是不能同时出现的。   


##### attributeGroup :
作用：  
把一组属性声明组合在一起；  
属性：  
```
name  ref
```
示例：  
name是设置组的名字，在组的名字下面包含了一些属性；   
那将来在使用的时候，可以使用ref来引用这个组就可以。   
```xml
<xs:attributeGroup name="myAttributeGroup">
  <xs:attribute name="someattribute1" type="xs:integer"/>
<xs:attribute name="someattribute2" type="xs:integer"/>
</xs:attributeGroup>

<xs:complexType name="myElementType">
  <xs:attributeGroup ref="myAttributeGroup"/>
</xs:complexType>
```
#### 简单类型simpleType：
作用：  
定义一个简单类型，它决定了元素和属性值的约束和相关信息。  
属性：
```  
name；
```
这个简单类型主要是用在对内置类型进行扩充的场合。  
##### simpleType的常用两种方式：    
restriction：   一个约束；多少到多少之间。   
list：从列表中选择；   


restriction：  
simpleType的子元素为： <xs:restriction>   
定义一个约束条件（重点）；  
示例：   
```xml
<xs:simpletype name="studentAge">
  <xs:restriction base="xs:integer">
   <xs:minInclusive value="18"/>
   <xs:maxInclusive value="45"/>
  </xs:restriction>
</xs:simpleType>
```
restriction是simpleType下面最常用的子元素。   
它是用于定义一个约束条件的，首先simpleType是一个自定义的简单类型。那对于类型来说，肯定要先定义一个名字，这就是第一行里面的     
```
xs:simpletype name="studentAge"
```
这个 studentAge 就是这个简单类型的名称；  
要完成的功能：   
18-45之间的数据类型的一个限制；  
由于这是一个约束，所以选择restriction；    
由于simpleType也就是这个简单类型，它是对内置类型进行扩充的。所以就要先去选择这个内置类型是什么，那后面就有一个  base="xs:integer"    
这里就是要对整型进行扩充，再往里就是设置范围。   
第一个是 minInclusive，这时设置最小值的，后面是value="18"    
第二个是 maxInclusive， value="45",    
这样的话就可以限制18-45之间了。   


#### list :
simpleType的子元素为：<xs:list>   
从一个特定数据类型的集合中选择定义一个简单类型元素；   

示例：   
list主要是定义在一个列表当中每一项的数据类型是什么。   
要在xml文档里面显示一个数组，要求在数组里的每一项都是整型值：   
```xml
<xs:simpleType name="ArrayOfInteger">
  <xs:lsit itemType="xs:integer"/>
</xs:simpleType>
```
在simpleType里面首先要取一个名字，然后在里面定义一个list。每一项的类型就用itemType来设置，使用 xs:integer    

simpleType主要是用来限制包含文本的一些元素。  
因为它是对内置数据类型进行扩充的。    


如果这个元素包含的是其他元素或者说它包含了属性，该如何限制？这个时候就要使用 complexType：    
#### 复合类型complexType：    
作用：   
定义一个复合类型，它决定了一组元素和属性值的约束和相关信息；   
属性：
```   
name；   
```
因为它也是类型，所以也需要定义一个类型的名字；  
常用的子元素：   
```
sequence   一个序列
choice     设置选择项；
```
##### sequence ：
作用：  
给一组**元素**一个特定的序列；  
sequence是指给一组元素去限制一个序列。  
示例：  
```xml
<xs:element name="动物园">
  <xs:complexType>
    <xs:sequence minOccurs="0"                   maxOccurs="unbounded">
       <xs:element name="大象"/>
       <xs:element name="狮子"/>
       <xs:element name="猴子"/>
  </xs:sequence>
 </xs:complexType>
<xs:element>
```
这里并没有名字；   
在这里面定义了3个元素"大象" "狮子" 和"猴子"   
那这时就表示这3个元素出现的顺序一定是 大象 狮子和猴子；   


##### choice ：
作用：  
把一组属性声明组合在一起，以便可以被复合类型应用；  
choice是指在一组元素当中去定义它只能选择这其中的一个。    
属性：      
```
name ref
```
示例：
```xml
<xs:complexType name="chadState">
  <xs:choice minOccurs="1" maxOccurs="1">
    <xs:element ref="selected"/>
    <xs:element ref="unselected"/>
    <xs:element ref="dimpled"/>
    <xs:element ref="perforated"/>
  <xs:choiec。
   
 <xs:attribute name="candidate"                     type="candidateType"/>
<xs:complexType>
```
里面包含了4个元素，这4个元素要求它从其中只能选择一个。   
mixOccurs和maxOccus表示选择项最多和最少只能出现一次。   


complexType和simpleType的区别：     
simpleType类型的元素当中不能包含其它元素或者属性，它只能包含普通的文本，也就是它是对内置的数据类型进行扩充的。    

当需要声明一个**元素的子元素或者属性**的时候，就需要使用complexType了。      
所以complexType针对的是包含元素的元素或者是包含属性的元素，而对文本是没有限制的。   

当需要基于内置的基本数据类型定义一个新的数据类型时，用simpleType；   

## 总结：
XML声明；   
XML文档声明：   
实例：   
`<?xml version="1.0"encoding="UTF-8"?>`   
根元素；  
元素；  
  空元素；  
元素的写法：  
 元素title  
`<title>XML编程</title>`  
属性；  
属性的语法：  
就是在元素名后面加上属性名和属性值。  
`<元素名 属性名="属性值"/>`
实体；  
CDATAT节；  
注释；  
命名空间；    

DTD文档结构：  
内部DTD文档语法结构；  
`<!DOCTYPE 根元素 [定义内容]>`

外部DTD文档语法结构；  
`<!DOCTYPE 根元素 SYSTEM"DTD文件路径">`

内外部DTD文档语法结构；   
语法结构：   
`<!DOCTYPE 根元素 SYSTEM "DTD文件路径"[定义内容]>`

DTD元素：  
元素的定义：  
语法：  
`<!ELEMENT 元素名称  元素类型> `
空元素定义；  

###### #PCDATA;

纯元素；  



写属性的语法：   
```
<ATTLIST 元素名称
 属性名称  属性类型 属性特点
 .....
>
```
DTD属性类型：   
```
CDATA;  

ID;

IDREF  IDREFS

Emunerated
```
属性特点：   
```
#REQUIRED;
#IMPLIED;
#FIXED;
Default;
```
DTD实体；  
Schema数据类型；  


Schema文档结构；  

Schema数据类型；  

Schema常用元素类型；  
element元素；  
group元素；  
attribute元素；  
attributeGroup元素；  

SimpleType元素；  
		restriction和list  

complexType元素；  
		sequence和choice；

