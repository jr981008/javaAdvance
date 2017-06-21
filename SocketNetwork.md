# Socket网络编程
## 学习方法：
- 了解`Socket`的概念、起源、分类等相关知识，只需要听懂并看懂课件中的内容即可；
- `Socket`通信原理以及`Socke`t类、`ServerSocket`类的使用是重点内容，结合讲解认真观看操作视频，要能独立完成上机以及课下练习任务，课下查阅JAVA帮助文档；
- 了解`DatagramSocket`类，`DatagramPacket`类的使用，结合操作视频能看懂并完成课下练习任务即可。
- 自己总结本专题中遇到的问题，结合课程中的总结内容以及提供的阅读文档和下载资料，梳理知识点及自己的问题。


## Socket基本概念：
### 网络编程要解决的问题：
如何建立两个节点（电脑）之间的网络连接？


如何向另外一个节点（电脑)发送信息？


如何从外部节点（电脑）接收一个请求并给予响应？

如何利用网络协议（TCP UDP)？


要解决这些问题，可能要对网卡进行编程，也可能需要对网络协议进行编程,对网卡进行编程，需要熟悉网卡的驱动，需要熟悉非常底层的硬件知识；  
对网络协议进行编程，要对网络协议的实现标准有精确的把握；  
可以说，这些方面的编程时非常困难的。    
还好，有`Socket`这么一套网络编程机制，让我们可以比较轻松的应对这些问题。

`Socket`的英文原义是“孔”或者“插座”，中文是“套接字”。  
应用程序通常通过“套接字”向网络发出请求或者应答网络请求。  
它最早出现在UNIX系统中，是UNIX上的一套网络程序通讯的标准；  
这套标准已被广泛移植到其它平台。  

在`Internet`上的注解一般运行了多个服务软件，同时提供了几种服务，每种服务都打开一个`Socket`并绑定到一个端口上，不同的端口对应于不同的服务进程。

`Socket`正如其英文原义“插座”一样，有的插座提供电流服务，有的插座提供电话服务，有的提供有线电视服务。  
客户软件将插头插到不同的插座上，就可以得到不同的服务。

`Socket`实质上提供了！！进程！！通信的端口，网络上的两个程序通过一个双向的通讯链路实现数据的交换，这个双向链路的一端称为一个`Socket`。

`TCP/IP`  5层模型中，`Socket`位于应用层和传输层。  
`OSI`  7层模型中，`Socket`位于会话层和传输层。  
在应用层，可以使用`Socket`进行网络通信的编程任务 。  
`Socket`封装了应用层和传输层的功能，不需要我们自己去实现。  

### Socket分为三种类型：
流式套接字   `SOCK_STREAM`

数据报式套接字`SOCK_DGRAM`

原始式套接字`SOCK_RAW`  
原始式套接字允许对较低层次协议，如：IP协议，直接访问。可以接收本机网卡上的数据帧或数据包，对监听网络流量和分析很有用。   
一般的程序涉及不到原始式套接字；  

#### 流式套接字
SOCK_STREAM  
流式套接字提供了一个面向连接，可靠的数据传输服务，数据无差错、无重复的发生，并且按发送顺序接收。  
内设流量控制，避免数据流超限。  
其实它对应使用的是TCP协议。  
流式套接字就像打电话，他们必须建立一个连接，有人呼叫，有人应答，所有的事情在到达时的顺序与它们出发时的顺序是一样的。  


#### 数据报式套接字
SOCK_DGRAM  
数据报式套接字提供了一个无连接服务。  
数据报以独立包形式被发送，不提供无差错保证，数据可能丢失或重复，并且接收顺序无序。  
其实它对应的是UDP协议。  
数据报式套接字操作，就像一个没有缴纳保价费的邮件投递，没有什么安全保证。而且，多个邮件可能在到达时的顺序与出发时的顺序不一样。
 

