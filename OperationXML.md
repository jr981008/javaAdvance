# 操作XML
RSS是一种描述和同步网站内容的格式，是目前使用最广泛的XML应用。

## 学习方法：
本专题以一个完整的项目贯穿起来，让大家理解操作XML文件相关知识，以及知识点的运用场合。
有关RSS的知识只需了解；  
XML的文件读取，修改等操作需要大量上级练习进行巩固。  
在完成项目的过程中，学会思考问题，解决问题；  
增强程序调试能力和会使用文档帮助也是提高效率的好方法。  

## RSS：
可以把RSS理解为XML格式的摘要，可以是手机新闻的摘要，也可以是博客新闻的摘要。    
重点熟悉必需的频道元素：`title link description pubDate`;

#### 为什么不把要收藏的信息存放在数据库中，而是放在XML文件当中？
数据库可以，但是XML是最合适的。  
这个项目首先是单机运行的，其次存储数据量少，不需要安全级别特别高，所以选择部署起来简单而且消耗资源少的XML更加合理。  
也可以用普通的文本文件，但是它不如XML文件解析起来方便。  
XML不仅可以用来传递数据，还能用来保存数据。  
用XML保存数据，一般只适用于数据量不大和安全级别低的情况。  

### XML的结构设计：
用XML存储数据，要先设计结构。  
手机收藏目录显示为树形结构。  
```xml
<?xml version="1.0" encoding = "utf-8"?>
<PhoneInfo name = "手机品牌">
  <Brand name="华为">
     <Type name="U8650"/>
  </Brand>
  <Brand name = "三星">
      <Type name="i9100G"/>
      <Type name="T9108"/>
   </Brand>
</PhoneInfo>
```
为什么不直接把`<PhoneInfo name = "手机品牌">`显示为
<手机品牌>?  
节点的命名是有限制的，为了避免错误，所以节点名全用英文名；  
是否可以把`  <Type name="U8650"/>`替换为`<Type>U8650</Type>` :  
在获取最新的`RSS`时，会把收藏的手机新闻保存在这个文档中，这样，Type就会有子节点，在这种情况下，使用属性保存型号，会更好。  

## XML解析技术：DOM和SAX
### DOM:
基于XML文档树结构的解析；  
DOM解析XML文档时，会根据读取的文档，构建一个驻留内存的树结构，然后代码就可以使用DOM接口来操作这个树结构，因为整个文档的树结构是驻留在内存中的，所以非常方便于各种操作，它支持删除，修改，重新排列等多种功能。  
DOM解析XML的方式，适用于多次访问的XML文档；  
比较消耗资源；  
### SAX:
基于事件的解析；  
为了解决DOM的资源消耗，不像DOM那样建立一棵完整的文档树，而是通过事件处理器完成对文档的解析；  
SAX解析不用事先调用整个文档，所以优势明显，占用资源少，内存消耗小；  
适用于大数据量的XML文档；  

### DOM：
文档对象模型（Document Object Model）;  
DOM会将XML文件映射为一棵倒挂的树，这棵树中有：元素节点，属性节点，文本节点；  
在这棵树中，每个节点都是以节点对象的形式存在的，通过操作这些对象，就能够完成XML文件的读写任务;  

在DOM解析中，可以根据元素的名称，属性查找节点；  
也可以根据一个节点查找其子节点或父节点的方式来找寻所需要的节点；  
然后对这些节点进行相关的操作；  

用这些的思路操作XML文件，就称之为DOM解析；  

