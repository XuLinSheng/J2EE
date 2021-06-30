# J2EE

J2EE的全称是Java 2 Platform Enterprise Edition，它是由SUN公司领导、各厂家共同制定并得到广泛认可的**工业标准**，或者说，它是在SUN公司领导下，多家公司参与共同制定的企业级**分布式应用程序开发规范**。目前，J2EE是市场上主流的企业级分布式应用平台的**解决方案**。  

## 背景

> Java于1995年由Sun公司推出，当时它的主要用途是制作产生动态网页的Applet。  
> 后来，人们发现Java的“一次开发，多次运行”，纯面向对象的特性，垃圾回收机制和内置安全特别适合于开发企业应用系统。  
> 于是，企业应用开发商纷纷在Java标准版的基础上各自扩展出许多企业应用API，其结果导致基于Java的企业应用呈爆炸式增长。  
> **但是各企业系统API之间又不能相互兼容，破坏了Java的平台独立性。**  
> 鉴于此，Sun公司联合IBM、Oracle、BEA等大型企业应用系统开发商于1999年共同制订了一个基于Java组件技术的企业应用系统开发规范，  
> **该规范定义了一个多层企业信息系统的标准平台，旨在简化和规范企业应用系统的开发和部署**。  
> 这一规范和其定义的平台就构成了J2EE。  
> 它定义了基于组件的方式设计、开发、组装和部署企业应用系统的各个组成部分。  
> 同时，J2EE规范定义了分布式多层应用系统模型、组件重用策略、一体化的安全模型以及灵活的事务控制策略等，使得独立软件提供商（ISV）能够以比以前更快的速度向市场推出适应用户的解决方案。  
> J2EE是一套针对企业级分布式应用的计算环境。  
> 它定义了动态Web页面功能（Servlet和Jsp）、商业组件（EJB）、异步消息传输机制（JMS）、名称和目录定位服务（JNDI）、数据库访问（JDBC）、与子系统的连接器（JCA）和安全服务等。  

## J2ee主要技术规范

1. ***[JDBC（Java Database Connectivity）](https://github.com/XuLinSheng)***   
JDBC API为访问不同的数据库提供了一种统一的途径，像ODBC一样，JDBC对开发者屏蔽了一些细节问题。另外，JDBC对数据库的访问也具有平台无关性。

2. ***[JNDI（Java Name and Directory Interface）](https://github.com/XuLinSheng)***  
JNDI API用于执行名字和目录服务。它提供了一致的模型来存取和操作企业级的资源，如DNS和LDAP、本地文件系统、应用服务器中的对象。

3. ***EJB（Enterprise JavaBean）***  
EJB技术是在Java Bean本地组件技术基础上开发的面向服务器端分布应用的组件技术。EJB是Sun推出的J2EE规范的一部分，自从J2EE推出之后，得到了广泛的发展，已经成为应用服务器端的标准技术。JB提供了一个开发和实施分布式商务逻辑的框架，大大地简化了具有可伸缩性和高度复杂的企业级应用的开发。EJB规范定义了EJB组件如何与EJB容器（container）进行交互。容器负责提供公用服务，如目录服务、事务管理、安全性、资源缓冲池以及容错性等。但EJB并不是实现J2EE的唯一途径。正是由于J2EE的开放性，使得有的厂商能够以一种和EJB平行的方式来达到同样的目的。
EJB基于Java语言，提供了基于Java二进制字节代码的重用方式。EJB技术的推出，使得用Java基于组件技术开发服务器端分布式应用成为可能。从企业应用多层结构的角度来看，EJB是业务逻辑层的中间件技术。与JavaBeans的关键不同是它提供了事务处理的能力。

4. ***JSP（Java Server Pages）***  
JSP页面由HTML代码和嵌入其中的Java代码所组成。服务器在页面被客户端所请求后对页面中的Java代码进行处理，然后将生成的HTML页面返回给客户端的浏览器。

5. ***[Java Servlet](https://github.com/XuLinSheng)***   
Servlet是一种小型的Java程序，它扩展了Web服务器的功能。
作为一种服务器端的应用，和CGI脚本类似，当被请求时开始执行。Servlet提供的功能与JSP类似，但实现方式不同。JSP通常在大量的HTML代码中嵌入少量的Java代码，而servlets全部由Java写成并且生成HTML。

6. ***[RMI/IIOP](https://github.com/XuLinSheng)***  
RMI（Remote Method Invocation，远程方法调用）是Java的分布式对象标准，允许位于不同主机上的Java类之间进行通信。Java RMI是个应用程序编程接口（API），还是个分布对象模型；使用RMI，Java程序员可以像调用本地操作一样进行网络调用，从而很容易地构造分布式系统。IIOP协议本来是CORBA的一种传输协议，和RMI结合在一起，使得整合非Java对象变得更加简单。

7. ***Java IDL/CORBA***  
在Java IDL的支持下，开发人员可以将Java和CORBA集成在一起。他们可以创建Java对象并在CORBAORB中部署，或者创建 Java类作为和其他ORB一起部署的CORBA对象的客户。后者可用于遗留系统的集成。

8. ***[XML（Extensible Markup Language）](https://github.com/XuLinSheng)***   
XML是一种可以用来定义其他标记语言的语言。它被用来在不同的商务过程中共享数据。XML的发展和Java是相互独立的，但是，它和Java具有的相同目标正是平台独立性。Java和XML的组合构成一个完美的具有平台独立性的解决方案。

9. ***[JavaMail](https://github.com/XuLinSheng)***  
JavaMail是用于存取邮件服务器的API，它提供了一套邮件服务器的抽象类。JavaMail同时支持SMTP服务器和IMAP服务器。

10. ***JAF（JavaBeans Activation Framework，JavaBeans 激活框架）***  
JavaMail利用JAF来处理MIME编码的邮件附件。MIME的字节流可以被转换成Java对象，或者转换自Java对象。大多数应用不需要直接使用JAF。

11. ***[JMS（Java Message Service）](https://github.com/XuLinSheng)***  
JMS是用于和面向消息的中间件相互通信的应用程序接口（API）。它既支持点对点的域，又支持发布/订阅（publish/subscribe）类型的域，并且提供对下列类型的支持：经认可的消息传递、事务型消息的传递、一致性消息和具有持久性的订阅者支持。JMS还提供了与遗留后台系统集成的一种方式。

12. ***[JTA（Java Transaction Architecture，Java事务构架）](https://github.com/XuLinSheng)***  
JTA定义了一种标准的API，应用系统由此可以访问各种事务监控。

13. ***JTS（Java Transaction Service，Java事务服务）***  
JTS是CORBAOTS事务监控的基本实现。JTS规定了事务管理器的实现方式。该事务管理器是在高层支持 Java Transaction API（JTA）规范，在系统底层实现OMGOTS规范的Java映像。JTS事务管理器为应用服务器、资源管理器、独立的应用以及通信资源管理器等提供事务服务 。