### Socket通信原理：
#### 服务器端的步骤如下：
1.建立服务器端的`Socket`，开始侦听整个网络中的连接请求。  
2.当侦听到来自用户端的连接请求时，向客户端发送收到连接请求的信息，并建立与客户端之间的连接。  
3.当完成通信后，服务器关闭与客户端的`Socket`连接。  

#### 客户端的步骤如下：
1.建立客户端的`Socket`，确定要连接的服务器的主机名和端口。  
2.发送连接请求到服务器，并等待服务器的回馈信息。  
3.连接成功后，与服务器进行数据的交互。  
4.数据处理完毕后，关闭自身的`Socket`连接。  

`Socket`的底层机制，相当棘手，但是JAVA平台降低了建立一个`Socket`程序的难度，每一种套接字都被封装到了不同的类当中。  
这些类位于`java.net`包中。
Java平台封装的流式套接字类    
`Socket`类和`ServerSocket`类，基于`TCP`协议的`Socket`编程：

目前较为流行的网络编程模型是：客户机/服务器，即`Client/Server(C/S)`结果，比如：QQ。  
通信双方一方作为服务器，等待客户提出请求并予以响应，而客户端则在需要访服务的时候，向服务器提出申请。  
`Socket`类，就是负责处理**客户端**通信的一个Java类，
在`JDK6.0`中，它一共有9种构造方法，这里只提供两种常用的，其他的，可参照`JDK6.0API`进行查询：
#### 构造方法 
`Socket(String host,int port)`
说明：      
这个构造方法是创建一个流式套接字，并且将其连接到指定主机上的指定端口号。  
#### 构造方法：
`Socket(String host,int port,InetAddress localAddr,int localPort)`
说明：  
这个构造方法也是创建一个套接字，并将其连接到指定远程主机上的指定远程端口。    
#### 新类型：InetAddress:  
这个类型表示的就是互联网协议地址，包含IP地址，`InetAddress`类就是Java对IP地址的一个封装。    
##### Socket类的常用方法：  
|常用方法                            | 说明|
|---|---|
|InetAddress getInetAddress()|返回与当前Socket对象关联的InetAddress对象|
|void shutdownInput()|将此套接字的输入流置于“流的末尾”|
|void shutdownOutput()|禁用此套接字的输出流。|
|InputStream getInputStream()|返回当前Socket对象关联的InputStream对象，它是服务器端向客户端发送回来的数据流|
|OutputStream getOutputStream()|返回当前Socket对象关联的OutputStream对象，它是客户端向服务器端发送的数据流|
|void close()|关闭该Socket对象建立的连接|

##### 处理服务器端通信的ServerSocket类：
在`JDK6.0`中，它有四种构造方法，而我们常用的，也是两种：
|构造方法                    | 说明|
|---|---|
|ServerSocket()  |    创建一个ServerSocket对象。|
|ServerSocket(int port)|创建一个ServerSocket对象，并绑定到指定的端口；|

##### ServerSocket类的常用方法：
|常用方法                   | 说明|
|---|---|
|Socket accept()|侦听并接收到此ServerSocket的连接，此方法在连接传入之前一直阻塞。|
|void close()|使服务器释放占用的资源，并断开所有与客户端的连接。|
|InetAddress getInetAddress()|返回当前服务器绑定的IP地址信息|


### Socket编程步骤：
#### 服务器端：
- 建立一个服务器`Socket`绑定指定端口并开始监听；
- 使用`accept()`方法阻塞等待监听，获得新的连接；
- 建立输入和输出流；
- 在已有的协议上产生会话；
- 使用`close()`关闭流和`Socket`；
#### 客户端：
- 建立客户端`Socket`连接，指定服务器的位置以及端口。
- 得到`Socket`的读写流；
- 利用流按照一定的协议对`Socket`进行读/写操作；
- 使用`close（）`关闭流和`Socket`；