#### XML文件：  
```xml
<?xml version="1.0" encoding="GB2312" ?>
<PhoneInfo>
   <Brand name="华为">
     <Type  name="U8650"/>
     </Brand>
   <Brand name="苹果">
     <Type name="iPhone4"/>
     <Type name="iPhone5"/>
   </Brand>
</PhoneInfo>
```
#### DOM解析：
```java
public class Test {

	public static void main(String[] args)  {
		try {
	 //1,得到DOM解析器的工厂示例
		DocumentBuilderFactory dbf =  DocumentBuilderFactory.newInstance();
	 //2,从DOM工厂获得DOM解析器
		DocumentBuilder db= dbf.newDocumentBuilder();
	 //3,解析XML文档，得到一个Document，即DOM树
		Document doc = db.parse("src/收藏信息.xml");
	 //4,得到所有<Brand>节点列表信息
		NodeList list=doc.getElementsByTagName("Brand");
	 //5,循环Brand信息
		for(int i=0;i<list.getLength();i++){
			Node brandNode = list.item(i);
			Element brandElement = (Element)brandNode;
			String brandName = brandElement.getAttribute("name");
			System.out.println(brandName);
			
			NodeList childList = brandNode.getChildNodes();
			for(int j=0;j<childList.getLength();j++){
			Element typeElement = (Element)childList.item(j);
				
				String typeName = typeElement.getAttribute("name");
				System.out.println("手机："+brandName+typeName);
				
			}
			
		}
		}catch(Exception e){
			System.out.println(e.getMessage());
		}

	}

}

```
#### DOM解析：
```java
//得到DOM解析器的工厂示例；
DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
//从DOM工厂获得DOM解析器
DocumentBuilder db = dbf.newDocumentBuilder();
//解析XML文档，得到一个Document，即DOM树；
Docment doc = db.parse("信息收藏.xml");
//得到所有<Brand>节点列表信息；
NodeList brandList = doc.getElementsByTagName("Brand");
//循环Brand信息
for(int i=0;i<brandList.getLength();i++) {
//获取第i个Brand元素信息
Node brand = brandList.item(i);
//获取第i个Brand元素的name属性的值并输出；
Element element = (Element)brand;
String attrValue = element.getAttribute("name");
//获取第i个Brand元素的所有子元素的name属性值；
NodeList types = element.getChildNodes("name");
for(int j=0;j<types.getLength();j++) {
 //type节点
Element typeElement = ((Element) types.item(j));
//获得手机型号
String type = typeElement.getAttribute("name");
```
#### 使用DOM解析XML文档的步骤主要有：
- 创建解析器工厂对象；
- 由解析器工厂对象创建解析器对象；
- 由解析器对象对指定XML文件进行解析，构建相应DOM树，创建Document对象；
- 以Document对象为起点对DOM树的节点进行增删改查操作；

### Document：
Document是一个接口；提供了对整个XML文档数据的基本访问；

|常用方法 |                           说明|
|---|---|
|getElementsByTagName(String tagName)|按文档顺序返回文档中指定标记名称的所有元素集合；|
|createElement(String tagName)|创建指定标记名称的元素；|

`Node`和`Element`是操作XML的重要接口；  
Node表示文档树中的任意一种类型节点，可以是元素节点，属性节点，文本节点等多种节点，而`Element`则只表示`Node`节点中的元素节点，即`Node`是`Element`的父接口；  
##### Node
|常用方法                       | 说明|
|---|---|
|NodeList getChildNodes()|获取该元素的所有子节点，返回为节点集合；|
##### Element
|常用方法                          | 说明|
|---|---|
|String getTagName()|              元素名称|

### 如何读取节点的文本值：
#### XML文档：
```xml
<? xml version="1.0" encoding="GB2312" ?>
<PhoneInfo>
  <Brand name="华为">
      <Type name="U8650">
         <Item>
             <title>标题信息</title>
             <link>链接</link>
             <description>标题信息</description>
             <putDate>2011-12-12</pubDate>
          </Item>
      </Type>
   </Brand>
</PhoneInfo>
```
#### 读取文本节点：
```java
public class Test {

	public static void main(String[] args) {
		try {
			 //1,得到DOM解析器的工厂示例
				DocumentBuilderFactory dbf =  DocumentBuilderFactory.newInstance();
			 //2,从DOM工厂获得DOM解析器
				DocumentBuilder db= dbf.newDocumentBuilder();
			 //3,解析XML文档，得到一个Document，即DOM树
				Document doc = db.parse("PB_XMLTest1/src/收藏信息.xml");
			//4，读取pubDate
			NodeList list =	doc.getElementsByTagName("pubDate");
		    //4.1 pubDate元素节点
			Element pubDateElement = (Element)list.item(0);
		    //4.2读取文本节点
			String pubDate = pubDateElement.getFirstChild().getNodeValue();
			System.out.println(pubDate);
		}catch(Exception e){
			e.printStackTrace();
		}

	}

}

getNodeValue();
getAttribute();

```
如果要实现添加手机收藏，其实就是在`DOM`树上添加新的节点对象，然后对`DOM`树对应的文档进行保存就可以了；  
首先，根据收藏信息在内存中构造出它的`DOM`树，因为要在`PhoneInfo`节点上添加信息的品牌节点，所以，要先找到`PhoneInfo`节点，然后在本棵树上创建添加新的`Brand`节点，设置它的属性name，然后根据它在`DOM`树的位置，把它加为`PhoneInfo`的子节点；
这样，这个`DOM`树就有了新的结构，后面要做的就是把这个`DOM`存回文件；