#### 再看Socket通信原理：
在服务器端，以服务器要使用的端口号作为参数来创建一个服务器`Socket`对象，（创建ServerSocket(int port)对象），用来在该端口监听客户请求，（在Socket上监听客户端的连接请求），阻塞、等待连接的建立。  
在客户端，首先创建一个`Socket`对象，（创建Socket(String host,int port)对象）指定服务器的位置以及端口，以此向服务器端发送连接请求，此时服务器正好在阻塞等待连接，这时候两端就可以建立连接了，这时，客户端就可以向服务器发送服务请求了，而此时的服务器看到客户请求到来，则获得并且处理客户请求，并且将处理结果，也就是响应返回给客户端。而客户端则可以通过输入流接收服务器端的响应结果，最后，分别关闭流和`Socket`对象。  

### Socket通信代码：

#### 服务器端代码：
```java
ServerSocket serverSocket = new ServerSocket(8899);
//阻塞等待客户请求
Socket socket = serverSocket.accept();
//由socket对象获得输入流
InputStream is = socket.getInputStream();
BufferedReader br = new BufferedReader(new InputStreamReader(is));
String mess = null;
while(!((mess = br.readLine())==null)) {
System.out.println("客户端发送的请求是： "+mess);
}
//关闭相关资源
is.close();
socket.close();
serverSocekt.close();
```
#### 客户端代码：
```java
//创建客户端Socket对象
Socket socket = new Socket("127.0.0.1",8899);
//由socket对象获得输出流
OutputStream os = socket.getOutputStream();
PrintWriter pw = new PrintWriter(os);
String request = "hello server";
//输出信息到服务器
pw.write(request);
//关闭资源
pw.flush();
pw.close();
socket.close();
```
使用对象序列化流对`Socket`发送和接收的数据进行封装，实现了网络中传输对象。因此，通过`Socket`传递Java对象，采用的方法就是对象序列化；    
在客户端通过`ObjectOutputStream`来写入Java对象，而服务器端则通过`ObjectInputStream`，对以前使用`ObjectOutputStream`写入的对象，进行反序列化来读取或者重构对象。  
#### 唯一需要注意的是：
传递的Java对象需要实现`Serializable`接口。

为了实现在服务器方给多个客户提供服务的功能，可以利用多线程实现多客户的机制。服务器总是在指定的端口上监听是否有客户请求，一旦监听到客户的请求，服务器就会启动一个专门的服务线程来响应该客户的请求，而服务器本身在启动完线程之后马上又进入到了监听状态，等待着下一个客户的到来。

#### 如何在服务器获得每个客户端的IP地址？
- 在`java.net`包中的`InetAddress`类：表示互联网协议地址，包含IP地址。是Java对IP地址的封装。  
- 它可以通过`Socket`的`getInetAddress()`方法获得。
##### java.net.InetAddress类常用方法：
|常用方法                          |说明|
|---|---|
|getHostAddress()| 返回IP地址字符串（以文本表现形式）。|
|getHostName()|获取此IP地址的主机名；|

有关InetAddress类的其他方法，可以查询API。

当数据需要可靠传递时，可以采用基于`TCP`协议的流式套接字，比如：远程登录、文件传输等等。    
### UDP协议：
`UDP`协议不需要像`TCP`协议那样可靠的数据传输，（数据不可靠传输）；   
因此，并不需要对数据内容正确性进行验证；  
付出代价小；效率高。  

对于一些不需要保证严格可靠性传输的场合，就可以`UDP`协议。

#### 基于UDP协议的Socket（数据报式套接字）：
这种套接字就是基于`UDP`协议的（基于UDP协议）  
这种模式下的`Socket`不需要连接一个目的`Socket`（无连接);

它只是简单的投出数据包，无连接的操作，是快速的和高效的，（投出数据包快速高效）；
但是数据安全性不佳，（数据安全性不佳）；  
比如网络游戏，实时性很强，通信及时快速；又比如视频会议，并不要求音频数据绝对正确，只要保证连贯性就可以了；又比如QQ聊天信息；    
其实，这些都是采用基于`UDP`协议的`Socket`通信来实现的。  

##### java.net包同样提供了两个类来支持基于UDP协议的Socket编程，它们分别就是：
- DatagramPacket类以及DatagramSocket类；
- DatagramPacket类表示的是数据报包；
- DatagramPacket对象封装了数据包的数据、数据长度、目标地址以及目标端口；
- DatagramSocket类，是发送和接收数据报包的套接字，它不维护连接状态，也不产生输入输出数据流；
这是和基于`TCP`的`Socket`最大的不同。  
它唯一的作用，就是接收和发送`DatagramPackeet`对象封装的数据报包。

注意：客户端要向外发送数据，必须首先创建一个`DatagramPacket`对象，再使用`DatagramSocket`对象来发送。

#### DatagramPacket类的构造方法：
|构造方法                        | 说明|
|----|---|
|DatagramPacket(byte[] buf,int length,InetAddress address,int port)|构造DatagramPacket对象，用来将长度为length的包发送到指定主机上的指定端口号；|
##### 四个参数：
- 第一个参数是数据的字节数组；
- 第二个参数是字节数组的长度；
- 第三个参数是目标主机的IP地址；
- 第四个参数表示目标主机的端口；

#### DatagramSocket类的构造方法：
在`JDK6.0`当中它有五种构造方法，这里只介绍常用的两种
|构造方法                       | 说明|
|----|---|
|DatagramSocket()|它没有构造参数，表示创建一个DatagramSocket对象，并将其与本地主机上任何可用的端口绑定；|
|DatagramSocket（intport）|包含一个构造参数，表示创建一个DatagramSocket对象，并且将其绑定到本机的指定端口port端口上。|

这两种构造方法的区别就是：一个指定了端口号，一个没有指定端口号；

##### DatagramSocket类的常用方法：
|常用方法                    |  说明|
|---|---|
|void send(DatagramPacket p)|发送指定的数据报|
|void receive(DatagramPacket p)|接收数据报。收到数据以后，存放在指定的DatagramPacket对象中|
|void close()|关闭当前DatagramSocket对象；|


课下阅读资料：  
URL类以及URLConnectoin类；

```java
 /*
    * 服务器端
    */
	public static void main(String[] args) {
		
		try {
			//1,建立一个服务器Socket(ServerSocket)绑定指定端口并开始监听
			ServerSocket serverSocket = new ServerSocket(8800);
			//2,使用accetp()方法阻塞等待监听，获得新的连接
			Socket socket = serverSocket.accept();
			//3,获得输入流
			InputStream is = socket.getInputStream();
			BufferedReader br = new BufferedReader(new InputStreamReader(is));
			//获取输出流
			OutputStream os = socket.getOutputStream();
			PrintWriter pw = new PrintWriter(os);
			//4,读取用户输入信息
			String info = null;
			while(!((info = br.readLine())==null)) {
				System.out.println("我是服务器，用户信息为："+info);
			}
			//给客户一个响应
			String reply = "Welcome!";
			pw.write(reply);
			pw.flush();
			
			//5,关闭资源
			pw.close();
			os.close();
			br.close();
			is.close();
			socket.close();
			serverSocket.close();
		} catch (IOException e) {
			
			e.printStackTrace();
		}
		
		

	}

}
```
```java

package pb.socket.loginStr1;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.PrintWriter;
import java.net.Socket;
import java.net.UnknownHostException;

/*
 * 客户端
 */
public class LoginClient {

	public static void main(String[] args) {
		
		
		try {
			//1,建立客户端Socket连接，指定服务器的位置以及端口
			Socket socket = new Socket("localhost",8800);
			//2,得到Socket的读写流
			OutputStream os = socket.getOutputStream();
			PrintWriter pw = new PrintWriter(os);
			//输入流
			InputStream is = socket.getInputStream();
			BufferedReader br = new BufferedReader(new InputStreamReader(is));
			//3,利用流按照一定的协议对Socket进行读/写操作
			String info = "用户名： Tom；用户密码：123456";
			pw.write(info);
			pw.flush();
			socket.shutdownOutput();
			//接收服务器的响应并打印显示
			String reply = null;
			while(!((reply = br.readLine())==null)) {
				System.out.println("我是客户端，服务器的响应为："+reply);
			}
			//4,关闭资源
			br.close();
			is.close();
			pw.close();
			os.close();
			socket.close();
		} catch (UnknownHostException  e) {
	
			e.printStackTrace();
		} catch (IOException e){
			e.printStackTrace();
		}
		
		

	}

}

```