##### 添加手机收藏信息：
```java
import java.io.FileOutputStream;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.transform.OutputKeys;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;

import org.w3c.dom.Document;
import org.w3c.dom.Element;

public class Test {
	public static void main(String[] args) {
		try {
		//1,得到DOM解析器的工厂实例
		DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
		//2,从DOM工厂获得DOM解析器
		DocumentBuilder db = dbf.newDocumentBuilder();
		//3,解析XML文档，得到一个Document，即DOM树
		Document doc = db.parse("src/收藏信息.xml");
		//4,创建brand节点
		Element brandElement = doc.createElement("Brand");
		brandElement.setAttribute("name","华为");
		//5,创建Type节点
		Element  typeElement = doc.createElement("Type");
		typeElement.setAttribute("name","U8650");
		//6,创建父子关系
		brandElement.appendChild(typeElement);
		Element PhoneElement =(Element) doc.getElementsByTagName("PhoneInfo").item(0);
		PhoneElement.appendChild(brandElement);
		
		//保存XML文件
		TransformerFactory transformerFactory = TransformerFactory.newInstance();
		Transformer transformer = transformerFactory.newTransformer();
		DOMSource domSource = new DOMSource(doc);
		//设置编码类型
		transformer.setOutputProperty(OutputKeys.ENCODING, "GB2312");
		StreamResult result = new StreamResult(new FileOutputStream("src/收藏信息.xml"));
		//把DOM树转换为XML文件
		transformer.transform(domSource, result);
		
		
		}catch(Exception e){
			e.printStackTrace();
		}
		
	}

}
```
##### 修改手机收藏：
```java
package com.pb.test;

import java.io.FileOutputStream;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.transform.OutputKeys;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;

import org.w3c.dom.Document;
import org.w3c.dom.Element;
import org.w3c.dom.NodeList;

public class Test2 {
	public static void main(String[] args) {
		try {
		//1,得到DOM解析器的工厂实例
		DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
		//2,从DOM工厂获得DOM解析器
		DocumentBuilder db = dbf.newDocumentBuilder();
		//3,解析XML文档，得到一个Document，即DOM树
		Document doc = db.parse("src/收藏信息.xml");
	    //4,找到修改的节点
		NodeList List = doc.getElementsByTagName("Brand");
		for(int i=0;i<List.getLength();i++){
			Element brandElement = (Element)List.item(i);
			String brandName = brandElement.getAttribute("name");
			if(brandName.equals("Apple")){
				//修改属性
				brandElement.setAttribute("name","苹果");
				
				
			}
		}
		
		
		//保存XML文件
		TransformerFactory transformerFactory = TransformerFactory.newInstance();
		Transformer transformer = transformerFactory.newTransformer();
		DOMSource domSource = new DOMSource(doc);
		//设置编码类型
		transformer.setOutputProperty(OutputKeys.ENCODING, "GB2312");
		StreamResult result = new StreamResult(new FileOutputStream("src/收藏信息.xml"));
		//把DOM树转换为XML文件
		transformer.transform(domSource, result);
		
		
		}catch(Exception e){
			e.printStackTrace();
		}
		
	}

}
```
##### 删除手机收藏：
```java
package com.pb.test;

import java.io.FileOutputStream;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.transform.OutputKeys;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;

import org.w3c.dom.Document;
import org.w3c.dom.Element;
import org.w3c.dom.NodeList;

public class Test3 {
	public static void main(String[] args) {
		try {
		//1,得到DOM解析器的工厂实例
		DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
		//2,从DOM工厂获得DOM解析器
		DocumentBuilder db = dbf.newDocumentBuilder();
		//3,解析XML文档，得到一个Document，即DOM树
		Document doc = db.parse("src/收藏信息.xml");
	    //找到删除的节点
		NodeList list = doc.getElementsByTagName("Brand");
		for(int i=0;i<list.getLength();i++){
			Element brandElement = (Element) list.item(i);
			String brandName = brandElement.getAttribute("name");
			if(brandName.equals("联想")){
		    brandElement.getParentNode().removeChild(brandElement);
		    
				
			}
		}
		
		
		
		//保存XML文件
		TransformerFactory transformerFactory = TransformerFactory.newInstance();
		Transformer transformer = transformerFactory.newTransformer();
		DOMSource domSource = new DOMSource(doc);
		//设置编码类型
		transformer.setOutputProperty(OutputKeys.ENCODING, "GB2312");
		StreamResult result = new StreamResult(new FileOutputStream("src/收藏信息.xml"));
		//把DOM树转换为XML文件
		transformer.transform(domSource, result);
		
		
		}catch(Exception e){
			e.printStackTrace();
		}
		
	}

}
```

## 总结：

### RSS标准：
`item title link description pubDate`

### 解析XML两种方式：
DOM和SAX

### DOM解析XML：
- 创建解析器工厂对象；
- 由解析器工厂对象创建解析器对象；
- 由解析器对象对指定的XML文件进行解析，构建相应的DOM树，创建Document对象；
- 以Document对象为起点对DOM树的节点进行增删该查操作；

##### 创建节点：
createElement()
##### 修改节点属性：
setAttribute()
##### 删除节点：
removeChilde()
##### 查找父节点：
getParentNode();