#### 利用多线程实现多客户机制：
通过在服务器端的死循环让服务器端不断的监听客户端的响应，当有客户端请求服务的时候，服务器端启动一个线程来接收新的客户端的请求
##### 用户类：
```java
import java.io.Serializable;
/*
 * 用户类
 */
public class User  implements Serializable{
	private String loginName; //用户名
	private String pwd; //用户密码
	
	public User() {
		
	}
	
	public User(String loginName,String pwd) {
		super();
		this.loginName = loginName;
		this.pwd = pwd;
	}

	public String getLoginName() {
		return loginName;
	}

	public void setLoginName(String loginName) {
		this.loginName = loginName;
	}

	public String getPwd() {
		return pwd;
	}

	public void setPwd(String pwd) {
		this.pwd = pwd;
	}
	
	
	
	

}
```
##### 线程：
```java
import java.io.IOException;
import java.io.InputStream;
import java.io.ObjectInputStream;
import java.io.OutputStream;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

/*
 * 专门的线程类
 */
public class ServerThread extends Thread   {
	//和本线程相关的Socket
	Socket socket =null;
	
	public ServerThread(Socket socket) {
		this.socket = socket;
	}
	
	//线程启动 :启动客户请求
	public void run()   {
		try {
		//3,获得输入流
		InputStream is = socket.getInputStream();
		//对象序列化
		ObjectInputStream ois = new ObjectInputStream(is);
		//获取输出流
		OutputStream os = socket.getOutputStream();
		PrintWriter pw = new PrintWriter(os);
		//4,读取用户输入信息
		User user = (User)ois.readObject();
		System.out.println("用户名为："+user.getLoginName()+"\n用户密码为："+user.getPwd());
		
		
		//给客户一个响应
		String reply = "Welcome!";
		pw.write(reply);
		pw.flush();
		
		//5,关闭资源
		pw.close();
		os.close();
		ois.close();
		is.close();
		socket.close();
		}catch(IOException e){
			e.printStackTrace();
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} 
		
	} 
	}
	
	
	
	
```


##### 客户端：
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.ObjectOutputStream;
import java.io.OutputStream;
import java.io.PrintWriter;
import java.net.Socket;
import java.net.UnknownHostException;

/*
 * 客户端
 */
public class LoginClient {

	public static void main(String[] args) {
		
		
		try {
			//1,建立客户端Socket连接，指定服务器的位置以及端口
			Socket socket = new Socket("localhost",8800);
			//2,得到Socket的读写流
			OutputStream os = socket.getOutputStream();
			ObjectOutputStream oos = new ObjectOutputStream(os);
			//输入流
			InputStream is = socket.getInputStream();
			BufferedReader br = new BufferedReader(new InputStreamReader(is));
			//3,利用流按照一定的协议对Socket进行读/写操作
			User user = new User();
			user.setLoginName("Tom");
			user.setPwd("12356");
			oos.writeObject(user);
			socket.shutdownOutput();
			//接收服务器的响应并打印显示
			String reply = null;
			while(!((reply = br.readLine())==null)) {
				System.out.println("我是客户端，服务器的响应为："+reply);
			}
			//4,关闭资源
			br.close();
			is.close();
			oos.close();
			os.close();
			socket.close();
		} catch (UnknownHostException  e) {
	
			e.printStackTrace();
		} catch (IOException e){
			e.printStackTrace();
		}
		
		

	}

}
```
##### 服务器端：
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.ObjectInputStream;
import java.io.OutputStream;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class LoginServer {
   /*
    * 服务器端
    */
	public static void main(String[] args) throws ClassNotFoundException {
		
		try {
			//1,建立一个服务器Socket(ServerSocket)绑定指定端口并开始监听
			ServerSocket serverSocket = new ServerSocket(8800);
			//2,使用accetp()方法阻塞等待监听，获得新的连接
			Socket socket = null;
			//客户数量
			int num = 0;
			//一直处于监听状态
			while(true){
				socket = serverSocket.accept();
				ServerThread serverThread = new ServerThread(socket);
				serverThread.start();
				num++;
				System.out.println("客户数量为："+num);
                          
                                //获取IP信息
				InetAddress ia = socket.getInetAddress();
				//客户的IP
				String ip = ia.getHostAddress();
				System.out.println("本客户的IP为："+ip);
				//客户的主机名称
				String hostname = ia.getHostName();
				System.out.println("本客户的主机为："+hostname);
				
			}

		} catch (IOException e) {
			
			e.printStackTrace();
		}
		
		

	}

}
```
#### UDP协议的Socket编程：
##### 服务器端：
```java
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.SocketAddress;
import java.net.SocketException;

public class AskServer {
/*
 * 服务器端
 */
	
	public static void main(String[] args) throws IOException {
	
		try {
         //1,创建接收方（服务器）套接字，并绑定端口号
			DatagramSocket ds = new DatagramSocket(8800);
		//2,确定数据包接收的数据的数组大小
			byte[] buf = new byte[1024];
		//3,创建接收类型的数据包，数据将存储在数组中
		DatagramPacket dp = new DatagramPacket(buf,buf.length);
		//4,通过套接字接收数据
		ds.receive(dp);
		//5,解析发送方发送的数据
		String mess = new String(buf,0,dp.getLength());
		System.out.println("客户端说："+mess);
		//响应客户端
		String reply = "您好，我在的，请咨询！";
		byte[] replys = reply.getBytes();
		//响应地址
		SocketAddress sa = dp.getSocketAddress();
		//数据包
		DatagramPacket dp2 = new DatagramPacket(replys,replys.length,sa);
		//发送
		ds.send(dp2);
		//6,释放资源
		ds.close();
		}catch(SocketException e) {
			e.printStackTrace();
		}
	}

}
```
##### 客户端：
```java
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.net.SocketException;
import java.net.UnknownHostException;

public class AskClient {

	public static void main(String[] args) {
		 //1,确定发送给服务器的信息，服务器地址以及端口
		String mess = "你好，我想咨询一个问题！";
		byte[] buf = mess.getBytes();
		InetAddress ia =null;
		try {
	         ia = InetAddress.getByName("localhost");
		} catch (UnknownHostException e) {
			
			e.printStackTrace();
		}
		int port = 8800;
		
		//2,创建数据包，发送指定长度的信息到指定服务器的指定端口
		DatagramPacket dp = new DatagramPacket(buf,buf.length,ia,port);
		//3,创建DatagramSocket对象
		DatagramSocket ds = null;
		try {
			 ds = new DatagramSocket();
		} catch (SocketException e) {
			
			e.printStackTrace();
		}
		//4,向服务器发送数据包
		try {
			ds.send(dp);
		} catch (IOException e) {
			
			e.printStackTrace();
		}
		//接收服务器的响应并打印
		//2,确定数据包接收的数据的数组大小
		byte[] buf2 = new byte[1024];
	//3,创建接收类型的数据包，数据将存储在数组中
	DatagramPacket dp2 = new DatagramPacket(buf2,buf2.length);
 try {
	 ds.receive(dp2);
 } catch (IOException e) {
	 e.printStackTrace();
 }
          //解析服务器的响应
 String reply = new String(buf2,0,dp2.getLength());
 System.out.println("服务器的响应为："+reply);
           
		//5,释放资源
		ds.close();
	}

}
```


