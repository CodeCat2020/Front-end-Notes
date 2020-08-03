#  Java Web开发核心内容

登陆请求背后的逻辑流程 （阿里二面）

1.  什么是Java Web？

> Java Web，是用Java技术来解决相关web互联网领域的技术总和。web包括：web服务器和web客户端两部分。Java在客户端的应用有java applet，不过使用得很少，Java在服务器端的应用非常的丰富，比如Servlet、JSP和第三方框架等等。Java技术对Web领域的发展注入了强大的动力。

2.  Java Web需要学什么？

-   Java 基础；

-   前端（HTML、CSS、JS、jQuery、bootstrap、reactjs）；

-   前后端交互（json）

-   HTTP和web基础（计算机网络、HTTP的报文结构和常见方法、URL的DNS解析）（应用问题：session、cookie）（安全问题：HTTPS协议、token、加密算法）

-   Servlet和jsp（早已过气。框架封装servlet，只需写controller）。现在的Java Web其实就是Spring全家桶+web相关技术。

-   Spring全家桶（Spring、Springmvc和Springboot，分布式服务的Springcloud）

-   数据库（MySQL）

-   Java Web实用工具和技术（Tomcat、Maven、日志组件和单元测试组件、ORM框架）

-   进阶后端技术（缓存、消息队列、分布式服务、负载均衡、反向代理、分布式事务、分布式数据库）

## 前端

### HTML

![](media/image1.png){width="5.124359142607174in" height="2.2913801399825022in"}

1.  什么是HTML？

> Hyper Text Markup Language 超文本标签语言，
>
> HTML：网页的"源码"
>
> 浏览器："解释和执行"HTML源码的工具

2.  HTML文档的基本结构

![](media/image2.png){width="5.3125in" height="3.033238188976378in"}

3.  HTML标签分类

    1.  块级

    2.  行级

4.  四种块状结构

5.  网页布局

-   框架布局

-   表格布局

-   DIV+CSS布局

### CSS

### JavaScript

6.  为什么要学JavaScript

    3.  表单验证－减轻服务器端压力

    4.  页面动态效果

    5.  动态改变页面内容

7.  什么是JavaScript

> ![](media/image3.png){width="3.3958333333333335in" height="1.1553641732283464in"}

8.  ECMAScript

9.  BOM

> 浏览器对象模型
>
> 指当用户打开浏览器时，浏览器中的JavaScript runtime engine将在内存中自动创建一组对象，用于对浏览器及HTML文档对象模型中数据的访问和操作。
>
> ![](media/image4.png){width="4.8848064304461944in" height="2.9683792650918637in"}

10. DOM

> 文档对象模型（Document Object Model，DOM）是一种与浏览器、平台、语言无关的接口。
>
> 当浏览器打开一个网页时，不管是HTML还是XML文档，对于网页中的每一个标记，都在内存中创建一个相应的内存对象。这些对象按照树型结构组织，这就是文档对象模型DOM。
>
> DOM理解为网页的API，它将网页中的元素看作一个个对象，这些对象通过标记的name属性来命名，通过对这些可访问的内存对象进行编程，来实现对网页中元素及其属性的修改，以便动态的修改网页。
>
> ![](media/image5.png){width="5.166020341207349in" height="2.7704866579177603in"}

11. 脚本的基本结构

> ![](media/image6.png){width="3.4583333333333335in" height="1.0408573928258968in"}

12. 脚本执行原理

> ![](media/image7.png){width="4.489022309711286in" height="2.2601345144356957in"}

13. JavaScript的使用方式

    6.  Html页面内嵌JS代码

    7.  外部JS文件

    8.  简短缩写方式

14. JavaScript核心语法

> ![](media/image8.png){width="2.8541666666666665in" height="2.234933289588801in"}

15. 变量的声明和赋值

> Java Script-弱类型语言：变量不需要指定类型，由解释器负责确定类型，存在出错可能性。
>
> 整型和浮点型都被当作浮点型存储。

16. 数据类型

> typeof检测变量的返回值

9.  undefined：变量被声明后，但未被赋值

10. string：用单引号或双引号来声明的字符串

11. boolean：true或false

12. number：整数或浮点数

13. object：javascript中的对象、数组和null

## Web基础

### B/S结构

17. 一般的Web架构是指B/S还是C/S，B/S架构是什么?

> 一般的Web架构是指B/S，即浏览器服务器的形式，是基于特定HTTP通信协议的CS架构，对C/S的一种变化或者改进，开发方式分为前后端分离和不分两种情况。
>
> 前后端分离的SPA接近于CS架构，前后端分离一般通过异步请求处理Ajax和前端路由实现。视图由前端处理，前后端只是JSON数据的交互。
>
> 前后端不分离，路由和业务和视图都是有后端完成。

18. 为什么要学习B/S技术

    14. 静态网页的局限性：无法实现交互功能（搜索、购买、登录等）；无法对静态页面的内容进行实时更新。

    15. 解决方案：使用动态网页。动态网页可以根据不同的输入(或操作)，返回不同的网页。

> 实现动态网页需要B/S技术。

![](media/image9.png){width="4.395833333333333in" height="2.8281430446194227in"}

19. 什么是B/S技术

> B/S结构（浏览器/服务器）：程序完全部署在服务器上，用户通过浏览器访问应用程序，它是基于Internet的产物。

![](media/image10.png){width="3.59375in" height="2.1419706911636047in"}

20. B/S技术的工作原理

> B/S结构中浏览器端与服务器端采用**请求/响应**模式进行交互

![](media/image11.png){width="4.760416666666667in" height="2.21792104111986in"}

21. 如何访问动态网页

> 使用URL实现页面访问

-   URL：Uniform Resource Locator，"统一资源定位符"，网址。

-   URL是唯一能识别Internet上具体的计算机、目录或文件夹位置的命名约定

-   URL的组成

    -   第一部分：协议

    -   第二部分：主机IP地址（有时包含端口号）

    -   第三部分：项目资源的地址，如目录和文件夹名等

![](media/image12.png){width="3.937007874015748in" height="1.1561056430446195in"}

22. 客户端、服务端、HTTP协议的联系

![](media/image13.png){width="4.9472976815398075in" height="1.5518897637795275in"}

### 服务器

23. 总结

+------------------+----------------------------------+-------------------+
| 客户端           | 客户端主机的浏览器               | Applet            |
+------------------+----------------------------------+-------------------+
| Web服务器        | 使用HTTP协议来传输数据           | Apache、Nginx     |
+------------------+----------------------------------+-------------------+
| 轻量级应用服务器 | 具有解释和执行服务器端代码的能力 | IIS、Tomcat       |
+------------------+----------------------------------+-------------------+
| 应用服务器       | 提供客户端应用程序可调用的方法   | WebLogic、JBoss、 |
+------------------+----------------------------------+-------------------+
| Servlet容器      | 运行在Web服务器上的服务端的组件  | Tomcat            |
|                  |                                  |                   |
|                  | 在服务器端使用Java来动态生成网页 |                   |
+------------------+----------------------------------+-------------------+

24. 有了解服务器吗，用的tomcat？其他的了解吗？ （小米一面）

25. 什么是Web服务器？主要有哪些Web服务器？

> Web服务器使用HTTP协议来传输数据。例子：用户在浏览器（客户端）中输入一个URL，然后就能获取网页进行阅览。因此，服务器完成的工作就是发送网页至客户端。传输过程遵循HTTP协议，它指明了请求（request）消息和响应（response）消息的格式。
>
> 最常用的Web服务器是Nginx（也是反向代理服务器）、Apache、Microsoft的Internet信息服务器（Internet Information Services，IIS）。
>
> 微软早期的IIS，就是一个纯粹的Web服务器。后来，它嵌入了ASP引擎，可以解释VBScript和JScript服务器端代码了，这时，它就可以兼作应用服务器。从原理上说，它勉强可以称之为应用服务器。确切地说，它是兼有一点应用服务器功能的Web服务器。

26. WEB服务器的工作原理

> 一般可分成4个步骤：连接过程、请求过程、应答过程以及关闭连接。

16. 连接过程：Web服务器和其浏览器之间所建立起来的一种连接。查看连接过程是否实现，用户可以找到和打开socket这个虚拟文件，这个文件的建立意味着连接过程这一步骤已经成功建立。

17. 请求过程：Web的浏览器运用socket这个文件向其服务器而提出各种请求。

18. 应答过程：运用HTTP协议把在请求过程中所提出来的请求传输到Web的服务器，进而实施任务处理，然后运用HTTP协议把任务处理的结果传输到Web的浏览器，同时在Web的浏览器上面展示上述所请求之界面。

19. 关闭连接：当应答过程完成以后，Web服务器和其浏览器之间断开连接的过程。

> 四个步骤环环相扣、紧密相联，逻辑性比较强，可以支持多个进程、多个线程以及多个进程与多个线程相混合的技术。

27. 什么是应用服务器？ 主要有哪些应用服务器？

> 应用程序服务器是通过很多协议来为应用程序提供(serves)商业逻辑(business logic)。
>
> 应用服务器包括WebLogic，JBoss等。应用服务器一般也支持HTTP协议，因此界限没这么清晰。但是应用服务器的HTTP协议部分仅仅是支持，一般不会做特别优化，所以Tomcat很少直接暴露给外面，而是和Nginx、Apache等配合，只让Tomcat处理JSP和Servlet部分。

28. Web服务器和应用服务器的区别是什么？

    20. 前台接待（web服务器） 与 真正的价值服务者（应用服务器）

    21. Web服务器传送（serves）页面使浏览器可以浏览。应用程序服务器提供的是客户端应用程序可以调用（call）的方法（methods）。

> 确切一点，Web服务器专门处理HTTP请求(request），但是应用程序服务器是通过很多协议来为应用程序提供（serves）商业逻辑（business logic）。

29. Tomcat，Apache，JBoss的区别？ （阿里官方面经）

    1.  Apache是HTTP服务器，Tomcat是Web服务器，JBoss是应用服务器。

    2.  Apache解析静态的Html文件；Tomcat可解析jsp动态页面、也可充当容器。

> Apache和Nginx是纯粹的Web服务器，而IIS和Tomcat因为具有了解释和执行服务器端代码的能力，可以称作为轻量级应用服务器。
>
> 面小易说：对于服务器而言，在面试中可能并不会过多涉及，相对而言，面小易认为像是Liunx、Tomcat这些背后的原理可能更受面试官的青睐。

### Applet

30. 什么是Applet？

> java applet是能够被包含在HTML页面中并且能被启用了java的客户端浏览器执行的程序。Applet主要用来创建动态交互的web应用程序。

31. 解释一下Applet的生命周期

<!-- -->

1)  Init：每次被载入的时候都会被初始化。

2)  Start：开始执行applet。

3)  Stop：结束执行applet。

4)  Destroy：卸载applet之前，做最后的清理工作。

<!-- -->

32. 当applet被载入的时候会发生什么？

> 首先，创建applet控制类的实例，然后初始化applet，最后开始运行。

33. Applet和普通的Java应用程序有什么区别？

> applet是运行在启用了java的浏览器中，Java应用程序是可以在浏览器之外运行的独立的Java程序。但是，它们都需要有Java虚拟机。
>
> 进一步来说，Java应用程序需要一个有特定方法签名的main函数来开始执行。Java applet不需要这样的函数来开始执行。
>
> 最后，Java applet一般会使用很严格的安全策略，Java应用一般使用比较宽松的安全策略。

34. Java applet有哪些限制条件？

主要是由于安全的原因，给applet施加了以下的限制：

1)  applet不能够载入类库或者定义本地方法。

2)  applet不能在宿主机上读写文件。

3)  applet不能读取特定的系统属性。

4)  applet不能发起网络连接，除非是跟宿主机。

5)  applet不能够开启宿主机上其他任何的程序。

<!-- -->

35. 什么是不受信任的applet？

> 不受信任的applet是不能访问或是执行本地系统文件的Java applet，默认情况下，所有下载的applet都是不受信任的。

36. 从网络上加载的applet和从本地文件系统加载的applet有什么区别？

> 当applet是从网络上加载的时候，applet是由applet类加载器载入的，它受applet安全管理器的限制。

当applet是从客户端的本地磁盘载入的时候，applet是由文件系统加载器载入的。

> 从文件系统载入的applet允许在客户端读文件，写文件，加载类库，并且也允许执行其他程序，但是，却通不过字节码校验。

37. applet类加载器是什么？它会做哪些工作？

> 当applet是从网络上加载的时候，它是由applet类加载器载入的。类加载器有自己的java名称空间等级结构。类加载器会保证来自文件系统的类有唯一的名称空间，来自网络资源的类有唯一的名称空间。
>
> 当浏览器通过网络载入applet的时候，applet的类被放置于和applet的源相关联的私有的名称空间中。然后，那些被类加载器载入进来的类都是通过了验证器验证的。验证器会检查类文件格式是否遵守Java语言规范，确保不会出现堆栈溢出(stack overflow)或者下溢(underflow)，传递给字节码指令的参数是正确的。

38. applet安全管理器是什么？它会做哪些工作？

> applet安全管理器是给applet施加限制条件的一种机制。浏览器可以只有一个安全管理器。安全管理器在启动的时候被创建，之后不能被替换覆盖或者是扩展。

### Servlet

39. 什么是Servlet？

> Servlet是用来处理客户端请求并产生动态网页内容的Java类。Servlet主要是用来处理或者是存储HTML表单提交的数据，产生动态内容，在无状态的HTTP协议下管理状态信息。

![](media/image14.png){width="3.3225010936132984in" height="2.124734251968504in"}

> 在Java Web程序中，Servlet主要负责接收用户请求 HttpServletRequest，在doGet()、doPost()中做相应的处理，并将回应HttpServletResponse反馈给用户。Servlet 可以设置初始化参数，供Servlet内部使用。一个Servlet类只会有一个实例，在它初始化时调用init()方法，销毁时调用destroy()方法\*\*。\*\*Servlet需要在web.xml中配置（MyEclipse中创建Servlet会自动配置），**一个Servlet可以设置多个URL访问。Servlet不是线程安全**，因此要谨慎使用类变量。

40. 为什么要用Servlet？

> 动态网页。处理浏览器带来HTTP请求，并返回一个响应给浏览器，从而实现浏览器和服务器的交互。

41. 说一下Servlet的体系结构。

> 所有的Servlet都必须要实现的核心的接口是javax.servlet.Servlet。每一个Servlet都必须要直接或者是间接实现这个接口，或者是继承javax.servlet.GenericServlet或者javax.servlet.http.HTTPServlet。最后，Servlet使用多线程可以并行的为多个请求服务。

42. Applet和Servlet有什么区别？

> Applet是运行在客户端主机的浏览器上的客户端Java程序。而Servlet是运行在web服务器上的服务端的组件。applet可以使用用户界面类，而Servlet没有用户界面，相反，Servlet是等待客户端的HTTP请求，然后为请求产生响应。

43. JSP 和 servlet 有什么区别？各自特点是什么？ （考）

> 总的可以理解为：jsp就是在html里面写java代码，servlet就是在java里面写html代码；其实jsp经过容器解释之后就是servlet。具体不同描述如下：

jsp和servlet的不同之处

-   Servlet在Java代码中通过HttpServletResponse对象动态输出HTML内容

-   JSP在静态HTML内容中嵌入Java代码，Java代码被动态执行后生成HTML内

jsp和servlet各自的特点

-   Servlet能够很好地组织业务逻辑代码，但是在Java源文件中通过字符串拼接的方式生成动态HTML内容会导致代码维护困难、可读性差

-   JSP虽然规避了Servlet在生成HTML内容方面的劣势，但是在HTML中混入大量、复杂的业务逻辑同样也是不可取的

![](media/image15.png){width="5.260416666666667in" height="2.086777121609799in"}

44. JSP和Servlet是什么关系

> 其实这个问题在上面已经阐述过了，Servlet是一个特殊的Java程序，它运行于服务器的JVM中，能够依靠服务器的支持向浏览器提供显示内容。JSP本质上是Servlet的一种简易形式，JSP会被服务器处理成一个类似于Servlet的Java程序，可以简化页面内容的生成。Servlet和JSP最主要的不同点在于，Servlet的应用逻辑是在Java文件中，并且完全从表示层中的HTML分离开来。而JSP的情况是Java和HTML可以组合成一个扩展名为.jsp的文件。有人说，Servlet就是在Java中写HTML，而JSP就是在HTML中写Java代码，当然这个说法是很片面且不够准确的。JSP侧重于视图，Servlet更侧重于控制逻辑，在MVC架构模式中，JSP适合充当视图（view）而Servlet适合充当控制器（controller）。

45. GenericServlet和HttpServlet有什么区别？

> GenericServlet类实现了Servlet和ServletConfig接口。实现了除了service()之外的其他方法，在创建Servlet对象时，可以继承GenericServlet类来简化程序的代码，但需要实现service()方法。
>
> HttpServlet类继承了GeneriServlet类，为实际开发中大多数用Servlet处理 HTTP请求的应用灵活的方法。

46. 阐述Servlet和CGI的区别?

CGI的不足之处:

> 1，需要为每个请求启动一个操作CGI程序的系统进程。如果请求频繁，这将会带来很大的开销。
>
> 2，需要为每个请求加载和运行一个CGI程序，这将带来很大的开销
>
> 3，需要重复编写处理网络协议的代码以及编码，这些工作都是非常耗时的。
>
> Servlet的优点:
>
> 1，只需要启动一个操作系统进程以及加载一个JVM，大大降低了系统的开销
>
> 2，如果多个请求需要做同样处理的时候，这时候只需要加载一个类，这也大大降低了开销
>
> 3，所有动态加载的类可以实现对网络协议以及请求解码的共享，大大降低了工作量。
>
> 4，Servlet能直接和Web服务器交互，而普通的CGI程序不能。Servlet还能在各个程序之间共享数据，使数据库连接池之类的功能很容易实现。
>
> 补充：Sun Microsystems公司在1996年发布Servlet技术就是为了和CGI进行竞争，Servlet是一个特殊的Java程序，一个基于Java的Web应用通常包含一个或多个Servlet类。Servlet不能够自行创建并执行，它是在Servlet容器中运行的，容器将用户的请求传递给Servlet程序，并将Servlet的响应回传给用户。通常一个Servlet会关联一个或多个JSP页面。以前CGI经常因为性能开销上的问题被诟病，然而Fast CGI早就已经解决了CGI效率上的问题，所以面试的时候大可不必信口开河的诟病CGI，事实上有很多你熟悉的网站都使用了CGI技术。
>
> 参考：《javaweb整合开发王者归来》P7

47. Servlet接口中有哪些方法及Servlet生命周期探秘

Servlet接口定义了5个方法，其中前三个方法与Servlet生命周期相关：

void init(ServletConfig config) throws ServletException

> void service(ServletRequest req, ServletResponse resp) throws ServletException, java.io.IOException

void destroy()

java.lang.String getServletInfo()

ServletConfig getServletConfig()

> 生命周期： Web容器加载Servlet并将其实例化后，Servlet生命周期开始，容器运行其init()方法进行Servlet的初始化；请求到达时调用Servlet的service()方法，service()方法会根据需要调用与请求对应的doGet或doPost等方法；当服务器关闭或项目被卸载时服务器会将Servlet实例销毁，此时会调用Servlet的destroy()方法。init方法和destroy方法只会执行一次，service方法客户端每次请求Servlet都会执行。Servlet中有时会用到一些需要初始化与销毁的资源，因此可以把初始化资源的代码放入init方法中，销毁资源的代码放入destroy方法中，这样就不需要每次处理客户端的请求都要初始化与销毁资源。

参考：《javaweb整合开发王者归来》P81

48. Servlet与线程安全

> Servlet不是线程安全的，多线程并发的读写会导致数据不同步的问题。 解决的办法是尽量不要定义name属性，而是要把name变量分别定义在doGet()和doPost()方法内。虽然使用synchronized(name){}语句块可以解决问题，但是会造成线程的等待，不是很科学的办法。 注意：多线程的并发的读写Servlet类属性会导致数据不同步。但是如果只是并发地读取属性而不写入，则不存在数据不同步的问题。因此Servlet里的只读属性最好定义为final类型的。

参考：《javaweb整合开发王者归来》P92

#### 生命周期

49. Servlet的生命周期 （阿里官方面经）

> 对每一个客户端的请求，Servlet引擎载入Servlet，调用它的init()方法，完成Servlet的初始化。然后，Servlet对象通过为每一个请求单独调用service()方法来处理所有随后来自客户端的请求，最后，调用Servlet的destroy()方法把Servlet删除掉。其中的3个方法说明了Servlet的生命周期：

-   init()：负责初始化Servlet对象。

-   service()：负责响应客户端请求。

-   destroy()：当Servlet对象推出时，负责释放占用资源。

> 大致分为4部：Servlet类加载--\>实例化--\>服务--\>销毁。Tomcat中Servlet的时序图如下：

![](media/image16.jpg){width="6.385416666666667in" height="3.3428947944006997in"}

![](media/image17.png){width="5.65625in" height="3.2321423884514435in"}

1)  HTTP请求：Web Client向Servlet容器(Tomcat)发出HTTP请求。

2)  解析请求：[Servlet容器]{.underline}接收Client端的请求。

3)  创建实例：[Servlet容器]{.underline}创建一个HttpRequest对象，将Client的请求信息封装到对象中。

4)  初始化对象：Servlet（容器（？））创建一个HttpResponse对象。

5)  Servlet调用HttpServlet对象的service方法，把HttpRequest对象和HttpResponse对象作为参数传递给HttpServlet对象中。

6)  HttpServlet调用HttpRequest对象的方法，获取Http请求，并进行相应处理。

7)  处理完成HttpServlet调用HttpResponse对象的方法，返回响应数据。

8)  Servlet容器把HttpServlet的响应结果传回客户端。

<!-- -->

50. doGet()方法和doPost()方法有什么区别？

> doGet：GET方法会把名值对追加在请求的URL后面。因为URL对字符数目有限制，进而限制了用在客户端请求的参数值的数目。并且请求中的参数值是可见的，因此，敏感信息不能用这种方式传递。
>
> doPOST：POST方法通过把请求参数值放在请求体中来克服GET方法的限制，因此，可以发送的参数的数目是没有限制的。最后，通过POST请求传递的敏感信息对外部客户端是不可见的。

51. 什么情况下调用doGet()和doPost()

Form标签里的method的属性为get时调用doGet()，为post时调用doPost()。

#### Servlet 容器

52. 什么是Servlet容器？

> Servlet容器的基本思想是在服务器端使用Java来动态生成网页。因此，Servlet容器是Web服务器和servlet进行交互的必不可少的组件。

![](media/image18.png){width="5.009790026246719in" height="1.5831353893263342in"}

53. Servlet容器有哪些？

### Tomcat 服务器

54. Tomcat服务器介绍

> Apache Jakarta的开源项目，JSP/Servlet容器，中小型应用服务器。
>
> 早期的Tomcat是一个嵌入Apache内的JSP/Servlet解释引擎，Apache+Tomcat就相当于IIS+ASP（动态服务器页面）。后来的Tomcat已不再嵌入Apache内，Tomcat进程独立于Apache进程运行。 而且，Tomcat已经是一个独立的Servlet和JSP容器，业务逻辑层代码和界面交互层代码可以分离了。因此，有人把Tomcat叫做轻量级应用服务器。

a.  启动和停止Tomcat服务器

> 启动：进入TomCat根目录下的bin目录，双击startup.bat文件
>
> 停止：关闭弹出的命令行窗口

b.  Tomcat服务启动检测

> 在IE地址栏中输入：http://localhost:端口号，页面进入到Tomcat启动成功界面
>
> 问题：tomcat8双击startup.bat直接闪退怎么办？如果是windows系统，按Ctrl+R，在弹出的"运行"对话框中输入cmd打开命令行窗口，通过cd命令进入startup.bat所在的目录，然后执行startup.bat 。

55. Tomcat服务器的目录结构

![](media/image19.png){width="4.614583333333333in" height="2.2729822834645668in"}

56. Tomcat工作原理

> ![](media/image20.png){width="4.020330271216098in" height="3.1662707786526685in"}

1)  Connector组件：接收客户端连接；加工处理客户端请求。

2)  Container组件：所有的子容器的父接口；责任链设计模式。

> ![](media/image21.png){width="3.1875in" height="2.18619094488189in"}

Server处理HTTP请求：

![](media/image22.png){width="4.072407042869641in" height="2.791317804024497in"}

57. Tomcat的端口配置

> 通过配置文件修改Tomcat端口号

-   Tomcat端口号默认使用的是8080端口

-   可以通过server.xml文件修改Tomcat的端口号

> ![](media/image23.png){width="5.15625in" height="2.265224190726159in"}

#### 单点登录

58. 单点登录是什么？

> 单点登录( Single Sign On，SSO) ，是目前比较流行的企业业务整合的解决方案之一。
>
> SSO：在多个应用系统中，用户只需要登录一次就可以访问所有相互信任的应用系统。

59. CAS

> 开源的企业级单点登录解决方案。包含CAS Server和CAS Client。
>
> ![](media/image24.png){width="4.666083770778653in" height="2.5725951443569555in"}

60. 单点登录原理

> ![](media/image25.png){width="4.22863845144357in" height="2.4580260279965005in"}

61. 

### Web项目的目录结构

62. Web项目的目录结构

  **目录**           **说明**
------------------ -----------------------------------------------------------------------------------------------
  /                  Web应用的根目录，该目录下所有文件在客户湍都可以访问，包括JSP、HTML，JPG等访问资源
  /WEB-INF           存放应用使用的各种资源，该目录及其子目录对客户端都是不可以访问，其中包括web. xml (部署表述符)
  /WEB-INF/classes   存放Web项目的所有的class文件
  /WEB-INF/lib       存放Web应用使用的JAR文件

63. 配置Web应用

> 使用web.xml文件配置应用发布

-   web.xml文件必须保存在/WEB-INF目录下

-   在 web.xml文件中配置各种资源的发布信息

![](media/image26.png){width="4.71875in" height="1.6497889326334207in"}

64. 配置访问页面

> 通过配置文件修改访问起始页
>
> 通过web.xml文件修改访问的起始页面

![](media/image27.png){width="5.759027777777778in" height="2.797518591426072in"}

65. 部署应用

> 部署的步骤

-   创建应用页面

-   在Tomcat目录的webapps目录下创建应用文件目录

-   将创建的页面复制到应用目录下

-   启动Tomcat服务

-   在IE地址栏中进行访问

![](media/image28.png){width="4.135416666666667in" height="2.968825459317585in"}

## JSP（了解）

1.  什么是JSP页面？

> JSP页面是一种包含了静态数据和JSP元素两种类型的文本的文本文档。静态数据可以用任何基于文本的格式来表示，比如：HTML或者XML。JSP是一种混合了静态内容和动态产生的内容的技术。这里看下JSP的例子。

2.  JSP请求是如何被处理的？

> 浏览器首先要请求一个以.jsp扩展名结尾的页面，发起JSP请求，然后，Web服务器读取这个请求，使用JSP编译器把JSP页面转化成一个Servlet类。需要注意的是，只有当第一次请求页面或者是JSP文件发生改变的时候JSP文件才会被编译，然后服务器调用servlet类，处理浏览器的请求。一旦请求执行结束，servlet会把响应发送给客户端。这里看下如何在JSP中获取请求参数。

3.  JSP有什么优点？

下面列出了使用JSP的优点：

JSP页面是被动态编译成Servlet的，因此，开发者可以很容易的更新展现代码。

JSP页面可以被预编译。

JSP页面可以很容易的和静态模板结合，包括：HTML或者XML，也可以很容易的和产生动态内容的代码结合起来。

开发者可以提供让页面设计者以类XML格式来访问的自定义的JSP标签库。

开发者可以在组件层做逻辑上的改变，而不需要编辑单独使用了应用层逻辑的页面。

4.  什么是JSP指令(Directive)？JSP中有哪些不同类型的指令？

> Directive是当JSP页面被编译成Servlet的时候，JSP引擎要处理的指令。Directive用来设置页面级别的指令，从外部文件插入数据，指定自定义的标签库。Directive是定义在 \<%@ 和 %\>之间的。下面列出了不同类型的Directive：
>
> 包含指令(Include directive)：用来包含文件和合并文件内容到当前的页面。
>
> 页面指令(Page directive)：用来定义JSP页面中特定的属性，比如错误页面和缓冲区。
>
> Taglib指令： 用来声明页面中使用的自定义的标签库。

5.  什么是JSP动作(JSP action)？

> JSP动作以XML语法的结构来控制Servlet引擎的行为。当JSP页面被请求的时候，JSP动作会被执行。它们可以被动态的插入到文件中，重用JavaBean组件，转发用户到其他的页面，或者是给Java插件产生HTML代码。下面列出了可用的动作：
>
> jsp:include-当JSP页面被请求的时候包含一个文件。
>
> jsp:useBean-找出或者是初始化Javabean。
>
> jsp:setProperty-设置JavaBean的属性。
>
> jsp:getProperty-获取JavaBean的属性。
>
> jsp:forward-把请求转发到新的页面。
>
> jsp:plugin-产生特定浏览器的代码。

6.  JSP工作原理

> JSP是一种Servlet，但是与HttpServlet的工作方式不太一样。HttpServlet是先由源代码编译为class文件后部署到服务器下，为先编译后部署。而JSP则是先部署后编译。JSP会在客户端第一次请求JSP文件时被编译为HttpJspPage类（接口Servlet的一个子类）。该类会被服务器临时存放在服务器工作目录里面。下面通过实例给大家介绍。 工程JspLoginDemo下有一个名为login.jsp的Jsp文件，把工程第一次部署到服务器上后访问这个Jsp文件，我们发现这个目录下多了下图这两个东东。 .class文件便是JSP对应的Servlet。编译完毕后再运行class文件来响应客户端请求。以后客户端访问login.jsp的时候，Tomcat将不再重新编译JSP文件，而是直接调用class文件来响应客户端请求。 JSP工作原理 由于JSP只会在客户端第一次请求的时候被编译 ，因此第一次请求JSP时会感觉比较慢，之后就会感觉快很多。如果把服务器保存的class文件删除，服务器也会重新编译JSP。
>
> 开发Web程序时经常需要修改JSP。Tomcat能够自动检测到JSP程序的改动。如果检测到JSP源代码发生了改动。Tomcat会在下次客户端请求JSP时重新编译JSP，而不需要重启Tomcat。这种自动检测功能是默认开启的，检测改动会消耗少量的时间，在部署Web应用的时候可以在web.xml中将它关掉。

参考：《javaweb整合开发王者归来》P97

66. 为什么需要JSP？

> ![](media/image29.png){width="5.427083333333333in" height="3.1220778652668417in"}

67. 什么是JSP？

> JSP (Java Server Pages)是指：

-   在HTML中嵌入Java脚本代码

-   由应用服务器中的JSP引擎来编译和执行嵌入的Java脚本代码

-   然后将生成的整个页面信息返回给客户端

> ![](media/image30.png){width="5.311836176727909in" height="2.333041338582677in"}

68. JSP执行过程

> Web容器处理JSP文件请求需要经过3个阶段：

-   翻译阶段

-   编译阶段

-   执行阶段

> ![](media/image31.png){width="4.208333333333333in" height="2.2462204724409447in"}
>
> 第一次请求之后，Web容器可以重用已经编译好的字节码文件。
>
> ![](media/image32.png){width="3.5416666666666665in" height="1.8776170166229222in"}
>
> 注意：如果对JSP文件进行了修改，Web容器会重新对JSP文件进行翻译和编译。

69. JSP页面组成

> JSP 页面的元素包括：
>
> ![](media/image33.png){width="6.415865048118985in" height="3.2079319772528434in"}

70. 什么是page指令

    22. page指令

        -   通过设置内部的多个属性来定义整个页面的属性

        -   语法：\<%@ page 属性1=\"属性值\" 属性2=\"属性值1,属性值2\"... 属性n=\"属性值n\"%\>

    23. page指令常用属性

> ![](media/image34.png){width="5.488897637795276in" height="2.405949256342957in"}

71. 小脚本与表达式

> 例子：在JSP页面中计算两个数的和，将结果输出显示
>
> ![](media/image35.png){width="5.874266185476816in" height="3.343332239720035in"}

72. 什么是声明

> 声明就是在JSP页面中定义Java的变量和方法
>
> 语法：\<%! Java代码%\>
>
> 方法声明后可在页面中多处调用

73. JSP中的注释

> 合理、详细的注释有利于代码后期的维护和阅读
>
> 在JSP文件的编写过程中，共有三种注释方法：
>
> ![](media/image36.png){width="4.229166666666667in" height="1.2228926071741033in"}

74. Web程序的调试与排错

> 在运行Web程序时，常犯的一些错误有：

-   未启动Tomcat服务，或者没有在预期的端口中启动Tomcat服务。（无法显示网页）

> 启动Tomcat服务。如果控制台上显示Tomcat服务已启动，观察端口号是否与预期端口号一致，按照实际端口号重新运行

-   未部署Web应用，就试图运行Web程序。（404）

> ![](media/image37.png){width="3.1662707786526685in" height="0.6145067804024497in"}

-   运行时，URL输入错误

> ![](media/image38.png){width="3.45790135608049in" height="0.7290758967629046in"}

-   存放文件的目录无法对外引用，如：文件放入了WEB-INF、META-INF等文件夹

75. 

[[JSP九大内置对象，七大动作，三大指令总结]{.underline}](http://blog.csdn.net/qq_34337272/article/details/64310849)

### 内置对象（9）

76. 什么是JSP内置对象？

    24. JSP内置对象是 Web 容器创建的一组对象

    25. JSP内置对象的名称是JSP 的保留字

    26. JSP内置对象是可以直接在JSP页面使用的对象，无需使用"new"获取实例

![](media/image39.png){width="3.7604166666666665in" height="1.7731353893263342in"} ![](media/image40.png){width="2.28125in" height="1.907665135608049in"}

77. JSP 有哪些内置对象？作用分别是什么？ （考）

JSP 有 9 大内置对象：

1)  request：封装（处理）客户端的请求，其中包含来自 get 或 post 请求的参数；

2)  response：封装服务器对客户端的响应；

3)  pageContext：通过该对象可以获取其他对象；

4)  session：封装用户会话的对象；

5)  application：封装服务器运行环境的对象；

6)  out：输出服务器响应的输出流对象；

7)  config：Web 应用的配置对象；

8)  page：JSP 页面本身（相当于 Java 程序中的 this）；

9)  exception：封装页面抛出异常的对象。

#### Request

78. request对象

> 主要用于处理客户端请求

![](media/image41.png){width="3.8229166666666665in" height="0.9409109798775153in"}

> request对象常用方法

![](media/image42.png){width="5.104166666666667in" height="2.428938101487314in"}

> 例子：信息读取显示

![](media/image43.png){width="3.7708333333333335in" height="1.9523753280839895in"} ![](media/image44.png){width="2.6979166666666665in" height="1.5655785214348206in"}

> 例子：乱码问题------**在页面设置支持中文字符的字符集**

![](media/image45.png){width="3.7708333333333335in" height="1.4010892388451444in"} ![](media/image46.png){width="2.59375in" height="1.5051323272090988in"}

79. Request对象的主要方法有哪些

setAttribute(String name,Object)：设置名字为name的request 的参数值

getAttribute(String name)：返回由name指定的属性值

getAttributeNames()：返回request 对象所有属性的名字集合，结果是一个枚举的实例

getCookies()：返回客户端的所有 Cookie 对象，结果是一个Cookie 数组

> getCharacterEncoding() ：返回请求中的字符编码方式 = getContentLength() ：返回请求的 Body的长度

getHeader(String name) ：获得HTTP协议定义的文件头信息

getHeaders(String name) ：返回指定名字的request Header 的所有值，结果是一个枚举的实例

getHeaderNames() ：返回所以request Header 的名字，结果是一个枚举的实例

getInputStream() ：返回请求的输入流，用于获得请求中的数据

getMethod() ：获得客户端向服务器端传送数据的方法

getParameter(String name) ：获得客户端传送给服务器端的有 name指定的参数值

> getParameterNames() ：获得客户端传送给服务器端的所有参数的名字，结果是一个枚举的实例

getParameterValues(String name)：获得有name指定的参数的所有值

getProtocol()：获取客户端向服务器端传送数据所依据的协议名称

getQueryString() ：获得查询字符串

getRequestURI() ：获取发出请求字符串的客户端地址

getRemoteAddr()：获取客户端的 IP 地址

getRemoteHost() ：获取客户端的名字

getSession(\[Boolean create\]) ：返回和请求相关 Session

getServerName() ：获取服务器的名字

getServletPath()：获取客户端所请求的脚本文件的路径

getServerPort()：获取服务器的端口号

removeAttribute(String name)：删除请求中的一个属性

80. request.getAttribute()和 request.getParameter()有何区别

> 从获取方向来看：
>
> getParameter()是获取 POST/GET 传递的参数值；
>
> getAttribute()是获取对象容器中的数据值；
>
> 从用途来看：
>
> getParameter()用于客户端重定向时，即点击了链接或提交按扭时传值用，即用于在用表单或url重定向传值时接收数据用。
>
> getAttribute() 用于服务器端重定向时，即在 sevlet 中使用了 forward 函数,或 struts 中使用了 mapping.findForward。 getAttribute 只能收到程序用 setAttribute 传过来的值。
>
> 另外，可以用 setAttribute(),getAttribute() 发送接收对象.而 getParameter() 显然只能传字符串。 setAttribute() 是应用服务器把这个对象放在该页面所对应的一块内存中去，当你的页面服务器重定向到另一个页面时，应用服务器会把这块内存拷贝另一个页面所对应的内存中。这样getAttribute()就能取得你所设下的值，当然这种方法可以传对象。session也一样，只是对象在内存中的生命周期不一样而已。getParameter()只是应用服务器在分析你送上来的 request页面的文本时，取得你设在表单或 url 重定向时的值。

总结：

> getParameter()返回的是String,用于读取提交的表单中的值;（获取之后会根据实际需要转换为自己需要的相应类型，比如整型，日期类型啊等等）
>
> getAttribute()返回的是Object，需进行转换,可用setAttribute()设置成任意对象，使用很灵活，可随时用

#### Response

81. response对象

> 用于响应客户请求并向客户端输出信息

![](media/image47.png){width="3.9479166666666665in" height="1.2397692475940507in"}

> response 对象常用方法

27. void sendRedirect (String location)：将请求重新定位到一个不同的URL，即页面重定向。

![](media/image48.png){width="4.15625in" height="2.556513560804899in"}

28. 使用转发取代重定向实现页面跳转，**请求信息不丢失。**

> 转发的作用：在多个页面交互过程中实现请求数据的共享
>
> 转发的实现：RequestDispatcher对象；forward()方法。

![](media/image49.png){width="4.957713254593176in" height="1.3852438757655292in"}

82. 转发（forward）与重定向（redirect）比较 （考）

> **转发是服务器行为，重定向是客户端行为。**
>
> 转发（Forward） 通过RequestDispatcher对象的forward（HttpServletRequest request,HttpServletResponse response）方法实现的。RequestDispatcher可以通过HttpServletRequest 的getRequestDispatcher()方法获得。例如下面的代码就是跳转到login\_success.jsp页面。
>
> 重定向（Redirect） 是利用服务器返回的状态码来实现的。客户端浏览器请求服务器的时候，服务器会返回一个状态码。服务器通过 HttpServletResponse 的 setStatus(int status) 方法设置状态码。如果服务器返回301或者302，则浏览器会到新的网址重新请求该资源。

1)  地址栏 url 显示：foward url 不会发生改变，redirect url 会发生改变；

> 转发是在服务器内部控制权的转移，客户端浏览器的地址栏不会显示出转向后的地址。重定向是通过浏览器重新请求地址，在地址栏中可以显示转向后的地址

2)  数据共享：forward 可以共享 request 里的数据，redirect 不能共享；

3)  效率：forward 比 redirect 效率高。

4)  转发是在服务器端发挥作用，通过forward方法将提交信息在多个页面间进行传递。重定向是在客户端发挥作用，通过请求新的地址实现页面转向

5)  从运用地方来说

> forward:一般用于用户登陆的时候,根据角色转发到相应的模块. redirect:一般用于用户注销登陆时返回主页面和跳转到其它的网站等

6)  

<!-- -->

83. 84. 自动刷新(Refresh)

> 自动刷新不仅可以实现一段时间之后自动跳转到另一个页面，还可以实现一段时间之后自动刷新本页面。Servlet中通过HttpServletResponse对象设置Header属性实现自动刷新例如：
>
> 其中5为时间，单位为秒。URL指定就是要跳转的页面（如果设置自己的路径，就会实现每过5秒自动刷新本页面一次）

85. include指令include的行为的区别

> include指令： JSP可以通过include指令来包含其他文件。被包含的文件可以是JSP文件、HTML文件或文本文件。包含的文件就好像是该JSP文件的一部分，会被同时编译执行。 语法格式如下： \<%@ include file=\"文件相对 url 地址\" %\>
>
> include动作： \<jsp:include\>动作元素用来包含静态和动态的文件。该动作把指定文件插入正在生成的页面。语法格式如下： \<jsp:include page=\"相对 URL 地址\" flush=\"true\" /\>

### JDBC

86. 什么是JDBC？ （考） （阿里二面）

> JDBC（Java Database Connectivity，Java数据库连接技术）提供连接各种常用数据库的能力，是允许用户在不同数据库之间做选择的一个抽象层。JDBC允许开发者用JAVA写数据库应用程序，而不需要关心底层特定数据库的细节。

![](media/image52.png){width="4.405698818897638in" height="1.9476727909011373in"} ![](media/image53.png){width="1.3811132983377077in" height="2.1041666666666665in"}

87. JDBC API

> JDBC API可做三件事：与数据库建立连接、执行SQL 语句、处理结果。

29. DriverManager类：载入各种不同的JDBC驱动。

30. Connection接口：负责连接数据库并担任传送数据的任务。

31. Statement接口：由 Connection 产生、负责执行SQL语句。

32. ResultSet接口：负责保存Statement执行后所产生的查询结果。

> ![](media/image54.png){width="4.259884076990376in" height="1.8018580489938758in"}

88. JDBC编程步骤：

<!-- -->

1)  加载驱动程序

2)  获得数据库连接

3)  创建Statement\\PreparedStatement对象

<!-- -->

89. JSP访问数据库

> ![](media/image55.png){width="5.677083333333333in" height="3.6019531933508313in"}

90. JDBC驱动

> JDBC驱动由数据库厂商提供

1)  纯Java驱动

-   由JDBC驱动直接访问数据库

-   优点：100% Java，快又可跨平台

-   缺点：访问不同的数据库需要下载专用的JDBC驱动

> ![](media/image56.png){width="2.5833333333333335in" height="1.000213254593176in"}

2)  使用纯Java驱动方式进行直连

-   下载数据库厂商提供的驱动程序包

-   将驱动程序包引入工程中

-   编程，通过纯Java驱动方式与数据库建立连接

> ![](media/image57.png){width="4.770833333333333in" height="1.5590015310586176in"}

91. JDBC URL的作用是什么？

指定数据库信息：数据库名称、用户、密码。

92. 配置MySQL-JDBC驱动程序

<!-- -->

1)  下载安装最新版mySQL（官网www.mysql.com）

2)  拷贝驱动程序至Tomcat库文件目录

3)  设置classpath环境变量

> 将"mysql-connector-java-5.1.34-bin"所在目录添加到classpath

4)  测试是否配置成功：connectionJDBC.jsp

> ![](media/image58.png){width="4.853559711286089in" height="1.885181539807524in"}

93. JavaScript页面验证与JSP的集成

> ![](media/image59.png){width="4.53125in" height="0.9769630358705161in"}

94. 解释下驱动(Driver)在JDBC中的角色。

> JDBC驱动提供了特定厂商对JDBC API接口类的实现，驱动必须要提供java.sql包下面这些类的实现：Connection, Statement, PreparedStatement,CallableStatement, ResultSet和Driver。

95. Class.forName()方法有什么作用？

> 初始化参数指定的类，并且返回此类对应的Class 对象

96. PreparedStatement比Statement有什么优势？

> PreparedStatements是预编译的，因此，性能会更好。同时，不同的查询参数值，PreparedStatement可以重用。

97. Statement与PreparedStatement的区别 （阿里官方面经）

<!-- -->

1)  PreparedStatement支持动态设置参数，Statement不支持。

2)  PreparedStatement可避免如类似 单引号 的编码麻烦，Statement不可以。

3)  PreparedStatement支持预编译，Statement不支持。

4)  在SQL语句出错时PreparedStatement不易检查，而Statement则更便于查错。

5)  PreparedStatement可防止SQL注入，更加安全，而Statement不行。

<!-- -->

98. 什么时候使用CallableStatement？用来准备CallableStatement的方法是什么？

> CallableStatement用来执行存储过程。存储过程是由数据库存储和提供的。存储过程可以接受输入参数，也可以有返回结果。非常鼓励使用存储过程，因为它提供了安全性和模块化。准备一个CallableStatement的方法是：
>
> CallableStatement Connection.prepareCall();

99. 数据库连接池是什么意思？

> 像打开关闭数据库连接这种和数据库的交互可能是很费时的，尤其是当客户端数量增加的时候，会消耗大量的资源，成本是非常高的。可以在应用服务器启动的时候建立很多个数据库连接并维护在一个池中。连接请求由池中的连接提供。在连接使用完毕以后，把连接归还到池中，以用于满足将来更多的请求。

100. 

### 状态管理

101. 实现会话跟踪的技术有哪些

        33. 使用Cookie

> 向客户端发送Cookie
>
> 从客户端读取Cookie
>
> 优点: 数据可以持久保存，不需要服务器资源，简单，基于文本的Key-Value
>
> 缺点: 大小受到限制，用户可以禁用Cookie功能，由于保存在本地，有一定的安全风险。

34. URL 重写

> 在URL中添加用户会话的信息作为请求的参数，或者将唯一的会话ID添加到URL结尾以标识一个会话。
>
> 优点： 在Cookie被禁用的时候依然可以使用
>
> 缺点： 必须对网站的URL进行编码，所有页面必须动态生成，不能用预先记录下来的URL进行访问。

35. 隐藏的表单域

36. HttpSession

> 在所有会话跟踪技术中，HttpSession对象是最强大也是功能最多的。当一个用户第一次访问某个网站时会自动创建 HttpSession，每个用户可以访问他自己的HttpSession。可以通过HttpServletRequest对象的getSession方 法获得HttpSession，通过HttpSession的setAttribute方法可以将一个值放在HttpSession中，通过调用 HttpSession对象的getAttribute方法，同时传入属性名就可以获取保存在HttpSession中的对象。与上面三种方式不同的 是，HttpSession放在服务器的内存中，因此不要将过大的对象放在里面，即使目前的Servlet容器可以在内存将满时将HttpSession 中的对象移到其他存储设备中，但是这样势必影响性能。添加到HttpSession中的值可以是任意Java对象，这个对象最好实现了 Serializable接口，这样Servlet容器在必要的时候可以将其序列化到文件中，否则在序列化时就会出现异常。

#### Cookie

102. 为什么使用Cookie

> 浏览器-HTTP-服务器。HTTP协议是无记忆的

-   用户请求，服务器响应，断开连接

-   任一请求，服务器都当做第一次请求

> 实际开发中，希望服务器识别用户。Netscape提出cookie，保存用户识别信息。

103. 什么是Cookie

> Cookie是Web服务器保存在客户端的一系列文本信息

37. Cookie的作用：对特定对象的追踪；统计网页浏览次数；简化登录

38. 安全性能：容易信息泄露

<!-- -->

104. Cookie的语法

        39. 导入包
    
        40. 创建Cookie

> Parameter：用于代表cookie的名称(key)
>
> value：用于表示当前key名称所对应的值

41. 写入Cookie

<!-- -->

105. 设置Cookie属性的常用方法

![](media/image66.png){width="4.270299650043745in" height="1.9060115923009624in"}

106. JSP中应用Cookie

![](media/image67.png){width="5.010416666666667in" height="3.1189654418197725in"}

107. Cookie有效期

![](media/image68.png){width="5.114583333333333in" height="3.06715769903762in"}

108. Cookie的传输过程？Cookie失效 （阿里二面）

#### Session

109. 访问控制

![](media/image69.png){width="4.822916666666667in" height="2.942930883639545in"}

110. 什么是会话

> 一个会话就是浏览器与服务器之间的一次通话，包含浏览器与服务器之间的多次请求、响应过程。
>
> session是JSP内置对象，与浏览器一一对应，允许用户存储和提取会话状态的信息。

![](media/image70.png){width="4.697916666666667in" height="2.2120548993875766in"}

111. JSP内置对象session

> Session原义：有始有终的一系列动作

-   打电话：甲方拿起电话拨通乙方电话的一系列过程，电话挂断，会话结束

-   浏览器打开到关闭的一系列过程

> Session须遵守的session机制（服务器端机制）

-   在服务器端通过散列表保存

-   当服务器接收客户端请求时

<!-- -->

-   先检查客户端是否已创建session（通过唯一的sessionid）

-   如果已包含sessionid，读取sessionid对应的session

-   否则，创建session，并生成sessionid，然后将sessionid在本次响应的过程返回到客户端保存

112. Sessionid在客户端的保存

> 客户端用cookie保存用户信息，因此，保存sessionid也是用cookie。
>
> 保存sessionid的名称（键）类似于SESSIONID，而其值是一串复杂的字符串
>
> 例如，JSESSIONID=25FAA004DF3881F5C1BE5EF27CC0D21C
>
> ![](media/image71.png){width="4.072916666666667in" height="0.7472069116360455in"}

113. session与窗口的关系

> 一个session对应一个窗口，那么通过超链接打开的窗口是否也是新的session呢？

-   每个session对象都与浏览器一一对应 重新开启一个浏览器，相当于重新创建一个session对象重新开启一个IE窗口，直接访问系统首页面

-   通过超链接打开的新窗口，新窗口的session与其父窗口的session相同

114. session对象

> 用来存储有关用户会话的所有信息
>
> session对象常用方法：

![](media/image72.png){width="3.8328543307086615in" height="1.9893350831146106in"}

115. 使用session实现访问控制

![](media/image73.png){width="5.34375in" height="2.41040791776028in"}

> 在控制页面获取用户请求的登录信息进行验证

![](media/image74.png){width="4.302083333333333in" height="1.422736220472441in"}

> 在新闻发布系统新闻发布页面增加登录验证

![](media/image75.png){width="3.5104166666666665in" height="1.558099300087489in"}

116. Include指令

> 除了首页面，其它页面中同样需要加入登录验证，有没有办法避免冗余代码的出现？
>
> 可以将一些共性的内容写入一个单独的文件中，然后通过include指令引用该文件，从而降低代码的冗余问题，也便于修改共性内容。

![](media/image76.png){width="4.2390529308836395in" height="2.7079943132108486in"}

117. Cookie与session的比较

<!-- -->

1)  session是在服务器端保存用户信息，Cookie是在客户端保存用户信息

2)  session中保存的是对象，Cookie保存的是字符串

3)  session随会话结束而关闭，Cookie可以长期保存在客户端

4)  Cookie通常用于保存不重要的用户信息，重要的信息使用session保存

#### application

118. JSP内置对象application

> application类似于系统的"全局变量"，用于实现用户之间的数据共享
>
> application对象的常用方法：

-   void setAttribute(String key, Object value)：以键/值的方式，将一个对象的值存放到application中

> ![](media/image77.png){width="4.645833333333333in" height="0.3567027559055118in"}

-   Object getAttribute(String key)：根据键去获取application中存放对象的值

![](media/image78.png){width="4.78125in" height="0.7841852580927384in"}

application是JSP内置对象：实现服务内数据的共享；在服务内值存在一个对象实例。

application对象的常用方法

![](media/image79.png){width="4.15573053368329in" height="1.1665212160979876in"}

119. Application实现访问人数统计

> ![](media/image80.png){width="4.9375in" height="3.0232688101487315in"}
>
> ![](media/image81.png){width="5.145833333333333in" height="2.151894138232721in"}

120. 

### 作用域（4）

121. 如何实现JSP或Servlet的单线程模式

对于JSP页面，可以通过page指令进行设置。 \<%\@page isThreadSafe=\"false\"%\>

对于Servlet，可以让自定义的Servlet实现SingleThreadModel标识接口。

> 说明：如果将JSP或Servlet设置成单线程工作模式，会导致每个请求创建一个Servlet实例，这种实践将导致严重的性能问题（服务器的内存压力很大，还会导致频繁的垃圾回收），所以通常情况下并不会这么做。

122. JSP内置对象的范围 说一下 JSP 的 4 种作用域？ （考）

> 对象的范围，决定了JSP是否可以进行对象访问。
>
> 范围的分类

1)  page：代表与一个页面相关的对象和属性。

2)  request：代表与客户端发出的一个请求相关的对象和属性。一个请求可能跨越多个页面，涉及多个 Web 组件；需要在页面显示的临时数据可以置于此作用域。

3)  session：代表与某个用户与服务器建立的一次会话相关的对象和属性。跟某个用户相关的数据应该放在用户自己的 session 中。

4)  application：代表与整个 Web 应用程序相关的对象和属性，它实质上是跨越整个 Web 应用程序，包括多个页面、请求和会话的一个全局作用域。

![](media/image82.png){width="3.8745155293088365in" height="1.9580883639545057in"}

123. pageContext对象

<!-- -->

1)  提供了对JSP页面所有的对象及命名空间的访问。可以访问除本身以外的8个JSP内部对象。包括application对象、exception对象，还有session对象等。

2)  include(String relativeUrlPath)方法：让当前文件包含进一个外部文件

<!-- -->

124. 

### JSP优化

125. JNDI介绍

> JNDI（Java Naming and Directory Interface，Java命名和目录接口），是一组在Java应用中访问命名和目录服务的API，通过名称将资源与服务进行关联，可以把JNDI简单的理解成一种将对象和名字绑定的服务。

-   指定一个资源名称，并将其与某一资源和服务相关联

-   尤其在分布式应用中，需要访问其他组件或资源时

    -   通过JIDI服务进行定位

    -   应用程序通过名称获得相应的资源或服务

126. JNDI的简单应用

> ![](media/image83.png){width="5.332666229221347in" height="2.7809022309711287in"}

127. JNDI VS Application对象

        42. Application对象只能在一个web应用程序中使用
    
        43. JNDI发布的信息对服务器上的所有web应用程序可见
    
        44. JNDI还提供了对其他资源的访问
    
        45. 使用JNDI和数据源实现数据库连接池的访问

> JNDI与数据库连接池的关系：通过JNDI给资源命名，以便直接通过名称来访问数据库连接池

#### 数据库连接池

数据库连接池的原理，大概说一下 （阿里一面）

128. 生活中的连接池

![](media/image84.png){width="2.9270833333333335in" height="1.7405916447944008in"} ![](media/image85.png){width="3.4583333333333335in" height="1.6586734470691165in"}

129. 为什么使用连接池

> 传统数据库连接方式的不足

a.  每一次请求时均需要与数据库进行连接，资源占用较多

b.  当并发访问数量较大时，网站速度收到极大影响

c.  在访问结束后必须要关闭连接释放资源

d.  系统的安全性和稳定性相对较差

> 企业级开发需要稳健和高效的数据访问层

a.  完成对数据库的CRUD操作

b.  能够处理数据库发生的各种错误

c.  可以灵活的修改配置

d.  提供方便使用的工具

e.  高性能

> CRUD操作：增加(Create)、查询(Retrieve)(重新得到数据)、更新(Update)和删除(Delete)。

130. 什么是连接池技术

> 连接池：在内存中预设好一定数量的连接对象，以备用户在进行数据库操作时直接使用
>
> 性能：数据库连接的建立、断开均由管理池统一管理
>
> 连接池技术与传统数据库连接的比较

-   数据库操作性能得到提升

-   通过连接池管理数据库的连接与释放、提高了系统资源的使用效率

131. 连接池技术工作原理

> 连接池是由容器提供的，用来管理池中连接对象。

![](media/image86.png){width="4.863975284339458in" height="1.9789195100612424in"}

132. 数据源（DataSource）

> 连接池中的连接对象由数据源创建。

46. javax.sql.DataSource接口负责建立与数据库的连接

47. 从Tomcat的数据源获得连接

48. 把连接保存在连接池中

<!-- -->

133. 如何获得DataSource对象

        49. 数据源由Tomcat提供，不能在程序中创建实例
    
        50. 使用JNDI获得DataSource引用

> ![](media/image87.png){width="5.030621172353456in" height="1.1665212160979876in"}
>
> ![](media/image88.png){width="5.4368208661417325in" height="3.22876312335958in"}
>
> Tomcat的conf/context.xml中的配置
>
> ![](media/image89.png){width="5.155605861767279in" height="3.2808398950131235in"}
>
> ![](media/image90.png){width="5.082697944006999in" height="2.3226268591426074in"}（红框内容替换）
>
> 加入数据库驱动文件：把数据库驱动的.jar文件，加入到Tomcat的common\\lib中
>
> 应用程序的web.xml文件的配置：在web.xml中配置\<resource-ref\>
>
> ![](media/image91.png){width="6.69707895888014in" height="1.9893350831146106in"}

#### JavaBean

134. 为什么需要JavaBean

> 传统处理的业务的弊端
>
> ![](media/image92.png){width="5.113943569553806in" height="2.6663331146106737in"}
>
> JavaBean的优势

-   解决代码重复编写，减少代码冗余

-   功能区分明确，避免业务逻辑处理与页面显示处理集中在一起造成混乱

-   提高了代码的维护性

135. JavaBean及其分类

> 符合规范的Java类都是JavaBean
>
> JavaBean的分类

1)  封装数据

-   按照OO原则，属性与数据库表字段相对应

-   属性私有

-   具有public的set/get方法

2)  封装业务

-   具有实现特定功能的方法和方法实现

-   通常与一个封装数据的JavaBean对应

136. 封装数据的JavaBean

> ![](media/image93.png){width="4.625in" height="2.817341426071741in"}

137. 封装业务的JavaBean

> ![](media/image94.png){width="4.791067366579178in" height="3.0100404636920386in"}

138. JavaBean的应用

> 在JSP页面中导入JavaBean
>
> ![](media/image95.png){width="4.4681911636045495in" height="1.3644127296587927in"}

### 业务应用

#### 分页

139. 分页显示的步骤

        51. 确定每页显示的数据数量
    
        52. 计算显示的页数
    
        53. 编写SQL语句

140. 分页实现步骤

        54. 获取总记录数

> ![](media/image96.png){width="3.4479166666666665in" height="1.6490037182852144in"}

55. 根据每页显示记录数与总记录数计算总页数

> ![](media/image97.png){width="5.429861111111111in" height="1.1690912073490813in"}

56. ......

#### SmartUpload

141. SmartUpload组件

专门用于实现文件上传及下载的免费组件

SmartUpload组件特点

-   使用简单：编写少量代码，完成上传下载功能

-   能够控制上传内容

-   能够控制上传文件的大小、类型

缺点：目前已停止更新服务

### MVC分层

142. 为什么需要分层

    -   JSP开发的弊端：业务处理的代码与JSP代码混在一起，不易于阅读，不易于代码维护
    
    -   软件设计中的分层模式：将解决方案的组件分隔到不同的层中；在同一个层中组件之间保持内聚性；层与层之间保持松耦合

143. 三层模式

![](media/image98.png){width="1.215923009623797in" height="2.0833333333333335in"}

144. 分层实现用户登录例子

        57. 创建用户实体类

> ![](media/image99.png){width="1.5625in" height="1.743561898512686in"}

58. 编辑数据访问层

![](media/image100.png){width="3.9375in" height="2.2157797462817146in"}

59. 编写业务逻辑层

![](media/image101.png){width="3.9375in" height="2.476415135608049in"}

60. 编写表示层

![](media/image102.png){width="3.4583333333333335in" height="2.5228193350831147in"}

145. 三层开发遵循的原则

        61. 上层依赖其下层，依赖关系不跨层

        -   表示层不能直接访问数据访问层

        -   上层调用下层的结果，取决于下层的实现

        62. 下一层不能调用上一层
    
        63. 下一层不依赖上一层

        -   上层的改变不会影响下一层

        -   下层的改变会影响上一层得到的结果

        64. 在上一层中不能出现下一层的概念

> 分工明确，各司其职

146. 分层开发的优势

-   职责划分清晰

-   无损替换

-   复用代码

-   降低了系统内部的依赖程度

147. 

### EL

148. 为什么需要EL

> JSP嵌入大量Java代码
>
> JavaBean在JSP中的局限：获取JavaBean属性必须要实例化；强制类型转化
>
> 使用EL表达式简化，解决上述问题。

149. 什么是EL

> EL即Expression Language（表达式语言）

150. EL的功能

> 替代JSP页面中的复杂代码
>
> 定义了一系列隐含对象和操作符，能方便的访问页面上下文

151. EL的语法

> 以"\${"作为开始，以"}"作为结束，直接使用变量名获取值\$
>
> ![](media/image103.png){width="3.582884951881015in" height="0.8957217847769029in"}
>
> 变量属性范围名称
>
> ![](media/image104.png){width="4.874390857392826in" height="1.7081200787401576in"}

152. EL的特点

-   自动转换类型：EL得到某个数据时可以自动转换类型(类似JS）；对类型的限制更加宽松

-   使用简单：相比较在JSP中嵌入Java代码，EL应用更简单

153. EL运算符

        65. 运算符"."：访问对象的属性
    
        66. 运算符"\[ \]"：访问对象的属性；访问数组元素

154. EL隐式对象

> ![](media/image105.png){width="5.041036745406824in" height="2.718409886264217in"}
>
> ![](media/image106.png){width="5.051452318460193in" height="2.5413484251968503in"}

### JSTL

155. 为什么使用JSTL？

> 使用了EL表达式可以简化JSP页面代码，但是如果需要进行逻辑判断怎么办？
>
> 虽然EL表达式可以访问JavaBean的属性，但是并不能实现在JSP中进行逻辑判断，因而要使用JSTL标签。

156. 什么是JSTL

> JSTL（JavaServerPages Standard Tag Library）JSP标准标签库，使用JSTL实现JSP页面中逻辑处理。JSTL提供一组标准标签，可用于编写各种动态 JSP 页面。
>
> JSTL通常会与EL表达式合作实现JSP页面的编码

157. 使用JSTL的步骤

        67. 创建Web工程，选择JSTL1.1
    
        68. 在JSP页面添加taglib指令

> ![](media/image107.png){width="4.22863845144357in" height="0.5624300087489064in"}

69. 使用JSTL标签

<!-- -->

158. JSTL标准标签库内的标签

> ![](media/image108.png){width="3.5516393263342083in" height="2.4788571741032372in"}
>
> ![](media/image109.png){width="5.301420603674541in" height="3.218347550306212in"}

159. 

### DisplayTag

### 事务管理，批处理

## Web

### 监听器（Listener）

160. 什么是监听器？

> Servlet规范中定义的一种特殊类，用于监听ServletContext、HttpSession和ServletRequest等域对象的创建与销毁事件。
>
> 用于监听域对象的属性发生修改的事件，可以在事件发生前、发生后做一些必要的处理。
>
> ![](media/image110.png){width="5.927083333333333in" height="2.4059175415573053in"}

161. 监听器有什么用？

1、统计在线人数和在线用户

2、系统启动时加载初始化信息

3、统计网站访问量

> 4、跟Spring结合

162. 监听器的实例

-   创建一个实现监听器接口的类

-   配置web.xml进行注册

> ![](media/image111.png){width="5.207682633420823in" height="0.4686909448818898in"}

163. 监听器的启动顺序

> ![](media/image112.png){width="6.145833333333333in" height="2.2357250656167977in"}

164. 监听器的分类

        70. 按监听对象划分

        i.  用于监听应用程序环境对象( ServletContext )的事件监听器

> ![](media/image113.png){width="6.179861111111111in" height="3.102648731408574in"}

ii. 用于监听用户会话对象( HttpSession )的事件监听器

> ![](media/image114.png){width="6.106944444444444in" height="3.1480325896762906in"}

iii. 用于监听请求消息对象( ServletRequest )的事件监听器

<!-- -->

71. 按监听事件划分

    iv. 监听域对象自身的创建和销毁的事件监听器)

> 包括：ServletContext（ServletContextListener接口）、HttpSession（HttpSessionListener接口）、ServletRequest（ServletRequestListener接口）
>
> ![](media/image115.png){width="5.148611111111111in" height="2.3129396325459317in"}

v.  监听域对象中的属性的增加和删除的事件监听器

vi. 监听绑定到HttpSession域中的某个对象的状态的事件监听器

<!-- -->

165. 

![](media/image116.png){width="6.290880358705162in" height="3.9474234470691165in"}

Servlet3.0下监听器的用法

\@WebListener

该注解用于将类声明为监听器,被\@WebListener标注的类必须实现以下至少一个接口:

ServletContextListener

ServletContextAttribute Listener

ServletRequestListener

ServletRequestAttributeListener

HttpSessionListener

HttpSessionAttributeListener

\@WebListener的常用属性

![](media/image117.png){width="6.499187445319335in" height="3.31208552055993in"}

### 过滤器（filter）

166. 过滤器有什么用？过滤器的应用场景

用户是否登录；输入的网址是否正确

> ![](media/image118.png){width="2.3958333333333335in" height="2.345217629046369in"}

167. 过滤器是什么？

> 过滤器是一个服务器端的组件，它可以截取用户端的请求与响应信息，并对这些信息过滤。
>
> Web过滤器：过滤请求，不处理结果。
>
> 过滤器能改变用户请求的web资源，能改变用户请求的路径。但不能直接返回数据，不能直接处理用户请求。

168. 过滤器工作原理

> ![](media/image119.png){width="4.25in" height="2.3275437445319334in"}

169. 过滤器生命周期

> ![](media/image120.png){width="3.9166666666666665in" height="2.484358048993876in"}

170. 过滤器常用方法API

> 过滤器实现Filter接口。
>
> ![](media/image121.png){width="5.260416666666667in" height="2.9609536307961504in"}

171. 过滤器在web.xml中的配置

> ![](media/image122.png){width="5.28125in" height="2.74002624671916in"}

172. 过滤器链

> Web项目中多个过滤器是如何实现的？多个过滤器对应同一个用户路径执行顺序如何？
>
> ![](media/image123.png){width="5.885416666666667in" height="1.3138943569553805in"}
>
> ![](media/image124.png){width="5.875in" height="3.107923228346457in"}

173. 过滤器的类型

> ![](media/image125.png){width="5.8125in" height="2.6305489938757654in"}
>
> \@WebFilter用于将一个类声明为过滤器,该注解将会在部署时被容器处理,容器将根据具体的属性配置将相应的类部署为过滤器。
>
> ![](media/image126.png){width="6.333333333333333in" height="3.052209098862642in"}
>
> ![](media/image127.png){width="6.7387412510936135in" height="3.8953466754155732in"}

174. 登录认证及编码

### 请求/响应架构原理

#### 跨域请求

175. 如何实现跨域请求？ （考）

<!-- -->

1)  ·jsonp

> 利用了 script 不受同源策略的限制
>
> 缺点：只能 get 方式，易受到 XSS攻击

2)  ·CORS（Cross-Origin Resource Sharing）,跨域资源共享

> 当使用XMLHttpRequest发送请求时，如果浏览器发现违反了同源策略就会自动加上一个请求头 origin；
>
> 后端在接受到请求后确定响应后会在后端在接受到请求后确定响应后会在 Response Headers 中加入一个属性 Access-Control-Allow-Origin；
>
> 浏览器判断响应中的 Access-Control-Allow-Origin 值是否和当前的地址相同，匹配成功后才继续响应处理，否则报错
>
> 缺点：忽略 cookie，浏览器版本有一定要求

3)  ·代理跨域请求

> 前端向发送请求，经过代理，请求需要的服务器资源
>
> 缺点：需要额外的代理服务器

4)  ·Html5 postMessage 方法

> 允许来自不同源的脚本采用异步方式进行有限的通信，可以实现跨文本、多窗口、跨域消息传递
>
> 缺点：浏览器版本要求，部分浏览器要配置放开跨域限制

5)  ·修改 document.domain 跨子域

> 相同主域名下的不同子域名资源，设置 document.domain 为 相同的一级域名
>
> 缺点：同一一级域名；相同协议；相同端口

6)  ·基于 Html5 websocket 协议

> websocket 是 Html5 一种新的协议，基于该协议可以做到浏览器与服务器全双工通信，允许跨域请求
>
> 缺点：浏览器一定版本要求，服务器需要支持 websocket 协议

7)  ·http://document.xxx + iframe

> 通过 iframe 是浏览器非同源标签，加载内容中转，传到当前页面的属性中
>
> 缺点：页面的属性值有大小限制

176. 说一下 JSONP 实现原理？ （考）

> jsonp：JSON with Padding，它是利用script标签的 src 连接可以访问不同源的特性，加载远程返回的"JS 函数"来执行的。

# 

# Java EE部分

## Maven

Apache Maven是主要用于Java项目的一个自动化构建工具，提供项目对象模型（Project Object Model，简称POM）文件的新概念来管理项目。POM提供单个项目的所有配置，涵盖[项目的名称，所有者及其对其他项目的依赖关系]{.underline}。此外，POM还可以配置构建过程的各个阶段，这些阶段以插件形式实现。Maven有两个核心功能：其一是软件构建，其二是依赖管理。使用Maven的Java项目的目录结构，如图3所示。Maven的逻辑模型如图4所示。

![2-maven文件](media/image128.png){width="1.9791666666666667in" height="2.6875in"}

图 3 Maven为Java项目自动生成的目录结构

![2-maven](media/image129.png){width="5.885416666666667in" height="3.75in"}

图 4 Maven的概念模型

177. 为什么要用Maven

> 在开发中经常需要依赖第三方的包，包与包之间存在依赖关系，版本间还有兼容性问题，有时还里要将旧的包升级或降级，当项目复杂到一定程度时包管理变得非常重要。

178. 有了Maven，它提供了三种功能：

-   依赖的管理：仅仅通过jar包的几个属性，就能确定唯一的jar包，在指定的文件pom.xml中，只要写入这些依赖属性，就会自动下载并管理jar包。

-   项目的构建：内置很多的插件与生命周期，支持多种任务，比如校验、编译、测试、打包、部署、发布\...

-   项目的知识管理：管理项目相关的其他内容，比如开发者信息，版本等等

179. maven打包，说出几个maven命令 （考）（小米一面）

打包步骤是：清除，打包

一般的maven项目打包命令是：mvn clean package

1)  mvn clean：打包前清理掉之前有过打包的文件夹target

2)  mvn compile：项目编译

3)  mvn package：开始项目打包

> 执行这步可以不用执行compile了
>
> package包括了编译、打包这两步
>
> package完成后，会自动生成一个target文件，根据你编写的pom打包命令和assembly文件可以在 \\target\\dist 目录下找到你打包好的项目文件夹和项目压缩包

4)  mvn install

> 将打包好的jar包部署到本地，放到你本地的.m2仓库中
>
> 这一步主要是当你的项目是几个模块组成的时候，其中的模块需要相互依赖时用到

## Bootstrap框架

Bootstrap用于设计网站和Web应用程序，是目前最受欢迎的开源前端框架。它包含基于HTML和CSS的版式设计模板、表单、按钮、导航和其他界面组件，以及可选的JavaScript扩展。

Bootstrap的优点主要有：

1.  兼容多种浏览器。如谷歌、火狐和IE8等浏览器。

2.  支持响应式网页设计。

它提供了一套响应式、移动设备优先的流式栅格系统布局。这意味着系统会根据使用设备的特性为用户动态调整页面布局。

3.  提供较为全面的组件以及JavaScript插件

4.  支持Less或Sass样式语言。

5.  个性化定制前端。用户可通过定制组件、样式表和JavaScript插件来设计实现自己的前端。

## SSM框架

Java Web框架 SSM有哪些框架 （阿里一面）

由Spring、Spring MVC和Mybaits三个开源框架整合而成的SSM框架是当前的Java EE（企业版）主流框架。

1.  Spring

Spring是控制反转和面向切面的一个容器框架，开源的轻量级Java开发框架。任何Java应用程序都可以使用该框架的核心功能，在Java EE（企业版）平台还可以扩展构建Web应用程序。

控制反转（IoC）是一种设计思想，提供了一种使用反射来配置和管理Java对象的一致方法。对象的生命周期及对象间的关系由容器负责管理。[容器创建的对象也称为托管对象或bean]{.underline}，可以通过加载XML（可扩展标记语言）文件或检测配置类上的特定Java注释来配置容器。这些数据源包含提供创建bean所需信息的bean定义。对象可以通过依赖查找或依赖注入（DI）获得。依赖查找是调用者向容器对象请求具有特定名称或特定类型的对象的模式。依赖注入是一种模式，容器通过构造函数，属性或工厂方法将对象按名称传递给其他对象。控制反转旨在降低对象间的耦合性。

面向切面编程（AOP）是一种编程范例，支持源代码层面的模块化，允许分离横切关注点来增加模块。在向现有系统添加新模块时它通过"切入点"规范分别指定需要修改的程序，不修改已编辑好的代码。AOP降低业务逻辑各部分间的耦合度，提高系统可重用性，提高开发效率。

2.  Spring MVC

Spring MVC是Spring框架的模型-视图-控制器（MVC）Web应用程序框架，是Spring产品组合的一部分，享有Spring的所有优点，是一个基于请求的框架^\[14-15\]^。该框架为所有必须由框架处理的任务定义了方法接口。所有接口都与Servlet API紧密耦合。每个接口的目标都是简单明了的，以便Spring MVC用户可以很容易地定制。

DispatcherServlet类是框架的前端控制器，负责在HTTP请求的执行阶段将控制委派给各个接口。具体的架构流程如图5所示。

![2-springmvc](media/image132.png){width="6.291666666666667in" height="1.71875in"}

图 5 Spring MVC 架构的具体流程

3.  Mybaits

MyBatis使用XML描述符或注释[将对象与存储过程或SQL语句连接起来]{.underline}，是一个Java持久层框架。它将Java方法映射到SQL语句，简化了编码。

MyBatis与Spring框架集成时，系统允许MyBatis参与Spring事务，将构建MyBatis映射器和会话，并将它们注入其他bean中。

## 项目结构设计

### 文件结构（代码、配置）

1.  后台文件结构

后台的文件可分解为以下包：Model、Dao、Mapper、Biz（Service）、BizImpl（ServiceImpl）、Controller、Property、Util、Crawler、Template。其中，Model层用来设计实体的属性和行为；Dao层，提供访问数据库的接口；Mapper层由Mybaits实现，实现Dao层中的接口，包含了各种数据库的操作方法的SQL语句，主要做数据库的交互工作，实现数据的持久化；Biz层，也叫Service层，提供业务逻辑处理，通过调用Dao中的方法来完成业务层上的操作，其目的是封装对数据库的操作；BizImpl层实现Biz中的接口；Controller层，起控制作用，是业务层的一部分，控制流程：取出前台界面的数据，调用BizImpl方法，转发到下一个方法或页面。

此外，Property包将固有属性从Controller中分离出来，为Controller包提供实体的默认属性，如添加项目论文时审核状态默认为"待审核"。Util包为工具类，主要为Controller层服务。Template包是为了Controller层设计的，提供了实体的导出模板文件。

后台文件的调用关系如图14所示。

![4-代码调用](media/image133.png){width="6.291666666666667in" height="2.0833333333333335in"}

图 14 后台文件调用关系

2.  前台文件结构

![4-前台](media/image134.png){width="4.885416666666667in" height="4.052083333333333in"}

图 15 前台文件夹结构及调用关系

前台的代码结构及其调用关系如图15所示。CSS中包含自定义的CSS文件；Frame中包含前台使用的框架，如Bootstrap等；images中包含图片文件；js中包含自定义的JavaScript文件；template中包含批量添加时的xls文件模板；在views中包含jsp文件，实现用户交互界面。Citation包含引用实验室成果的他人成果，在本系统中，仅需要实现引用论文。Data包含领域专家、权威机构和知名期刊以及实验室资料。Others包含实验室附件以及实验室公告。Result中包含项目、项目论文、项目专利、项目软件著作权和学位论文。User中包含管理员、学生和教师。

### 逻辑层次

1)  Model类：用来设计实体的属性和行为。就是java been或者pojo用来存放[实体类]{.underline}对象，有Get、Set的方法，把现实中的东西看成一个实体，封装成一个类，一个实体类对应数据库里的一个表。

2)  Dao接口：提供访问数据库的接口。用来存放对数据库操作的方法，没有逻辑，只有增删改查。

3)  Mapper文件（XML）：由Mybaits实现，实现Dao层中的接口，包含了各种数据库的操作方法的SQL语句，主要做数据库的交互工作，实现数据的持久化。

4)  Biz接口，也叫Service层，提供业务逻辑处理，通过调用Dao中的方法来完成业务层上的操作，其目的是封装对数据库的操作；

5)  BizImpl类：业务逻辑实现，实现Biz中的接口。

6)  Controller类：起控制作用，是业务层的一部分，控制流程：取出前台界面的数据，调用BizImpl方法，转发到下一个方法或页面。

7)  Property包将固有属性从Controller中分离出来，为Controller包提供实体的默认属性，如添加项目论文时审核状态默认为"待审核"

8)  Util包为工具类，主要为Controller层服务。

9)  Template包是为了Controller层设计的，提供了实体的导出模板文件。

## Spring（\*）

### 概述

180. 对Spring的理解，项目中都用什么？怎么用的？对IOC、和AOP的理解及实现原理。 （阿里官方面经、一面3、二面） Spring的特点， （阿里一面） Spring源码 （阿里三面） Spring生命周期 （阿里二面） 介绍一下Spring （考）（美团一面）

> Spring 是一个java企业级应用的开源开发框架。Spring主要用来开发Java应用，但是有些扩展是针对构建J2EE平台的web应用。Spring 框架目标是简化Java企业级应用开发，并通过POJO为基础的编程模型促进良好的编程习惯。
>
> Spring~~处于MVC模式中的控制层~~，[它能应对需求快速的变化，其主要原因它有一种**面向切面编程（AOP）**的优势]{.underline}；其次它**提升了系统性能**，因为通过**依赖倒置机制（IoC）**，[系统中用到的对象不是在系统加载时就全部实例化，而是在调用到这个类时才会实例化该类的对象]{.underline}。这两个优秀的性能使得Spring受到许多J2EE公司的青睐，比如，阿里。
>
> **Spring的优点**：

-   降低了组件之间的耦合性，实现了软件各层之间的解耦。（*耦合度指程序模块间存在联系的紧密程度。*）

-   可以使用容易提供的众多服务，如事务管理，消息服务，日志记录等。

-   容器提供了AOP技术，利用它很容易实现如权限拦截、运行期监控等功能。

> Spring中AOP技术是设计模式中的**动态代理模式**。只需实现jdk提供的动态代理接口InvocationHandler，所有被代理对象的方法都由InvocationHandler接管实际的处理任务。面向切面编程中还要理解[切入点、切面、通知、织入]{.underline}等概念。
>
> Spring中IoC则利用了Java强大的反射机制来实现。依赖注入即**组件之间的依赖关系由容器在运行期决定**。依赖注入的方法有两种：通过构造函数注入，通过set方法注入。

181. 为什么要使用 Spring？ （考）

        72. 方便解耦，便于开发。降低了组件之间的耦合性，实现了软件各层之间的解耦。（耦合度：程序模块间存在联系的紧密程度。）将所有对象的创建和依赖关系维护都交给Spring管理。
    
        73. 可以使用容易提供的众多服务，如事务管理，消息服务，日志记录等。通过配置就完成对事务的支持，不需要手动编程。
    
        74. 容器提供了AOP技术，利用它很容易实现如权限拦截、运行期监控等功能。
    
        75. 降低javaEE API的使用难度。Spring 对javaEE开发中非常难用的一些API都提供了封装，例如JDBC，javaMail，远程调用等，使这些API应用难度大大降低。
    
        76. 方便程序的测试，Spring 对junit4支持，可以通过注解方便的测试Spring 程序。
    
        77. **方便集成各种优秀的框架**。
    
        78. Spring灵活而全面的扩展集和第三方库使开发人员可以构建几乎任何可以想象的应用程序。Spring框架的核心是控制反转（IoC）和依赖注入（DI）功能，为广泛的功能集奠定了基础。可用于为Web构建安全的，响应式的，基于云的微服务，还是为企业构建复杂的流数据流，Spring都可以提供帮助的工具。

182. 什么是 Spring 框架？为什么说Spring是轻量级的框架？

> Spring （Spring Framework）是[一种轻量级开发框架]{.underline}，旨在提高开发人员的[开发效率]{.underline}以及[系统的可维护性]{.underline}。一开始是为了解决企业应用开发的复杂性创建的，但现在已经不止应用于企业应用，可以构建J2EE平台的web应用。**高内聚，低耦合**。
>
> Spring是一个轻量级的控制反转(IoC)和面向切面(AOP)的容器框架。

-   从大小与开销两方面而言Spring都是轻量的；

-   [通过控制反转( IoC )的技术达到松耦合的目的]{.underline}，

-   提供了面向切面编程的丰富支持，允许通过分离应用的业务逻辑与系统级服务进行内聚性的开发。

-   包含并管理应用对象的配置和生命周期,这个意义上是一种容器。

183. 列举一些重要的Spring模块？ Spring 有哪些主要模块？ （考）

Spring 官网列出的 Spring 的 6 个特征：

1)  核心技术：依赖注入(DI)，AOP（面向切面编程），事件(events)，资源，i18n，验证，数据绑定，类型转换，SpEL（Spring Expression Language）。

2)  测试：模拟对象，TestContext框架，Spring MVC测试，WebTestClient。

3)  数据访问：事务，DAO支持，JDBC，ORM，封送XML。

4)  Web支持：Spring MVC和Spring WebFlux Web框架。

5)  集成：远程处理，JMS，JCA，JMX，电子邮件，任务，调度，缓存。

6)  语言：Kotlin，Groovy，动态语言。

> Spring 框架是很多模块的集合，使用这些模块可以很方便地协助我们进行开发。
>
> 5.x版本中 Web 模块的 Portlet 组件已经被废弃掉，同时增加了用于异步响应式处理的 WebFlux 组件。
>
> ![](media/image135.png){width="3.805237314085739in" height="2.7916666666666665in"}（4.x 版本）

79. Core Container：Core 组件是Spring 所有组件的核心，主要实现IoC功能。Beans 组件和 Context 组件是实现IoC和依赖注入的基础。Spring所有功能都是借助IoC实现的。

> Context模块提供框架式的Bean访问方式，其他程序可以通过Context访问Spring的Bean资源，相当于资源注入。

80. AOP：提供了面向切面的编程实现。提供了AOP（拦截器）机制，并提供常用的拦截器，供用户自定义和配置。

81. 数据访问/集成：事务，DAO支持，ORM，编组XML。

    -   JDBC：Spring对JDBC进行封装，允许JDBC使用Spring资源，并能统一管理JDBC事物，并不对JDBC进行实现。（执行sql语句）

    -   ORM（对象关系映射，Object Relational Mapping）：提供对常用的ORM框架的管理和辅助支持，支持Hibernate，ibtas，jdao等框架。本身不实现ORM。

    -   JMS ：Java消息服务

82. WEB模块：为创建Web应用程序提供支持。Spring MVC和Spring WebFlux Web框架。

> WEB模块提供对常见框架如Struts1，WEBWORK（Struts 2），JSF的支持，Spring能够管理这些框架，将Spring的资源注入给框架，也能在这些框架的前后插入拦截器。
>
> 在Spring的开发中，我们既可以用Struts也可以用Spring自己的MVC框架，相对于Struts，Spring自己的MVC框架更加简洁和方便。

83. Spring Aspects ： 该模块为与AspectJ的集成提供支持。

84. Spring Test：提供了对 JUnit 和 TestNG 测试的支持。测试 ：模拟对象，TestContext框架，Spring MVC 测试，WebTestClient。

<!-- -->

184. 设计模式是如何在Spring中体现的？Spring为什么用简单工厂模式？ （阿里三面）

<!-- -->

1)  工厂模式：Spring使用工厂模式通过BeanFactory、ApplicationContext创建bean对象。

2)  代理设计模式：Spring AOP 功能的实现。

3)  单例设计模式：Spring 中的 Bean 默认都是单例的。

4)  模板方法模式：Spring 中 jdbcTemplate、hibernateTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。

5)  包装器设计模式：项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以[根据客户的需求能够动态切换不同的数据源]{.underline}。

6)  观察者模式：Spring 事件驱动模型就是观察者模式很经典的一个应用。

7)  适配器模式：Spring AOP 的增强或通知(Advice)使用到了适配器模式、Spring MVC 中也是用到了适配器模式适配Controller。

<!-- -->

185. Spring的工作原理，控制反转是怎么实现的？自己写过滤器，过滤编码怎么实现？ （阿里官方面经）

> Spring的核心组成：IoC&DI(工厂设计)、AOP(代理设计、动态代理设计)；
>
> Spring之中针对于XML的解析处理采用的是DOM4J的实现；
>
> Anntation的时候必须要求有一个容器；

对于编码过滤需要考虑两种情况：

Struts1.x、SpringMVC、JSP+Servlet：都可以以直接通过过滤器完成；

Struts2.x：必须通过拦截器完成；

> 实现：考虑到可扩展性的配置，所以在配置文件里面设置编码，在程序运行的时候动态取得设置的编码进行操作。但是需要设置两个操作：请求编码、回应编码。

186. 框架与类库

框架一般是封装了逻辑、高内聚的，类库则是松散的工具组合

> 框架专注于某一领域，类库则是更通用的

187. 框架的源码有没有看过？ （阿里官方面经）

> 不要回答没有，即使你真的没有，你也别回答没有看过；
>
> 框架的核心思想：**反射+XML(Annotation)**

-   Struts2.X：请求交由过滤器执行，而后过滤器交给控制器完成，后面由于将跳转路径等信息都写在了配置文件或知识Annoration里面，所以还需要进行这部分内容的加载；

-   SpringMVC：它是基于方法的请求处理，所有的参数都提交到方法上，本质上还是一个DispatcherServlet；

-   Hibernate：就是反射和DOM4J解析处理流程。

### IoC与Bean配置、管理

#### IoC

188. 解释一下什么是 IoC？ （考）（美团一面）（小米一面、二面）（阿里一面）

> IoC（Inverse of Control，控制反转）是一种**设计思想**，就是 **将原本在程序中手动创建对象的控制权**，**交由Spring框架来管理**。 IoC 在其他语言中也有应用，并非 Spring 特有。 **IoC 容器是 Spring 用来实现 IoC 的载体**， **IoC 容器实际上就是个Map（key,value），Map 中存放的是各种对象**。
>
> IoC是Spring的核心。对于 Spring 框架来说，就是由 Spring 来负责控制对象的生命周期和对象间的关系。在Java开发中，IoC意味着将设计好的类交给系统去控制，而不是在类内部控制。这称为控制反转。
>
> [控制指的是当前对象对内部成员的控制权；控制反转指的是，这种控制权不由当前对象管理了，由其他（类、第三方容器）来管理]{.underline}。通俗地讲：就是把原本你自己制造，使用的对象，现在交由别人制造，而通过构造函数，setter方法或方法（这里指使用这个对象的方法）参数的方式传给你，由你使用。

![](media/image136.png){width="3.6037160979877516in" height="2.333041338582677in"}

189. 为什么要IoC？

> 将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。这样可以很大程度上简化应用的开发，大大增加了项目的**可维护性**且降低了开发难度，把应用从复杂的依赖关系中解放出来。 **IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可**，完全不用考虑对象是如何被创建出来的。 在实际项目中一个 Service 类可能有几百甚至上千个类作为它的底层，假如需要实例化这个 Service，可能每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。
>
> Spring 时代我们一般通过 XML 文件来配置 Bean，后来开发人员觉得 XML 文件来配置不太好，于是 SpringBoot 注解配置就慢慢开始流行起来。

190. 怎么实现IoC？

> 依赖注入(Dependency Injection，DI)是一种实现方式。目的是创建对象并且组装对象之间的关系。依赖注入即**组件之间的依赖关系由容器在运行期决定**，就是由IOC容器在运行期间，动态地将某种依赖关系注入到对象之中。
>
> 依赖注入的方法有两种：通过构造函数注入，通过set方法注入。
>
> 扩展： Martin Fowler：既然IOC是控制反转，那么到底是"哪些方面的控制被反转了呢？"获得依赖对象的过程被反转了。控制被反转之后，[获得依赖对象的过程由自身管理变为了由IOC容器主动注入]{.underline}。于是，他给"控制反转"取了一个更合适的名字：依赖注入（DI）。这个答案实际上给出了实现IOC的方法：注入。

![](media/image137.png){width="3.7708333333333335in" height="1.0409831583552056in"}

191. IoC的流程 IoC原理详细讲讲，源码看过么 （阿里零面、一面2）

> Spring IoC的初始化过程：

![](media/image138.png){width="6.700694444444444in" height="0.6146467629046369in"}

> Bean容器初始化

![](media/image139.png){width="6.239583333333333in" height="0.8387029746281714in"}

1)  org.springframework.beans。BeanFactory提供配置结构和基本功能，加载并初始化Bean。

2)  org.springframework.context。ApplicationContext保存了Bean对象并被广泛使用。

> 初始化时，ApplicationContext有以下方式：

a.  本地文件；

![](media/image140.png){width="5.645127952755906in" height="0.4791065179352581in"}

b.  Classpath；

![](media/image141.png){width="5.457650918635171in" height="0.4895220909886264in"}

c.  Web应用中依赖servlet或Listener。

![](media/image142.png){width="6.065277777777778in" height="1.3950612423447069in"}

#### 注入

192. IoC 与 DI 的关系

> IoC：控制权的转移，应用程序本身不负责依赖对象的创建和维护，而是由外部容器负责创建和维护(获得依赖对象的过程被反转了)

DI：由 IoC 容器在运行期间，动态地将某种依赖关系注入到对象之中

IoC 是一种设计思想，DI 是这种思想的一种实现

193. 什么是注入？

> Spring注入是指在启动Spring容器加载bean配置的时候，完成对变量的赋值行为。依赖注入即**组件之间的依赖关系由容器在运行期决定**，就是由IOC容器在运行期间，动态地将某种依赖关系注入到对象之中。

常用的两种注入方式：设值注入；构造注入。

194. Spring 常用的注入方式有哪些？ （考） 讲一下依赖注入，Spring实现注入的方式有哪些 （阿里一面）

<!-- -->

1)  setter 属性注入（设值注入）

> 在injectionService里有一个injectionDAO的**属性**，这个属性引用InjectionDAOImpl。

![](media/image143.png){width="6.54084864391951in" height="2.3747036307961507in"}

2)  构造方法注入

> 用injectionService接口创建InjectionServiceImpl实现类的实例时，构造InjectionDAOImpl，InjectionDAOImpl实现了injectionDAO接口。

![](media/image144.png){width="6.509603018372704in" height="2.3851181102362204in"}

3)  注解方式注入

#### bean

195. Bean的创建过程 （考）（美团一面）

196. 怎么让bean延迟创建 （考）（美团一面）

Spring使用一个bean的时候是同一个吗 （考）（美团一面）

197. spring Bean的装配流程（源码）（考）（小米一面）

198. 怎么配置bean？ （阿里官方面经）

> 这样的配置主要是在Spring里面，重点只有xml和annotation的扫描负责：

-   xml中直接使用\"bean\"，这样在Spring容器启动的时候就可以通过容器进行初始化；

-   annotation必须设置context命名空间，而后进行扫描包的配置。\@Componet、\@Service、\@Repository、\@Controller

![](media/image145.png){width="5.457650918635171in" height="0.44786089238845145in"}

199. Bean的定义及作用域的注解实现 将一个类声明为Spring的 bean 的注解有哪些？ Spring的自动注入注解有哪些？ IoC自动注入的注解？ （阿里官方面经）

> \@Componet、\@Service、\@Repository、\@Controller
>
> 我们一般使用 \@Autowired 注解自动装配 bean，要想把类标识成可用于 \@Autowired 注解自动装配的 bean 的类，采用以下注解可实现：

-   \@Component ：通用的注解，可标注任意类为 Spring 组件。如果一个Bean不知道属于哪个层，可以使用\@Component 注解标注。

-   \@Repository ：对应持久层即 Dao 层，主要用于数据库相关操作。

-   \@Service：对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao层。

![](media/image146.png){width="4.009915791776028in" height="0.6561679790026247in"}

-   \@Controller：对应 Spring MVC 控制层，主要用户接受用户请求并调用 Service 层返回数据给前端页面。

![](media/image147.png){width="2.8017333770778654in" height="0.9998753280839895in"}

200. Bean的配置项

<!-- -->

1)  Id：整个 IoC 容器中的唯一标识

2)  Class：具体实例化的类(必须配置项)

3)  Scope：作用域

4)  Constructor arguments：构造器参数

![](media/image148.png){width="1.6143810148731408in" height="0.22913823272090988in"}

5)  Properties：属性

![](media/image149.png){width="4.572344706911636in" height="0.20830708661417321in"}

6)  Autowiring mode：自动装配模式

7)  lazy-initialization mode：懒加载模式

8)  Initialization/destruction method：初始化/销毁 方法

![](media/image150.png){width="5.895096237970254in" height="0.41661417322834643in"}

201. Spring 支持几种 bean 的作用域？ （考）

<!-- -->

1)  singleton：bean以单例模式存在（默认选项），IoC容器中只存在一个 bean 实例；

![](media/image151.png){width="6.165895669291339in" height="0.2395538057742782in"}

2)  prototype：每次从容器调用 bean 时都会创建一个新的实例，destroy方式不生效。即每次 getBean()相当于执行 new Bean()操作；（使用 prototype需慎重，因为频繁创建和销毁 bean 会带来很大的性能开销）

> **Web 环境下的作用域**：

3)  request：每一次HTTP请求都会产生一个新的bean，该bean仅在当前request内有效。

4)  session：同一个 http session 共享一个 bean 实例；每一次HTTP请求都会产生一个新的 bean，该bean仅在当前 HTTP session 内有效。

5)  global-session：用于 portlet 容器，因为每个 portlet 有单独的 session，globalsession 提供一个全局性的 http session。

> 全局session作用域，仅仅在基于portlet的web应用中才有意义，Spring 5已经没有了。Portlet是能够生成语义代码(例如：HTML)片段的小型Java Web插件。它们基于portlet容器，可以像servlet一样处理HTTP请求。但是，与 servlet 不同，每个 portlet 都有不同的会话。

![](media/image152.png){width="5.8846806649168855in" height="3.1662707786526685in"}

202. Spring 中的 bean 是线程安全的吗？ （考） Spring 中的单例 bean 的线程安全问题了解吗？

> Spring 中的 bean 默认是单例模式，Spring 框架并没有对单例 bean 进行多线程的封装处理。
>
> 实际上大部分时候 Spring bean 无状态的（比如 dao 类），所有某种程度上来说 bean 也是安全的，但[如果 bean 有状态的话（比如 view model 对象），那就要开发者自己去保证线程安全了]{.underline}，最简单的就是改变 bean 的作用域，把"singleton"变更为"prototype（原型）"，这样请求 bean 相当于 new Bean()了，所以就可以保证线程安全了。

-   有状态就是有数据存储功能。

-   无状态就是不会保存数据。

> 大部分时候我们并没有在系统中使用多线程，所以很少有人会关注这个问题。[单例 bean 存在线程问题，主要是因为当多个线程操作同一个对象的时候，对这个对象的非静态成员变量的写操作会存在线程安全问题]{.underline}。
>
> 常见的有两种解决办法：

-   在Bean对象中尽量避免定义可变的成员变量（不太现实）。

-   在类中定义一个ThreadLocal成员变量，将需要的可变成员变量保存在 ThreadLocal 中（推荐的一种方式）。

203. Aware接口

> Spring 中提供了一些以 Aware 结尾的接口，实现了 Aware 接口的 bean 在被初始化之后可以获取相应资源

-   通过 Aware 接口，可以对 Spring 相应资源进行操作(一定要慎重)

-   为对 Spring 进行简单的扩展提供了方便的入口

204. Spring 中的 bean 生命周期 （考）（美团一面）

-   Bean 容器找到配置文件中 Spring Bean 的定义。

-   Bean 容器利用 Java Reflection API 创建一个Bean的实例。

-   如果涉及到一些属性值 利用 set()方法设置一些属性值。

-   如果 Bean 实现了[BeanNameAware]{.underline}接口，调用 setBeanName()方法，传入Bean的名字。

-   如果 Bean 实现了[BeanClassLoaderAware]{.underline}接口，调用 setBeanClassLoader()方法，传入 ClassLoader对象的实例。

-   与上面的类似，如果实现了其他 \*.Aware接口，就调用相应的方法。

-   如果有和加载这个 Bean 的 Spring 容器相关的 BeanPostProcessor 对象，执行postProcessBeforeInitialization() 方法

-   **[初始化]{.underline}**：如果Bean实现了org.springframework.beans.factory.InitializingBean接口，执行afterPropertiesSet()方法。

-   如果 Bean 在配置文件中的定义包含 init-method 属性，执行指定的方法。

-   如果有和加载这个 Bean的 Spring 容器相关的 BeanPostProcessor 对象，执行postProcessAfterInitialization() 方法

-   要**[销毁]{.underline}** Bean 时，如果 Bean 实现了 org.springframework.beans.factory.DisposableBean接口，执行 destroy() 方法。

-   要销毁 Bean 时，如果 Bean 在配置文件中的定义包含 destroy-method 属性，执行指定的方法。

![](media/image153.png){width="6.1875in" height="3.6934601924759405in"}

> 配置全局默认初始化、销毁

![](media/image154.png){width="5.155605861767279in" height="1.6039665354330708in"}

205. Spring 自动装配（autowriting） bean 有哪些方式？ （考）

-   no：默认值，表示没有自动装配，应使用显式 bean 引用进行装配。

-   byName：根据 bean 的名称（属性名）注入对象依赖项。此选项将检查容器并根据名字查找与属性完全一致的 bean，并将其与属性自动装配。

-   byType：根据类型注入对象依赖项。如果容器中存在一个与指定属性类型相同的 bean，那么将与该属性自动装配；如果存在多个该类型的 bean，那么抛出异常，并指出不能使用 byType 方式进行自动装配；如果没有找到相匹配的 bean，则什么事都不发生。

-   构造函数：通过构造函数来注入依赖项，需要设置大量的参数。与 byType 方式类似，不同之处在于它应用于构造器参数。如果容器中没有找到与构造器参数类型一致的 bean 则抛出异常。

-   autodetect：容器首先通过构造函数使用 autowire 装配，如果不能，则通过 byType 自动装配。

206. Resource

> Spring 针对资源文件的统一接口

85. UrlResource：URL 对应的资源，根据一个 URL 地址即可构建

86. ClassPathResource：获取类路径下的资源文件

87. FileSystemResource：获取文件系统里面的资源

88. ServletContextResource：ServletContext 封装的资源，用于访问 ServletContext 环境下的资源

89. InputStreamResource：针对于输入流封装的资源

90. ByteArrayResource：针对于字节数组封装的资源

<!-- -->

207. ResourceLoader

> 所有的 application context 都实现了 ResourceLoader 接口

![](media/image155.png){width="3.38499343832021in" height="0.624922353455818in"}

  **前缀**     **例子**                         **解释**
------------ -------------------------------- ---------------------------
  classpath:   classpath:com/myapp/config.xml   从 classpath 加载
  file:        file:/data/config.xml            从文件系统加载
  http:        http://myserver/logo.png         从 URL 加载
  无           /data/config.xml                 依赖于 ApplicationContext

#### 注解

208. \@Required

> 适用于 bean 属性的 setter 方法。仅仅表示，受影响的 bean 属性必须在配置时被填充，否则就会抛出一个BeanInitializationException异常。通过在 bean 定义或通过自动装配一个明确的属性值：
>
> ![](media/image156.png){width="4.22863845144357in" height="1.5102274715660542in"}
>
> \@Required 使用比较少，一般使用 \@Autowired。

209. \@Autowired的功能？ \@Autowired 的作用是什么？ （考）（阿里一面）

> \@Autowired 它可以对类成员变量、方法及构造函数进行标注，完成自动装配的工作，通过\@Autowired 的使用来消除 set/get 方法。
>
> ![](media/image157.png){width="4.259884076990376in" height="1.5206430446194226in"}
>
> 默认情况下，如果因找不到合适的 bean 将会导致 autowiring 失败抛出异常，可以通过下面的方式避免：
>
> ![](media/image158.png){width="4.5410990813648295in" height="1.489397419072616in"}

-   每个类只能有一个构造器被标记为 required=true

-   \@Autowired 的必要属性，建议使用 \@Required 注解

> 可以使用 \@Autowired 注解那些众所周知的解析依赖性接口，比如：BeanFactory, ApplicationContext, Environment, ResourceLoader, ApplicationEventPublisher, MessageSource
>
> ![](media/image159.png){width="2.99962489063867in" height="1.5518897637795275in"}
>
> 可以通过添加注解给需要该类型的数组的字段或方法，以提供 ApplicationContext 中的所有特定类型的 bean
>
> ![](media/image160.png){width="4.707744969378828in" height="1.1352744969378827in"}
>
> 可以用于装配 key 为 String 的 Map
>
> ![](media/image161.png){width="5.2910050306211724in" height="1.1665212160979876in"}
>
> 若希望数组有序，可让 bean 实现org.springframework.core.Ordered 接口或使用 \@Order注解
>
> \@Autowired 是由 BeanPostProcessor 处理的，所以不能在自己的 BeanPostProcessor 或 BeanFactoryPostProcessor 类型应用这些注解，这些类型必须通过 XML 或 \@Bean 注解加载

210. \@Qualifier

> 按类型自动装配可能多个 bean 实例的情况，可以使用 \@Qualifier 注解缩小范围(或指定唯一)，也可以用于指定单独的构造器参数或方法参数
>
> 可用于注解集合类型变量
>
> ![](media/image162.png){width="5.145190288713911in" height="3.5933005249343832in"}
>
> 在 XML 文件中实现 Qualifier：
>
> ![](media/image163.png){width="3.2391786964129485in" height="1.3956583552055992in"}
>
> 如果通过名字进行注解注入，主要使用的不是 \@Autowired (即使在技术上能够通过 \@Qualifier 指定 bean 的名字)，替代方式是使用 JSR-250 \@Resource 注解，它是通过其独特的名称定义来识别特定的目标(这是一个与所声明的类型无关的匹配过程)
>
> 因语义差异，集合或 Map 类型的 bean 无法通过 \@Autowired 来注入时，因为没有类型匹配到这样的 bean，为这些 bean 使用 \@Resource 注解，通过唯一名称引用集合或 Map 的 bean
>
> \@Autowired 适用于 fields, constructors, multi-argument methods 这些允许在参数级别使用 \@Qualifier 注解缩小范围的情况
>
> \@Resource 适用于成员变量、只有一个参数的 setter 方法，所以在目标时构造器或一个多参数方法时，最好的方式时使用 \@Qualifier
>
> 也可以定义自己的 qualifier 注解：

211. 基于Java的容器注解

<!-- -->

1)  \@Bean

> \@Bean 标识一个用于配置和初始化一个由 Spring IoC 容器管理的新对象的方法，类似于 XML 配置文件的\<bean/\>
>
> 可以在 Spring 的 \@Configuration 注解的类中使用 \@Bean 注解任何方法（仅仅是可以），在方法里面创建对象返回
>
> ![](media/image164.png){width="2.6871642607174104in" height="1.3227515310586178in"}
>
> \@Bean 默认是单例的，如果要改变作用域范围，可以再添加 \@Scope 注解

2)  \@ImportResource

> ![](media/image165.png){width="6.197142388451444in" height="3.041286089238845in"}
>
> 使用 \@ImportResource 可以代替上面 XML 配置：
>
> ![](media/image166.png){width="5.1764359142607175in" height="3.2079319772528434in"}

212. Spring 对 JSR 支持\@Resource

Spring 还支持使用 JSR-250 中的 \@Resource 注解的变量或 setter 方法

\@Resource 有一个 name 属性，并且默认 Spring 解释该值作为被注入 bean 的名称

![](media/image167.png){width="4.322376421697288in" height="1.5518897637795275in"}

> 如果没有显式指定 \@Resource 的 name，默认名称 是从属性名或 setter 方法得出
>
> 注解提供的名字被解析为一个 bean 的名称，这是由 ApplicationContext 中的 CommonAnnotationBeanPostProcessor 发现并处理的
>
> CommonAnnotationBeanPostProcessor 不仅能识别 JSR-250 中的生命周期注解 \@Resource，在Spring 2.5 中引入支持初始化回调和销毁回调，前提是 CommonAnnotationBeanPostProcessor 是在 Spring 的 ApplicationContext 中注册的

213. \@Resource与\@Autowired区别 （阿里官方面经）

> 使用Spring的自动的Annotation注解的时候经常会见到：\@Resource（个人常用）、\@Autowired ，如果想要了解两者区别，最好的做法是先认真学完了Spring依赖注入的时候讲解过的自动配置操作，在Spring里面自动配置的模式有两类：按照类型、按照名称。

1)  \@Autowired：byType，按照类型进行自动注入，缺点是[如果类型相同，则无法注入]{.underline}；

2)  \@Resource：byName，具备按照类型自动注入的特点，而后[如果现在类型相同，则可以设置一个名称]{.underline}，也就是说你使用\@Component、\@Service等注解设置自动扫描的时候可以设置一个名字，而这个名字就可在\@Resource中使用了；

> SpringBoot里面，因为其自动支持一些环境配置，如果使用的是\@Autowired，那么配置多个相同类型的Bean的话，将无法进行准确的注入操作。必须使用\@Resource完成。

214. JSR330 标准注解

从 Spring 3.0 开始支持 JSR330 标准注解(依赖注入注解)，其扫描方式与 Spring 注解一致

使用 JSR330 需要依赖 javax.inject 包

1)  \@Inject

\@Inject 等效于 \@Autowired，可以使用于类、属性、方法、构造器

2)  \@Named

如果想使用特定名称 进行依赖注入，使用 \@Named

\@Named 与 \@Component 是等效的

215. \@Component 和 \@Bean 的区别是什么？

<!-- -->

1)  作用对象不同：\@Component 注解作用于类，而\@Bean注解作用于方法。

2)  \@Component通常是通过类路径扫描来自动侦测以及自动装配到Spring容器中（我们可以使用 \@ComponentScan 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。\@Bean 注解通常是我们在标有该注解的方法中定义产生这个 bean,\@Bean告诉了Spring这是某个类的示例，当我需要用它的时候还给我。

3)  \@Bean 注解比 Component 注解的自定义性更强，而且很多地方我们只能通过 \@Bean 注解来注册bean。比如当我们引用第三方库中的类需要装配到 Spring容器时，则只能通过 \@Bean来实现。

> \@Bean注解使用示例：
>
> 上面的代码相当于下面的 xml 配置
>
> 下面这个例子是通过 \@Component 无法实现的。

216. 异常通知是哪个注解 （阿里一面）

### AOP与事务、权限控制

.Spring AOP相关 before after 织入的概念

#### AOP原理

217. 解释一下什么是 Aop？ （考）（美团一面）（小米一面、二面） Spring的aop作用 （阿里一面） aop原理和应用 （阿里二面2） 什么时候创建代理对象（？） （美团一面） 除了事务，AOP还用于哪些方面 AOP的使用场景 （小米一面、二面）

> AOP（Aspect Oriented Programming，面向切面编程），是OOP编程（面向对象）的有效补充，是**通过预编译方式**和**运行期动态代理实现程序功能的[统一维护]{.underline}的一种技术**。切面适合功能垂直的。[在运行时，动态地将代码切入到类的指定方法、指定位置上]{.underline}。
>
> 主要功能是：**日志记录**、**性能统计**、**安全控制**、**事务处理**、**异常处理**等。
>
> 使用AOP技术，可以将一些系统性相关的编程工作，独立提取出来，独立实现，然后通过切面切入进系统。从而避免了在业务逻辑的代码中混入很多的系统相关的逻辑，达到了 [将不同的关注点分离出来]{.underline}的效果。
>
> 能够将那些与业务无关，**却为业务模块所共同调用的逻辑或责任**（例如[事务处理、日志管理、权限控制]{.underline}等）封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可拓展性（增加功能时很方便）和可维护性。

![](media/image171.png){width="2.8645833333333335in" height="1.722711067366579in"}

![](media/image172.png){width="2.8433945756780403in" height="1.8018580489938758in"}

> Spring AOP就是基于**动态代理**的，如果要代理的对象实现了某个接口，那么Spring AOP会使用JDK Proxy，去创建代理对象，而对于没有实现接口的对象，就无法使用 JDK Proxy 去进行代理了，这时候Spring AOP会使用Cglib ，这时候Spring AOP会使用 Cglib 生成一个被代理对象的子类来作为代理，如下图所示：

![](media/image173.png){width="6.354166666666667in" height="2.952283464566929in"}

> 也可以使用 **AspectJ**。Spring AOP 已经集成了AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。

218. Spring 框架中 AOP 的用途

-   提供了**声明式的企业服务**，特别是 EJB 的替代服务的声明。

-   **允许用户定制自己的切面**，以完成 OOP 与 AOP 的互补使用。

219. AOP 实现方式

> 声明切面，即切在某方法之前、之后或前后都执行。

1)  预编译：AspectJ

2)  运行期动态代理（JDK 动态代理，CGLib 动态代理）：SpringAOP， JbossAOP

<!-- -->

220. Spring AOP 和 AspectJ AOP 有什么区别？

-   Spring AOP 属于**运行时增强**，而 AspectJ 是**编译时增强**。 Spring AOP 基于代理(Proxying)，而 AspectJ 基于字节码操作(Bytecode Manipulation)。

-   Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。AspectJ 相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单。

-   如果切面比较少，那么两者性能差异不大。当切面很多，最好选择 AspectJ ，它比Spring AOP 快很多。

221. Spring 的 AOP 实现方式： aop代码层如何实现 （阿里一面）（美团一面）

    -   纯 java 实现，无需特殊大的编译过程，不需要控制类加载器层次
    
    -   目前只支持方法执行连接点(通知 Spring Bean 的方法执行)
    
    -   不是为了提供最完整的 AOP 实现，而是侧重于提供一种 AOP 实现和 Spring IoC 容器之间的整合，用于帮助解决企业应用中的常见问题
    
    -   Spring AOP 不会与 AspectJ 竞争，不会提供综合全面的 AOP 解决方案

222. 有接口和无接口的 Spring AOP 实现区别

    -   Spring AOP 默认使用标准的 Jave SE 动态代理作为 AOP 代理，这使得任何接口(或者接口集)都可以被代理
    
    -   Spring AOP 中也可以使用 CGLIB 代理(如果一个业务对象并没有实现一个接口)

223. 不通过Spring，如何实现AOP 抛开Spring来说，如何自己实现Spring AOP?

> Spring AOP的实现是动态代理模式，需要在运行时生成代理对象，因为需要进行类扫描，看看哪些个类有切面需要生成代理对象。
>
> 动态代理模式的实现方式：JDK动态代理、cglib。

-   JDK动态代理：仅对接口有效。主函数的代码，应该放在IOC容器初始化中，扫描包，去看看哪些个类需要生成代理对象，然后构造代理对象到容器中。然后在invoke方法里，把统计费用的逻辑改成切面的逻辑。

> JDK动态代理生成一个实现相应接口的代理类。但是Spring又不是只能通过接口注入。
>
> Spring的\@Autowired是通过声明的类型去容器里找符合的对象然后注进来的，接口是类型，类也是类型。所以，[JDK动态代理针对直接注入class类型的，就代理不了]{.underline}。

-   Cglib：根据当前的类，动态生成一个子类，在子类中织入切面逻辑。然后使用子类对象代理父类对象。"代理模式，不要拘泥于接口"。织入成功的，都是子类能把父类覆盖的方法。所以cglib也不是万能的，方法是final的，子类重写不了，它当然也无计可施了。

224. 动态代理是怎么实现的？ 动态代理的实现方式，有什么区别？ （考）（美团一面） 讲一下动态代理细节 （阿里一面2）（阿里官方面经） 比较jdk动态代理和cglib的性能。（阿里一面2）

> Java 中实现动态的方式：JDK 中的反射机制生成动态代理 和 Java类库 CGLib。
>
> **JDK代理必须要提供接口**，而CGLIB则不需要，可以直接代理类。下面分别举例说明。

225. 实现动态代理方式：利用JDK反射机制生成代理 （考）（阿里官方面经）

> **直接使用Invocation Handler接口进行实现，同时利用Proxy类设置动态请求对象**；

Java 实现动态代理主要涉及以下几个类：

-   java.lang.reflect.**Proxy**:生成代理类的主类，通过 Proxy 类生成的代理类都继承了 Proxy 类，即 DynamicProxyClass extends Proxy。

-   java.lang.reflect.**InvocationHandler**："调用处理器"，我们动态生成的代理类需要完成的具体内容需要自己定义一个类，而这个类必须实现 InvocationHandler 接口。

> Java实现动态代理的大致步骤如下：

1)  [定义一个委托类和公共接口]{.underline}。

2)  [自己定义一个类（调用处理器类，即实现 InvocationHandler 接口）]{.underline}，目的是指定运行时将生成的代理类需要完成的具体任务（包括Preprocess和Postprocess），即代理类调用任何方法都会经过这个调用处理器类。

3)  **生成代理对象**（当然也会生成代理类），需要为他指定：委托对象；实现的一系列接口；调用处理器类的实例。因此可以看出[一个代理对象对应一个委托对象，对应一个调用处理器实例]{.underline}。

<!-- -->

226. 使用CGLIB代理 （考）（阿里官方面经）

避免对于"**代理设计模式需要使用接口实现**"的限制。需要引入CGLIB相关Jar包。

#### AOP术语

227. 切入点、切面、通知、织入 （考）切面的含义 （阿里一面）

![](media/image181.png){width="3.197516404199475in" height="2.2288877952755906in"}

1.  切面 (Aspect)：**一个关注点的模块化**，这个关注点可能会横切多个对象。关注点有事务、日志等。切面是通知和切入点的结合。通知和切点共同定义了切面的全部内容：它是什么，在何时和何处完成其功能。

2.  连接点 (Joinpoint)：**程序执行过程中某个特定的点**。和方法有关的前前后后都是连接点。

> 应用可能有数以千计的时机应用通知。这些时机被称为连接点。连接点是在应用执行过程中能够插入切面的一个点。这个点可以是调用方法时、抛出异常时、甚至修改一个字段时。切面代码可以利用这些点插入到应用的正常流程之中，并添加新的行为。

3.  通知、增强处理 (Advice)：在切面的某个特定的连接点上执行的动作。通知定义了切面是**什么**以及**何时**使用。除了描述切面要完成的工作，通知还解决了何时执行这个工作的问题。它应该应用在某个方法被调用之前?之后?之前和之后都调用?还是只在方法抛出异常时调用?

4.  切点 (Pointcut)：**匹配连接点的断言**，在 AOP 中通知(Advice)和一个切入点表达式关联。如果说通知定义了切面的"**什么**\"和"**何时**"的话，那么切点就定义了"**何处**\"。切点的定义会匹配通知所要织入的一个或多个连接点。通常使用明确的类和方法名称，或是利用正则表达式定义所匹配的类和方法名称来指定这些切点。有些AOP框架允许创建动态的切点，可以根据运行时的决策(比如方法的参数值)来决定是否应用通知。

5.  引入 (Introduction)：在不修改类代码的前提下，为类添加新的方法和属性。

6.  目标对象 (Target Object)：被一个或者多个切面所通知的对象。

7.  AOP 代理 (AOP Proxy)：AOP 框架创建的对象，用来实现切面契约(aspect contract)(包括通知方法执行等功能)

8.  织入 (Weaving)：把切面连接到其它的应用程序类型或者对象上，并创建一个被通知的对象。分为：编译时织入、类加载时织入、执行时织入。Spring采用的是运行时。

<!-- -->

228. Advice 的类型

<!-- -->

1)  前置通知 (Before advice)：在某连接点之前执行的通知，但不能阻止连接点前的执行(除非它抛出一个异常)

2)  返回后通知 (After returning advice)：在某连接点正常完成后执行的通知

3)  抛出异常通知 (After throwing advice)：在方法抛出异常退出时执行的通知

4)  后通知 (After (finally) advice)：当某连接点退出的时候执行的通知(不论是正常返回还是异常退出)

5)  环绕通知 (Around advice)：包围一个连接点的通知

<!-- -->

229. 织入分类

> 织入是把切面应用到目标对象并创建新的代理对象的过程。切面在指定的连接点被织入到目标对象中。在目标对象的生命周期里有多个点可以进行织入：

-   编译期：切面在目标类编译时被织入。需要特殊的编译器。AspectJ的织入编译器就是以这种方式织入切面的。

-   类加载期：切面在目标类加载到JVM时被织入。需要特殊的类加载器(ClassLoader)，它可以在目标类被引入应用之前增强该目标类的字节码。AspectJ 5的加载时织入(load-time weaving, LTW) 就支持以这种方式织入切面。.

-   运行期：切面在应用运行的某个时刻被织入。一般情况下，在织入切面时，AOP容器会为目标对象动态地创建一个代理对象。Spring AOP就是以这种方式织入切面的。

#### AspectJ

230. Spring 对 AspectJ 的支持

\@AspectJ 的风格类似纯 java 注解的普通 java 类

Spring 可以使用 AspectJ 来做切入点解析

AOP 的运行时仍旧是纯的 Spring AOP，对 AspectJ 的编译器或者织入无依赖性

231. Spring 中配置 \@AspectJ

        91. 对 \@AspectJ 支持可以使用 XML 或 Java 风格的配置
    
        92. 确保 AspectJ 的 aspectjweaver.jar (1.6.8或更高版本) 库包含在应用程序的 classpath 中

#### 事务实现

232. 事务：

> 满足ACID特性的一组操作：原子性、一致性、隔离性、持久性

233. Spring 事务实现方式有哪些？ （考）

<!-- -->

1)  编程式事务，在代码中硬编码。(不推荐使用) 提供编码的形式管理和维护事务。

2)  声明式事务，在配置文件中配置（推荐使用），声明式事务也有两种实现方式。

    a.  基于 xml 配置文件的方式
    
    b.  基于注解的声明方式（在类上添加 \@Transaction 注解）

#### 事务隔离

234. 说一下 Spring 的事务隔离？ （考） Spring事务隔离级别 （小米一面）

> TransactionDefinition 接口中定义了五个表示隔离级别的常量：
>
> Spring 有五大隔离级别，默认值为 ISOLATION\_DEFAULT（使用数据库的设置），其他四个隔离级别和数据库的隔离级别一致：

1)  TransactionDefinition.ISOLATION\_DEFAULT：使用后端数据库默认的隔离级别，Mysql 默认采用 REPEATABLE\_READ隔离级别，Oracle 默认采用 READ\_COMMITTED级别

2)  TransactionDefinition.ISOLATION\_READ\_UNCOMMITTED：未提交读，最低隔离级别、事务未提交前，就可被其他事务读取（会出现幻读、脏读、不可重复读）；

3)  TransactionDefinition.ISOLATION\_READ\_COMMITTED：提交读，一个事务提交后才能被其他事务读取到（可以阻止脏读，但仍会造成幻读、不可重复读），SQL server 的默认级别；

4)  TransactionDefinition.ISOLATION\_REPEATABLE\_READ：可重复读，保证多次读取同一个数据时，其值都和事务开始时候的内容是一致，禁止读取到别的事务未提交的数据（会造成幻读），[MySQL 的默认级别]{.underline}；

5)  TransactionDefinition.ISOLATION\_SERIALIZABLE：序列化，代价最高最可靠的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰。该隔离级别能防止脏读、不可重复读、幻读。

-   脏读 ：表示一个事务能够读取另一个事务中还未提交的数据。比如，某个事务尝试插入记录 A，此时该事务还未提交，然后另一个事务尝试读取到了记录 A。

-   不可重复读 ：是指在一个事务内，多次读同一数据。

-   幻读 ：指同一个事务内多次查询返回的结果集不一样。比如同一个事务 A 第一次查询时候有 n 条记录，但是第二次同等条件下查询却有 n+1 条记录，这就好像产生了幻觉。发生幻读的原因也是另外一个事务新增或者删除或者修改了第一个事务结果集里面的数据，同一个记录的数据内容被修改了，所有数据行的记录就变多或者变少了。

235. Spring 事务中哪几种事务传播行为? 事务的传播属性 （考）（阿里官方面经） （小米一面）

> 在Transaction Definition接口中定义了七个事务传播行为：
>
> 支持当前事务的情况：

-   TransactionDefinition.PROPAGATION\_REQUIRED：如果当前存在事务，则加入（支持）该事务；如果当前没有事务，则创建（开启）一个新的事务。

-   TransactionDefinition.PROPAGATION\_SUPPORTS：如果当前存在事务，则加入（支持）该事务；如果当前没有事务，则以非事务的方式继续运行。但是对于事务同步的事务管理器，PROPAGATION SUPPORTS与不使用事务有少许不同；

-   TransactionDefinition.PROPAGATION\_MANDATORY： 如果当前存在事务，则加入（支持）该事务；如果当前没有事务，则抛出异常。（mandatory：强制性）

> 不支持当前事务的情况：

-   TransactionDefinition.PROPAGATION\_REQUIRES\_NEW： 总是开启一个新的事务，如果一个事务已经存在，则将这个存在的事务挂起。

-   TransactionDefinition.PROPAGATION\_NOT\_SUPPORTED： 以非事务方式运行，如果当前存在事务，则把当前事务挂起。

-   TransactionDefinition.PROPAGATION\_NEVER： 以非事务方式运行，如果当前存在事务，则抛出异常。

其他情况：

-   TransactionDefinition.PROPAGATION\_NESTED： 如果当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行；如果当前没有事务，则按Transaction Definition.PROPAGATION\_REQUIRED属性执行。

236. \@Transactional(rollbackFor = Exception.class)注解了解吗？

> Exception分为运行时异常RuntimeException和非运行时异常。事务管理对于企业应用来说是至关重要的，即使出现异常情况，它也可以保证数据的一致性。
>
> 当\@Transactional注解作用于类上时，该类的所有 public 方法将都具有该类型的事务属性，同时，我们也可以在方法级别使用该标注来覆盖类级别的定义。如果类或者方法加了这个注解，那么这个类里面的方法抛出异常，就会回滚，数据库里面的数据也会回滚。
>
> 在\@Transactional注解中如果不配置rollbackFor属性，那么事物只会在遇到RuntimeException的时候才会回滚，加上rollbackFor=Exception.class，可以让事物在遇到非运行时异常时也回滚。

### JPA整合

237. 如何使用JPA在数据库中非持久化一个字段？

> 假如我们有有下面一个类：
>
> 如果我们想让secrect 这个字段不被持久化，也就是不被数据库存储怎么办？我们可以采用下面几种方法：（一般使用后面两种方式比较多，我个人使用注解的方式比较多。）

## Spring MVC（\*）

#### 概述

238. 说说自己对于 Spring MVC 了解?

        1.  Model1时代：整个 Web 应用几乎全部用 JSP 页面组成，只用少量的 JavaBean 来处理数据库连接、访问等操作。
    
        2.  Model2时代：Java Bean(Model)+ JSP（View）+Servlet（Controller）

> Model2 模式下还存在很多问题，Model2的抽象和封装程度还远远不够，使用Model2进行开发时不可避免地会重复造轮子，这就大大降低了程序的可维护性和复用性。于是很多JavaWeb开发相关的 MVC 框架应运而生比如Struts2，但是 Struts2 比较笨重。随着 Spring 轻量级开发框架的流行，Spring 生态圈出现了 Spring MVC 框架， Spring MVC 是当前最优秀的 MVC 框架。相比于 Struts2 ， [Spring MVC 使用更加简单和方便，开发效率更高，并且 Spring MVC 运行速度更快]{.underline}。
>
> MVC 是一种设计模式，Spring MVC 是一款很优秀的 MVC 框架。Spring MVC 可以帮助我们进行更简洁的Web层的开发，并且它天生与 Spring 框架集成。Spring MVC 下我们一般把后端项目分为 Service层（处理业务）、Dao层（数据库操作）、Entity层（实体类）、Controller层(控制层，返回数据给前台页面)。
>
> ![](media/image184.png){width="6.802083333333333in" height="2.8197583114610674in"}

239. Spring mvc 有哪些组件？ （考）

<!-- -->

1)  前置控制器 DispatcherServlet。

2)  映射控制器 HandlerMapping。

3)  处理器 Controller。

4)  模型和视图 ModelAndView。

5)  视图解析器 ViewResolver。

#### 处理流程、工作原理

240. 说一下 Spring mvc 运行流程？ （考） 说一下你理解的MVC，SpringMVC处理流程，拦截请求怎么实现？ （阿里一面） SpringMVC的执行原理和流程 （阿里零面、一面） springMVC的运行原理，从一个请求进入到返回的过程 （小米一面）

-   Spring mvc 先将请求发送给 DispatcherServlet。

-   DispatcherServlet 查询一个或多个 HandlerMapping，找到处理请求的 Controller。

-   DispatcherServlet 再把请求提交到对应的 Controller。

-   Controller 进行业务逻辑处理后，会返回一个ModelAndView。

-   Dispathcher 查询一个或多个 ViewResolver 视图解析器，找到 ModelAndView 对象指定的视图对象。

-   视图对象负责渲染返回给客户端。

![2-springmvc](media/image132.png){width="6.291666666666667in" height="1.71875in"}

1)  客户端（浏览器）发送请求，直接请求到 DispatcherServlet。

2)  DispatcherServlet 根据请求信息调用 HandlerMapping，解析请求对应的 Handler()。

3)  解析到对应的 Handler（也就是Controller 控制器）后，开始由 HandlerAdapter 适配器处理。

4)  HandlerAdapter 会根据Handler来调用真正的处理器处理请求，并处理相应的业务逻辑。

5)  处理器处理完业务后，会返回一个 ModelAndView 对象，Model 是返回的数据对象，View 是个逻辑上的 View。

6)  ViewResolver 会根据逻辑 View 查找实际的 View。

7)  DispaterServlet 把返回的 Model 传给 View（视图渲染）。

8)  把 View 返回给请求者（浏览器）。

<!-- -->

241. \@RequestMapping 的作用是什么？ （考）

> \@RequestMapping是一个用来处理请求地址映射的注解，可用于类或方法上。用于类，表示类中的所有响应请求的方法都是以该地址作为父路径。\@RequestMapping注解有六个属性：

1)  value:指定请求的实际地址，指定的地址可以是URI Template模式。

2)  method:指定请求的method类型，GET、POST、PUT、DELETE等。

3)  consumes:指定处理请求的提交内容类型（Content-Type），例如application/json,text/html。

4)  produces:指定返回的内容类型，仅当request请求头中的（Accept）类型中包含该指定类型才返回。

5)  params:指定request中必须包含某些参数值才让该方法处理。

6)  headers

<!-- -->

242. \@RestController 与 \@Controller

> \@Controller **返回一个页面**
>
> 单独使用 \@Controller 不加 \@ResponseBody的话一般使用在要返回一个视图的情况，这种情况属于比较传统的Spring MVC 的应用，对应于前后端不分离的情况。
>
> ![](media/image185.png){width="3.5520833333333335in" height="2.16374343832021in"}
>
> \@RestController **返回JSON 或 XML 形式数据**
>
> 但\@RestController只返回对象，对象数据直接以 JSON 或 XML 形式写入 HTTP 响应(Response)中，这种情况属于 RESTful Web服务，这也是目前日常开发所接触的最常用的情况（前后端分离）。
>
> ![](media/image186.png){width="4.072916666666667in" height="1.9410640857392827in"}
>
> \@Controller +\@ResponseBody **返回JSON 或 XML 形式数据**
>
> 如果你需要在Spring4之前开发 RESTful Web服务的话，你需要使用\@Controller 并结合\@ResponseBody注解，也就是说\@Controller +\@ResponseBody= \@RestController（Spring 4 之后新加的注解）。
>
> \@ResponseBody 注解的作用是将 Controller 的方法返回的对象通过适当的转换器转换为指定的格式之后，写入到HTTP 响应(Response)对象的 body 中，通常用来返回 JSON 或者 XML 数据，返回 JSON 数据的情况比较多。

243. 除了\@ResponseBody，controller层如何标准返回给前端所要的数据类型？你会怎么实现？ （阿里零面）

244. SpringMVC的一个实现，然后讲讲自己的SpringMVC有哪些缺点，如何处理参数 （阿里一面）

245. SpringMVC返回值，使用SpringMVC的时候我看到两种风格的开发，一种是控制层的方法返回值类型主要是ModelAndView（就如我们的BSM项目），另外一种风格是返回值Spring类型，在开发中要怎么取舍？ （阿里官方面经）

> 从简单来讲就是ModelAndView，如果只是做一个过渡，符合MVC标准设计，可能有人就会认为返回ModelAndView需要实例化新对象太麻烦了，就直接返回String。
>
> MVC的设计角度在于你需要通过控制层传输相应的对象信息给显示层来进行显示，而且业务层也会返回Map数据，这个时候就希望可以把Map的数据直接传递到JSP里面，这样的话使用ModelAndView就很简单。最关键的是ModelAndView整体的处理来讲是很容易的，只是一个跳转的页面路径，以及相关的属性设置，可以帮助一些基础不牢固的人员不使用错误的属性范围，例如：request。（如果要想更好的理解细节，那么就必须在项目之中感受。）

## SpringBoot

246. 什么是 SpringBoot？ （考）

> Spring Boot 是为 Spring 服务的，是用来简化新 Spring 应用的初始搭建以及开发过程的。Spring Boot是Spring开源组织下的子项目，是Spring组件一站式解决方案，主要是简化了使用Spring的难度，简省了繁重的配置，提供了各种启动器，开发者能快速上手。

247. 为什么要用SpringBoot？ （考）

-   为了解决java开发中的，繁多的配置、底下的开发效率，复杂的部署流程，和第三方技术集成难度大的问题，产生了Spring boot。

-   Springboot 使用 "习惯优于配置"的理念让项目快速运行起来，使用Springboot很容易创建一个独立运行的jar，内嵌servlet容器

-   Springboot的核心功能一：独立运行Spring项目，Springboot可以以jar包的形式独立运行，运行一个Springboot项目只需要 java -jar xxx.jar 来运行

-   Springboot的核心功能二：内嵌servlet容器，可以内嵌tomcat，接天jetty，或者undertow，这样我们就可以不用war包形式部署项目

-   Springboot的核心功能三，提供starter简化maven配置，Spring提供了一系列starter pom 来简化maven的依赖加载， 当使用了 Spring-boot-starter-web时，会自动加载所需要的依赖包

-   Springboot的核心功能三：自动配置Spring sprintboot 会根据在类路径的jar包，类，为jar包中的类自动配置bean，这样会极大的减少使用的配置，会根据启动类所在的目录，自动配置bean

248. SpringBoot核心配置文件是什么？ （考）

> Spring boot 核心的两个配置文件：

-   bootstrap (. yml 或者 . properties)：boostrap 由父 ApplicationContext 加载的，比 applicaton 优先加载，且 boostrap 里面的属性不能被覆盖；

-   application (. yml 或者 . properties)：用于 Spring boot 项目的自动化配置。

249. SpringBoot配置文件有哪几种类型？它们有什么区别？ （考）

配置文件有 . properties 格式和 . yml 格式，它们主要的区别是书法风格不同。

. properties 配置如下：

. yml 配置如下：

. yml 格式不支持 \@PropertySource 注解导入。

250. Spring boot 有哪些方式可以实现热部署？ （考）

-   使用 devtools 启动热部署，添加 devtools 库，在配置文件中把 Spring. devtools. restart. enabled 设置为 true；

-   使用 Intellij Idea 编辑器，勾上自动编译或手动重新编译。

251. SpringBoot Starter原理 （阿里零面）（考）（字节一面）

252. springboot的bean放在那里 （考）（小米二面）

253. springBoot启动过程（只说了\@SpringbootApplication的作用） （考）（小米二面）

254. springboot的bean的注入方式（知道三种，但只清楚自动注入） （考）（小米二面）

255. 如果现在需要一个注入一个第三方库的方法，但不能直接拿到类应该怎么注入（不知道，面试官说XML注入就可以） （考）（小米二面）

## SpringCloud

256. 什么是 Spring cloud？ （考） Spring cloud介绍 （阿里一面）

> Spring cloud 是一系列框架的有序集合。它利用 Spring boot 的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等，都可以用 Spring boot 的开发风格做到一键启动和部署。

257. Spring cloud 断路器的作用是什么？ （考）

> 在分布式环境下，特别是微服务结构的分布式系统中， 一个软件系统调用另外一个远程系统是非常普遍的。这种远程调用的被调用方可能是另外一个进程，或者是跨网路的另外一台主机, 这种远程的调用和进程的内部调用最大的区别是，远程调用可能会失败，或者挂起而没有任何回应，直到超时。更坏的情况是， 如果有多个调用者对同一个挂起的服务进行调用，那么就很有可能的是一个服务的超时等待迅速蔓延到整个分布式系统，引起连锁反应， 从而消耗掉整个分布式系统大量资源。最终可能导致系统瘫痪。
>
> 断路器（Circuit Breaker）模式就是为了防止在分布式系统中出现这种瀑布似的连锁反应导致的灾难。
>
> 一旦某个电器出问题，为了防止灾难，电路的保险丝就会熔断。断路器类似于电路的保险丝， 实现思路非常简单，可以将需要保护的远程服务嗲用封装起来，在内部监听失败次数， 一旦失败次数达到某阀值后，所有后续对该服务的调用，断路器截获后都直接返回错误到调用方，而不会继续调用已经出问题的服务， 从而达到保护调用方的目的, 整个系统也就不会出现因为超时而产生的瀑布式连锁反应。

258. Spring cloud 的核心组件有哪些？ （考） SpringCloud都有哪些组件？和阿里开源的有什么区别？如果要用，怎么选择？ （阿里三面）

> Spring Cloud由众多子项目组成，如Spring Cloud Config、Spring Cloud Netflix、Spring Cloud Consul 等，提供了搭建分布式系统及微服务常用的工具，如配置管理、服务发现、断路器、智能路由、微代理、控制总线、一次性token、全局锁、选主、分布式会话和集群状态等，满足了构建微服务所需的所有解决方案。

1)  服务发现------Netflix Eureka

2)  客服端负载均衡------Netflix Ribbon

3)  断路器------Netflix Hystrix

4)  服务网关------Netflix Zuul

5)  分布式配置------Spring Cloud Config

<!-- -->

259. 服务注册与发现概念 （阿里一面）

## mybatis

![](media/image189.png){width="2.4163648293963256in" height="3.707869641294838in"}

260. 什么是ORM？ （考）

261. sqlSeesionFactory说一下 源码 （小米一面）

自己配置数据源 （小米一面）

262. 使用MyBatis的步骤 （阿里一面）

263. 

#### 标签

264. mybatis的xml有什么标签 （阿里零面） Xml 映射文件中，除了常见的 select\|insert\|updae\|delete 标签之外，还有哪些标签？

> 还有很多其他的标签，\<resultMap\>、\<parameterMap\>、\<sql\>、\<include\>、\<selectKey\>，加上动态 sql 的 9 个标签，trim\|where\|set\|foreach\|if\|choose\|when\|otherwise\|bind等，其中为 sql 片段标签，通过\<include\>标签引入 sql 片段，\<selectKey\>为不支持自增的主键生成策略标签。

最佳实践中，通常一个 Xml 映射文件，都会写一个 Dao 接口与之对应，请问，这个 Dao 接口的工作原理是什么？Dao 接口里的方法，参数不同时，方法能重载吗？

注：这道题也是京东面试官面试我时问的。

答：Dao 接口，就是人们常说的 Mapper接口，接口的全限名，就是映射文件中的 namespace 的值，接口的方法名，就是映射文件中MappedStatement的 id 值，接口方法内的参数，就是传递给 sql 的参数。Mapper接口是没有实现类的，当调用接口方法时，接口全限名+方法名拼接字符串作为 key 值，可唯一定位一个MappedStatement，举例：com.mybatis3.mappers.StudentDao.findStudentById，可以唯一找到 namespace 为com.mybatis3.mappers.StudentDao下面id = findStudentById的MappedStatement。在 Mybatis 中，每一个\<select\>、\<insert\>、\<update\>、\<delete\>标签，都会被解析为一个MappedStatement对象。

Dao 接口里的方法，是不能重载的，因为是全限名+方法名的保存和寻找策略。

Dao 接口的工作原理是 JDK 动态代理，Mybatis 运行时会使用 JDK 动态代理为 Dao 接口生成代理 proxy 对象，代理对象 proxy 会拦截接口方法，转而执行MappedStatement所代表的 sql，然后将 sql 执行结果返回。

#### 插件

265. 简述 Mybatis 的插件运行原理，以及如何编写一个插件。 （考）

> Mybatis 仅可以编写针对 ParameterHandler、ResultSetHandler、StatementHandler、Executor 这 4 种接口的插件，Mybatis 使用 JDK 的动态代理，为需要拦截的接口生成代理对象以实现接口方法拦截功能，每当执行这 4 种接口对象的方法时，就会进入拦截方法，具体就是 InvocationHandler 的 invoke()方法，当然，只会拦截那些你指定需要拦截的方法。
>
> 实现 Mybatis 的 Interceptor 接口并复写 intercept()方法，然后在给插件编写注解，指定要拦截哪一个接口的哪些方法即可，记住，别忘了在配置文件中配置你编写的插件。

Mybatis 执行批量插入，能返回数据库主键列表吗？

注：我出的。

答：能，JDBC 都能，Mybatis 当然也能。

Mybatis 动态 sql 是做什么的？都有哪些动态 sql？能简述一下动态 sql 的执行原理不？

注：我出的。

答：Mybatis 动态 sql 可以让我们在 Xml 映射文件内，以标签的形式编写动态 sql，完成逻辑判断和动态拼接 sql 的功能，Mybatis 提供了 9 种动态 sql 标签 trim\|where\|set\|foreach\|if\|choose\|when\|otherwise\|bind。

其执行原理为，使用 OGNL 从 sql 参数对象中计算表达式的值，根据表达式的值动态拼接 sql，以此来完成动态 sql 的功能。

Mybatis 是如何将 sql 执行结果封装为目标对象并返回的？都有哪些映射形式？

注：我出的。

答：第一种是使用\<resultMap\>标签，逐一定义列名和对象属性名之间的映射关系。第二种是使用 sql 列的别名功能，将列别名书写为对象属性名，比如 T\_NAME AS NAME，对象属性名一般是 name，小写，但是列名不区分大小写，Mybatis 会忽略列名大小写，智能找到与之对应对象属性名，你甚至可以写成 T\_NAME AS NaMe，Mybatis 一样可以正常工作。

有了列名与属性名的映射关系后，Mybatis 通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。

Mybatis 能执行一对一、一对多的关联查询吗？都有哪些实现方式，以及它们之间的区别。

注：我出的。

答：能，Mybatis 不仅可以执行一对一、一对多的关联查询，还可以执行多对一，多对多的关联查询，多对一查询，其实就是一对一查询，只需要把 selectOne()修改为 selectList()即可；多对多查询，其实就是一对多查询，只需要把 selectOne()修改为 selectList()即可。

关联对象查询，有两种实现方式，一种是单独发送一个 sql 去查询关联对象，赋给主对象，然后返回主对象。另一种是使用嵌套查询，嵌套查询的含义为使用 join 查询，一部分列是 A 对象的属性值，另外一部分列是关联对象 B 的属性值，好处是只发一个 sql 查询，就可以把主对象和其关联对象查出来。

那么问题来了，join 查询出来 100 条记录，如何确定主对象是 5 个，而不是 100 个？其去重复的原理是\<resultMap\>标签内的\<id\>子标签，指定了唯一确定一条记录的 id 列，Mybatis 根据列值来完成 100 条记录的去重复功能，\<id\>可以有多个，代表了联合主键的语意。

同样主对象的关联对象，也是根据这个原理去重复的，尽管一般情况下，只有主对象会有重复记录，关联对象一般不会重复。

举例：下面 join 查询出来 6 条记录，一、二列是 Teacher 对象列，第三列为 Student 对象列，Mybatis 去重复处理后，结果为 1 个老师 6 个学生，而不是 6 个老师 6 个学生。

t\_id t\_name s\_id

\| 1 \| teacher \| 38 \| \| 1 \| teacher \| 39 \| \| 1 \| teacher \| 40 \| \| 1 \| teacher \| 41 \| \| 1 \| teacher \| 42 \| \| 1 \| teacher \| 43 \|

266. MyBatis通过接口没有实现就能实现一些增删改查操作，背后原理？如果自己设计，大概是怎样的流程？ （阿里一面）

267. MyBatis如何防止SQL注入 （阿里一面）

268. mybatis如何进行类型转换 （阿里零面）

269. MyBatis的原理分析 （阿里一面）

    a.  读取核心配置文件并返回InputStream流对象。

> 配置文件mybatis-config.xml
>
> 环境元素体中包含了事务管理和mapper元素。mapper元素则是包含一组mapper映射器（这些mapper的XML文件包含了SQL代码和映射定义信息）。
>
> BookMapper.xml

b.  根据InputStream流对象解析出Configuration对象，然后创建SqlSessionFactory工厂对象

c.  根据类别属性从工厂中创造SqlSessionFactorySqlSession

d.  从SqlSession中调用Executor执行数据库操作&&生成具体的SQL指令

e.  对执行结果进行二次封装

f.  提交与事务

<!-- -->

270. 在MyBatis的sql语句中使用if判断传递过来的某参数是不是null是有效的，但是却不能判断空字符串" '''' "。 （阿里官方面经）

> 动态SQL是依靠配置实现的，它只能够判断null。你可以在业务层的处理上追加一些判断功能，例如：如果发现有内容为空字符串( ''''),那么你就为其设置null。
>
> 动态SQL很有帮助。

271. MyBatis和Hibernate中的set方法 （阿里官方面经）

> MyBatis开发里面主要的核心是要求用户自己来定义使用的SQL语句。而Hibernate特点由于其要考虑其可移植性的问题，所以在Hibernate处理之中，它所需要考虑的就是一个自动生成SQL问题。
>
> 现在所有问题都放在了POJO类（VO）、Hibernate下，如果该POJO类的对象处于持久态状态，那么每一次调用setter方法都会更新数据（如果你的事务是手工控制，则在若干个setter调用后才会发出更新操作），而MyBatis没有这样的功能，因为Hibernate之中搞的这种对象的状态设计有些糟糕，而且这也是Hibernate本身性能低的原因。追究其起源，主要是因为传统的EJB(EntityBean)影响。

272. 谈谈Hibernate与iBatis的区别，哪个性能会更高一些 （阿里官方面经）

<!-- -->

1)  Hibernate偏向于对象的操作达到数据库相关操作的目的；而iBatis更偏向于SQL语句的优化。

2)  Hibernate的使用的查询语句是自己的HQL，而iBatis则是标准的SQL语句。

3)  Hibernate相对复杂，不易学习；iBatis类似SQL语句，简单易学。

> **性能方面**：

4)  如果系统数据处理量巨大，性能要求极为苛刻时，往往需要人工编写高性能的SQL语句或存错过程，此时iBatis具有更好的可控性，因此性能优于Hibernate。

5)  同样的需求下，由于Hibernate可以自动生成HQL语句，而iBatis需要手动写SQL语句，此时采用Hibernate的效率高于iBatis。

<!-- -->

273. MyBatis 和 hibernate 的区别有哪些？ （考）

-   灵活性：MyBatis更加灵活，自己可以写 SQL 语句，使用起来比较方便。

-   可移植性：MyBatis可移植性比较差。MyBatis有很多自己写的 SQL，因为每个数据库的 SQL 可以不相同，所以可移植性比较差。

-   学习和使用门槛：MyBatis入门比较简单，使用门槛也更低。

-   二级缓存：hibernate 拥有更好的二级缓存，可以自行更换为第三方的二级缓存。

274. MyBatis 中 \#{}和 \${}的区别是什么？ （考）

-   \#将传入的数据都当成一个字符串，会对自动传入的数据加一个双引号。

-   如：where username=\#{username}，如果传入的值是111,那么解析成sql时的值为where username=\"111\", 如果传入的值是id，则解析成的sql为where username=\"id\".　

-   \$将传入的数据直接显示生成在sql中。

-   如：where username=\${username}，如果传入的值是111,那么解析成sql时的值为where username=111；

-   针对上面的sql，如果传入的值是;drop table user;，

-   那么第一条用\#{}的sql解析为：select id, username, password, role from user where username=\";drop table user;\"

-   那么第二条用\${}的sql解析为：select id, username, password, role from user where username=;drop table user;

这时候已经sql注入了。

-   \#方式能够很大程度防止sql注入，\$方式无法防止Sql注入。

-   \$方式一般用于传入数据库对象，例如传入表名和列名，还有排序时使用order by动态参数时需要使用\$ ，ORDER BY \${columnName}

-   一般能用\#的就别用\$，若不得不使用"\${xxx}"这样的参数，要手工地做好过滤工作，来防止sql注入攻击。

-   在MyBatis中，"\${xxx}"这样格式的参数会直接参与SQL编译，从而不能避免注入攻击。但涉及到动态表名和列名时，只能使用"\${xxx}"这样的参数格式。所以，这样的参数需要我们在代码中手工进行处理来防止注入。

-   【结论】在编写MyBatis的映射语句时，尽量采用"\#{xxx}"这样的格式。若不得不使用"\${xxx}"这样的参数，要手工地做好过滤工作，来防止SQL注入攻击。

-   \${}是 Properties 文件中的变量占位符，它可以用于标签属性值和 sql 内部，属于静态文本替换，比如\${driver}会被静态替换为com.mysql.jdbc.Driver。

-   \#{}是 sql 的参数占位符，Mybatis 会将 sql 中的\#{}替换为?号，在 sql 执行前会使用 PreparedStatement 的参数设置方法，按序给 sql 的?号占位符设置参数值，比如 ps.setInt(0, parameterValue)，\#{item.name} 的取值方式为使用反射从参数对象中获取 item 对象的 name 属性值，相当于 param.getItem().getName()。

### 延迟加载、性能优化

40\. MyBatis 是否支持延迟加载？延迟加载的原理是什么？ （考）

> MyBatis 支持延迟加载，设置 lazyLoadingEnabled=true 即可。
>
> 延迟加载的原理的是调用的时候触发加载，而不是在初始化的时候就加载信息。比如调用 a. getB(). getName()，这个时候发现 a. getB() 的值为 null，此时会单独触发事先保存好的关联 B 对象的 SQL，先查询出来 B，然后再调用 a. setB(b)，而这时候再调用 a. getB(). getName() 就有值了，这就是延迟加载的基本原理。
>
> Mybatis 仅支持 association 关联对象和 collection 关联集合对象的延迟加载，association 指的就是一对一，collection 指的就是一对多查询。在 Mybatis 配置文件中，可以配置是否启用延迟加载 lazyLoadingEnabled=true\|false。
>
> 它的原理是，使用 CGLIB 创建目标对象的代理对象，当调用目标方法时，进入拦截器方法，比如调用 a.getB().getName()，拦截器 invoke()方法发现 a.getB()是 null 值，那么就会单独发送事先保存好的查询关联 B 对象的 sql，把 B 查询上来，然后调用 a.setB(b)，于是 a 的对象 b 属性就有值了，接着完成 a.getB().getName()方法的调用。这就是延迟加载的基本原理。
>
> 当然了，不光是 Mybatis，几乎所有的包括 Hibernate，支持延迟加载的原理都是一样的。

275. Mybatis 的 Xml 映射文件中，不同的 Xml 映射文件，id 是否可以重复？

注：我出的。

答：不同的 Xml 映射文件，如果配置了 namespace，那么 id 可以重复；如果没有配置 namespace，那么 id 不能重复；毕竟 namespace 不是必须的，只是最佳实践而已。

原因就是 namespace+id 是作为 Map\<String, MappedStatement\>的 key 使用的，如果没有 namespace，就剩下 id，那么，id 重复会导致数据互相覆盖。有了 namespace，自然 id 就可以重复，namespace 不同，namespace+id 自然也就不同。

Mybatis 中如何执行批处理？

注：我出的。

答：使用 BatchExecutor 完成批处理。

43\. MyBatis 有哪些执行器（Executor）？ （考）

MyBatis 有三种基本的Executor执行器：

1)  SimpleExecutor：每执行一次 update 或 select 就开启一个 Statement 对象，用完立刻关闭 Statement 对象；

2)  ReuseExecutor：执行 update 或 select，以 SQL 作为 key 查找 Statement 对象，存在就使用，不存在就创建，用完后不关闭 Statement 对象，而是放置于 Map 内供下一次使用。简言之，就是重复使用 Statement 对象；

3)  BatchExecutor：执行 update（没有 select，jdbc 批处理不支持 select），将所有 SQL 都添加到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个 Statement 对象，每个 Statement 对象都是 addBatch()完毕后，等待逐一执行 executeBatch()批处理，与 jdbc 批处理相同。

Mybatis 都有哪些 Executor 执行器？它们之间的区别是什么？

注：我出的

答：Mybatis 有三种基本的 Executor 执行器，SimpleExecutor、ReuseExecutor、BatchExecutor。

\*\*SimpleExecutor：\*\*每执行一次 update 或 select，就开启一个 Statement 对象，用完立刻关闭 Statement 对象。

\*\*\`\`ReuseExecutor\`：\*\*执行 update 或 select，以 sql 作为 key 查找 Statement 对象，存在就使用，不存在就创建，用完后，不关闭 Statement 对象，而是放置于 Map\<String, Statement\>内，供下一次使用。简言之，就是重复使用 Statement 对象。

\*\*BatchExecutor：\*\*执行 update（没有 select，JDBC 批处理不支持 select），将所有 sql 都添加到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个 Statement 对象，每个 Statement 对象都是 addBatch()完毕后，等待逐一执行 executeBatch()批处理。与 JDBC 批处理相同。

作用范围：Executor 的这些特点，都严格限制在 SqlSession 生命周期范围内。

14、Mybatis 中如何指定使用哪一种 Executor 执行器？

注：我出的

答：在 Mybatis 配置文件中，可以指定默认的 ExecutorType 执行器类型，也可以手动给 DefaultSqlSessionFactory 的创建 SqlSession 的方法传递 ExecutorType 类型参数。

Mybatis 是否可以映射 Enum 枚举类？

注：我出的

答：Mybatis 可以映射枚举类，不单可以映射枚举类，Mybatis 可以映射任何对象到表的一列上。映射方式为自定义一个 TypeHandler，实现 TypeHandler 的 setParameter()和 getResult()接口方法。TypeHandler 有两个作用，一是完成从 javaType 至 jdbcType 的转换，二是完成 jdbcType 至 javaType 的转换，体现为 setParameter()和 getResult()两个方法，分别代表设置 sql 问号占位符参数和获取列查询结果。

16、Mybatis 映射文件中，如果 A 标签通过 include 引用了 B 标签的内容，请问，B 标签能否定义在 A 标签的后面，还是说必须定义在 A 标签的前面？

注：我出的

答：虽然 Mybatis 解析 Xml 映射文件是按照顺序解析的，但是，被引用的 B 标签依然可以定义在任何地方，Mybatis 都可以正确识别。

原理是，Mybatis 解析 A 标签，发现 A 标签引用了 B 标签，但是 B 标签尚未解析到，尚不存在，此时，Mybatis 会将 A 标签标记为未解析状态，然后继续解析余下的标签，包含 B 标签，待所有标签解析完毕，Mybatis 会重新解析那些被标记为未解析的标签，此时再解析 A 标签时，B 标签已经存在，A 标签也就可以正常解析完成了。

17、简述 Mybatis 的 Xml 映射文件和 Mybatis 内部数据结构之间的映射关系？

注：我出的

答：Mybatis 将所有 Xml 配置信息都封装到 All-In-One 重量级对象 Configuration 内部。在 Xml 映射文件中，\<parameterMap\>标签会被解析为 ParameterMap 对象，其每个子元素会被解析为 ParameterMapping 对象。\<resultMap\>标签会被解析为 ResultMap 对象，其每个子元素会被解析为 ResultMapping 对象。每一个\<select\>、\<insert\>、\<update\>、\<delete\>标签均会被解析为 MappedStatement 对象，标签内的 sql 会被解析为 BoundSql 对象。

18、为什么说 Mybatis 是半自动 ORM 映射工具？它与全自动的区别在哪里？

注：我出的

答：Hibernate 属于全自动 ORM 映射工具，使用 Hibernate 查询关联对象或者关联集合对象时，可以根据对象关系模型直接获取，所以它是全自动的。而 Mybatis 在查询关联对象或关联集合对象时，需要手动编写 sql 来完成，所以，称之为半自动 ORM 映射工具。

276. MyBatis 如何编写一个自定义插件？

> 自定义插件实现原理
>
> MyBatis 自定义插件针对 MyBatis 四大对象（Executor、StatementHandler、ParameterHandler、ResultSetHandler）进行拦截：

-   Executor：拦截内部执行器，它负责调用 StatementHandler 操作数据库，并把结果集通过 ResultSetHandler 进行自动映射，另外它还处理了二级缓存的操作；

-   StatementHandler：拦截 SQL 语法构建的处理，它是 MyBatis 直接和数据库执行 SQL 脚本的对象，另外它也实现了 MyBatis 的一级缓存；

-   ParameterHandler：拦截参数的处理；

-   ResultSetHandler：拦截结果集的处理。

> 自定义插件实现关键
>
> MyBatis 插件要实现 Interceptor 接口，接口包含的方法，如下：

-   setProperties 方法是在 MyBatis 进行配置插件的时候可以配置自定义相关属性，即：接口实现对象的参数配置；

-   plugin 方法是插件用于封装目标对象的，通过该方法我们可以返回目标对象本身，也可以返回一个它的代理，可以决定是否要进行拦截进而决定要返回一个什么样的目标对象，官方提供了示例：return Plugin. wrap(target, this)；

-   intercept 方法就是要进行拦截的时候要执行的方法。

自定义插件实现示例

官方插件实现：

### 查询、分页

#### 分页

277. MyBatis 有几种分页方式？ （考）

> 分页方式：逻辑分页和物理分页。

-   逻辑分页： 使用 MyBatis 自带的 RowBounds 进行分页，它是一次性查询很多数据，然后在数据中再进行检索。它是针对 ResultSet 结果集执行的内存分页。

-   物理分页： 自己手写 SQL 分页或使用分页插件 PageHelper，去数据库查询指定条数的分页数据的形式。

278. MyBatis 逻辑分页和物理分页的区别是什么？ （考）

-   逻辑分页是一次性查询很多数据，然后再在结果中检索分页的数据。这样做弊端是需要消耗大量的内存、有内存溢出的风险、对数据库压力较大。

-   物理分页是从数据库查询指定条数的数据，弥补了一次性全部查出的所有数据的种种缺点，比如需要大量的内存，对数据库查询压力较大等问题。

279. RowBounds 是一次性查询全部结果吗？为什么？ （考）

> RowBounds 表面是在"所有"数据中检索数据，其实并非是一次性查询出所有数据，因为 MyBatis 是对 jdbc 的封装，在 jdbc 驱动中有一个 Fetch Size 的配置，它规定了每次最多从数据库查询多少条数据，假如你要查询更多数据，它会在你执行 next()的时候，去查询更多的数据。就好比你去自动取款机取 10000 元，但取款机每次最多能取 2500 元，所以你要取 4 次才能把钱取完。只是对于 jdbc 来说，当你调用 next()的时候会自动帮你完成查询工作。这样做的好处可以有效的防止内存溢出。

Fetch Size 官方相关文档：http://t. cn/EfSE2g3

280. MyBatis 分页插件的实现原理是什么？ （考）

> 分页插件的基本原理是使用 MyBatis 提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的 SQL，然后重写 SQL，根据 dialect 方言，添加对应的物理分页语句和物理分页参数。
>
> 举例：select \_ from student，拦截 sql 后重写为：select t.\_ from （select \\\* from student）t limit 0，10

#### 模糊查询

281. 使用MyBatis做模糊查询的时候，在日志中看到执行了sql语句，但是查询不到结果。 （阿里参考面经）

> 面对这样的问题，如果可以看到后台的日志出现有相关的信息显示，那么就表示现在的整体环境搭建是没有任何问题的，但是为什么数据没有呢？
>
> 个人经验总结有如下几点：

a.  你的数据库里没有符合条件的数据，观察你的事务问题，更换一个新的客户端连接；

b.  你在使用模糊查询的时候，所传递的参数可能就有问题，这个时候最好的解决方案，就是观察数据层里面传入的内容是否正确；

c.  在使用模糊查询的时候千万要记住在关键字的左右增加一个"%"，如果没有加，那么就不叫模糊查询了；

d.  你现在所连接的数据库并不是你真正的数据库。

### 缓存

282. 说一下 MyBatis 的一级缓存和二级缓存？ （考）

-   一级缓存：基于 PerpetualCache 的 HashMap 本地缓存，它的声明周期是和 SQLSession 一致的，有多个 SQLSession 或者分布式的环境中数据库操作，可能会出现脏数据。当 Session flush 或 close 之后，该 Session 中的所有 Cache 就将清空，默认一级缓存是开启的。

-   二级缓存：也是基于 PerpetualCache 的 HashMap 本地缓存，不同在于其存储作用域为 Mapper 级别的，如果多个SQLSession之间需要共享缓存，则需要使用到二级缓存，并且二级缓存可自定义存储源，如 Ehcache。默认不打开二级缓存，要开启二级缓存，使用二级缓存属性类需要实现 Serializable 序列化接口(可用来保存对象的状态)。

> 开启二级缓存数据查询流程：二级缓存 -\> 一级缓存 -\> 数据库。
>
> 缓存更新机制：当某一个作用域(一级缓存 Session/二级缓存 Mapper)进行了C/U/D 操作后，默认该作用域下所有 select 中的缓存将被 clear。

## Hibernate

hibernate中如何在控制台查看打印的sql语句? （考）

为什么要使用Hibernate？ （考）

Hibernate有几种查询方式 （考）

Hibernate的实体类能被定义为final吗？ （考）

在Hibernate中使用integer和int做映射有什么区别？ （考）

Hibernate是如何工作的？ （考）

Get() 和 load的区别？（考）

283. 谈谈Hibernate的理解，一级和二级缓存的作用，在项目中Hibernate都是怎么使用缓存的？ （阿里官方面经）

> Hibernate是一个开发的对象关系映射框架（ORM）。它对JDBC进行了非常对象封装，Hibernate允许程序员采用面向对象的方式来操作关系数据库。

1)  优点：1、程序更加面向对象；2、提高了生产率；3、方便移植；4、无入侵性

2)  缺点：1、效率比JDBC略差；2、不适合批量操作；3、只能配置一种关联关系

3)  Hibernate有四种查询方式：

    -   get、load方法，根据ID号查询对象。
    
    -   Hibernate Query Language, HQL
    
    -   标准查询语言
    
    -   通过SQL查询

4)  Hibernate工作原理：

    -   配置Hibernate对象关系映射文件、启动服务器
    
    -   服务器通过实例化Configuration对象，读取hibernate.cfg.xml文件的配置内容，并根据相关的需求建好表以及表之间的映射关系。
    
    -   通过实例化的Configuration对象建立SessionFactory实例，通过SessionFactory实例创建Session对象。
    
    -   通过Session对象完成数据库的增删改查操作。

5)  Hibernate中的状态转移：

<!-- -->

a)  临时状态（Transient）

-   不处于Session缓存中

-   数据库中没有对象记录

> 补充说明-Java是如何进入临时状态的：1、通过new语句创建一个对象时。2、刚调用Session的delete()方法时，从Session缓存中删除一个对象时。

b)  持久化状态(Persisted)

    -   处于Session缓存中
    
    -   持久化对象数据库中没有对象记录
    
    -   Session在特定的时刻会保存两者同步

> 补充说明-Java如何进入持久化状态：1、Session的save()方法。2、Session的load().get()方法返回的对象。3、Session的find()方法返回的list集合中存放的对象。4、Session的update().save()方法。

c)  流离状态（Detached）

    -   不再位于Session缓存中
    
    -   游离对象由持久化状态转变而来，数据库中还没有相应记录。

> 补充说明-Java如何进入流离状态：1、Session的close()。2、 Session的evict()方法，从缓存中删除一个对象。
>
> 具体如下图所示：

![](media/image192.png){width="5.333333333333333in" height="3.3183278652668418in"}

6)  Hibernate中的缓存主要有Session缓存（一级缓存）和SessionFactory缓存（二级缓存，一般由第三方提供）。

<!-- -->

284. Hibernate控制反转 （阿里官方面经）

> 现在所说的是Hibernate中针对关系的配置处理，控制反转就是把控制权交给了对方，这种情况一般出现在数据的级联关系配置上：一对多、多对多。
>
> 以一个程序的分析为例：一个人有多本书，在Hibernate的世界里充满了神奇，它可以自动将没有的数据进行增加处理。正常的流程，首先要有一个人，这个人会有一个编号，在进行书的信息添加的时候就需要把这个人的编号一起保存进去。
>
> 如果不配置控制反转，它的处理：

-   ------增加人的信息；

-   ------增加所有书的信息，但此时人的保存的关联字段内容是null；

-   ------再更新所有书的信息，将人的关系的内容保存进来。

> 正常的流程（控制反转，将子表与父表关联字段的使用控制权交给子表自己控制）是：

-   ------保存人的信息，同时取得人的编号，将这些编号设置到书的内容里面；

-   ------保存书的信息

说一下Hibernate的缓存机制？ （考）

Hibernate对象有哪些状态？ （考）

在Hibernate中getCurrentSession和openSession的区别是什么？ （考）

Hibernate实体类必须要有无参构造函数吗？为什么？ （考）

### ORM与持久化映射

### 延迟加载、性能优化

### HQL查询、条件查询、SQL查询

### 二级缓存与查询缓存

285. Hibernate是不是只能与Struts2组合才好？我怎么没看到SpringMVC+Hibernate的组合？

> Hibernate实现的是一个数据层的开发框架，数据层是不会与MVC层产生任何直接联系，必须通过控制层与业务层来进行操作的处理后才可以使用。
>
> 最初的时候（2005）开始流行这个框架开发，使用最多的就是Struts1.X、Hibernate、Spring，而后就形成SSH的开发框架。现在的环境出现了改变，因为MyBatis出现之后会有人觉得Hibernate操作过于频繁，而MyBatis的开发更加简单。正因为如此，对于整体新项目设计而言就不会再过多的去考虑Hibernate了，基本上都是使用MyBatis开发框架。同时，在这个时期之后SpringMVC开始流行了，因为Struts毕竟需要与Spring整合，有人认为麻烦，现在对于开发就可能有如下几种结构：
>
> Struts 2.X+Hibernate+Spring；
>
> Struts 2.X+MyBatis+Spring；
>
> SpringMVC+Hibernate；
>
> SpringMVC+MyBatis。

286. SSH整合 （阿里官方面经）

> SSH整合实际上需要考虑到一个核心的问题：Struts之所以要整合到Spring之中主要是希望可以利用里面的IOC&DI机制实现业务层接口对象的注入处理，如果不使用Spring去管理Struts，那么无法直接利用容器注入的模式来实现业务层接口对象的配置，这样整个的整合效果就会出现严重的问题。
>
> 从另外一个角度来讲，虽然Struts支持Spring管理，但毕竟Spring属于两个开发框架，所以从2016年开始许多互联网公司的开发都不再选择使用Struts 2.x，但这并不表示Struts 2.x没有人使用，许多传统公司还在使用着。

## Struts

287. 描述Struts的工作流程 （阿里官方面经）

<!-- -->

1)  在web应用启动时，加载并初始化ActionServlet，ActionServlet从struts-config.xml文件中读取配置信息，将它们存放到各个配置对象中。

2)  当ActionServlet接收到一个客户请求时，首先检索和用户请求相匹配的ActionMapping实例，如果不存在，就返回用户请求路径无效信息。

3)  如果ActionForm实例不存在，就创建一个ActionForm对象，把客户提交的表单数据保存到ActionForm对象中。

4)  根据配置信息决定是否需要验证表单，如果需要，就调用ActionForm的validate()方法，如果ActionForm的validate()方法返回null或返回一个不包含ActionMessage的ActionErrors对象，就表示表单验证成功。

5)  ActionServlet根据ActionMapping实例包含的映射信息决定请求转发给哪个Action，如果相应的Action实例不存在，就先创建一个实例，然后调用Action的execute()方法。

> 面小易说：以上部分的相关问题考查面试者在实际软件开发中使用的Java语言相关框架以及对于框架原理的了解程度，这一部分我们需要注意一些常见的框架，不仅需要知道它们是干什么的，还需要知道它们背后的原理，常会问到的框架有Spring Boot/Spring Cloud全家桶、Hibernate、MyBaits、Netty、Kafka等，最重要的还有alibaba开源的Apache Dubbo框架。

288. action是单实例还是多实例? （阿里官方面经）

    -   Struts 2.x和Spring MVC中的Action都是多实例；
    
    -   Struts 1.x的Action是单实例；
    
    -   Struts 2.x和Spring MVC是否单实例可以控制，只要交由Spring管理的Action类，都可以通过"\@scope="prototype""来进行控制。

289. 修改单实例多实例 （阿里官方面经）

> "\@scope="prototype""来进行控制。

MVC模式与Struts体系

## 各框架对比与项目优化

290. Spring mvc 和 struts 的区别是什么？ （考）

-   拦截级别：struts2 是类级别的拦截；Spring mvc 是方法级别的拦截。

-   数据独立性：Spring mvc 的方法之间基本上独立的，独享 request 和 response 数据，请求数据通过参数获取，处理结果通过 ModelMap 交回给框架，方法之间不共享变量；而 struts2 虽然方法之间也是独立的，但其所有 action 变量是共享的，这不会影响程序运行，却给我们编码和读程序时带来了一定的麻烦。

-   拦截机制：struts2 有以自己的 interceptor 机制，Spring mvc 用的是独立的 aop 方式，这样导致struts2 的配置文件量比 Spring mvc 大。

-   对 ajax 的支持：Spring mvc 集成了ajax，所有 ajax 使用很方便，只需要一个注解 \@ResponseBody 就可以实现了；而 struts2 一般需要安装插件或者自己写代码才行。

291. sendRedirect, foward区别 （阿里官方面经）

<!-- -->

1)  foward是服务器端控制页面转向，在客户端的浏览器地址中不会显示转向后的地址；sendRedirect则是完全的跳转，浏览器中会显示跳转的地址并重新发送请求链接。原理：forward是服务器请求资源，服务器直接访问目标地址的URL，把那个URL的响应内容读取过来，然后再将这些内容返回给浏览器，浏览器根本不知道服务器发送的这些内容是从哪来的，所以地址栏还是原来的地址。

2)  redirect是服务器端根据逻辑，发送一个状态码，告诉浏览器重新去请求的那个地址，浏览器会用刚才的所有参数重新发送新的请求。

<!-- -->

292. ShiroRealm机制 （阿里官方面经）

Realm是几乎所有的认证授权框架都具备的一个概念，Realm本身有两层含义：

> （1）进行用户的认证处理：主要是进行用户名或密码的判断，同时还可以判断出该用户是否被锁定；
>
> （2）用户的授权处理：进行角色或权限认证，而且这里的认证所需要的就是根据用户名查询角色或权限标记。对于授权处理需要一些特殊处理方式：授权的操作在实际检测之中有两类：
>
> ------实时授权检测：修改了一个用户的角色或权限之后该配置立即生效，而且立即影响到已登陆的用户，这样的操作需要频繁进行数据库的查询处理，所以一般不建议使用；
>
> ------非实时授权检测：因为用户的角色和权限几乎很少会被改动，所以这样频繁的进行数据库的查询，性能会比较差。在实际开发之中，会考虑在用户第一次使用角色和权限的时候将数据信息查询出来。如果是单节点，会将授权信息保存在内存里（EhCache），如果是分布式集群，会将这些信息保存在Redis里面，总之就一个原则，不要在用户授权检测的时候重复查询数据库即可。
>
> 总结：ShiroRealm有一套自己的Session，在WEB中该Session会在HttpSession里面保存数据，但用户看不见这些。所有的授权处理一定要使用缓存，否则会影响程序性能。

293. Shiro中的Session与HttpSession的关系是什么？ （阿里官方面经）

> 如果说你现在使用的不是WEB程序，而是一个Java程序，那么Shiro中的认证与授权依然有效。可以得出一个结论：Shiro有一套自己维护的"Session"机制（不等同于HttpSession），如果要在WEB中应用，实际上就表示该Shiro Session要结合HttpSession一起使用，也就是说在Shiro Session中保存的内容在WEB容器里面实质上是保存在了HttpSession里面。
>
> 理解为：HttpSession中存在一个指定的Shiro属性，Shiro在设计的时候考虑到了用户的使用习惯，所以对于一些用户的身份信息，会将这些身份信息保存在Session里面，用户也可以直接利用Session属性取得相关的身份信息。

294. Shiro与Redis整合操作 （阿里官方面经）

前提是你的系统之中有多个WEB容器，并且使用了负载均衡，例如：Nginx。

![image.png](media/image193.png){width="4.614583333333333in" height="2.2083333333333335in"}

> 如果要想实现Session数据的共享，那么需要继承一个默认的企业SsessionDAO管理器：\
> ![image.png](media/image194.png){width="4.59375in" height="0.1875in"}\
> 里面就是针对Redis数据的CRUD操作。
>
> 如果要想实现缓存数据的共享（角色或者权限），那么就去继承一个默认的缓存管理器：
>
> ![image.png](media/image195.png){width="3.5729166666666665in" height="0.21875in"}\
> CacheManager、同时还需要去实现一个Cache的接口的子类才可以实现这样的共享操作。\
> 在整个流程之中你还需要考虑Tomcat的Session缓存。

![image.png](media/image196.png){width="4.833333333333333in" height="2.03125in"}

> 如果想要实现缓存：需要知道Nginx、Shiro的具体操作类的方法、Jedis工具类、Redis使用，这样才能去做集群的Session的缓存处理过程。

## JPA

295. jpa 和 hibernate 有什么区别？ （考）

> Hibernate是一个JPA实现，而Spring Data JPA是一个JPA数据访问抽象。Spring Data提供了GenericDao 自定义实现的解决方案 。它还可以通过方法名称约定代表您生成JPA查询。
>
> 使用Spring Data，您可以使用Hibernate，Eclipse Link或任何其他JPA提供程序。一个非常有趣的好处是您可以使用\@Transactional注释以声明方式控制事务边界。
>
> Spring Data JPA不是一个实现或JPA提供程序，它只是一个抽象，用于显着减少为各种持久性存储实现数据访问层所需的样板代码量。
>
> Hibernate提供了Java Persistence API的参考实现，使其成为具有松散耦合优势的ORM工具的绝佳选择。

请记住，Spring Data JPA始终需要JPA提供程序，如Hibernate或Eclipse Link。

### EJB

#### POJO

Entity：实体类。基本和数据表一一对应，一个实体一张表。

BO（business object）：把**业务逻辑**封装为一个对象，这个对象可以包括一个或多个其它的对象。通过调用Dao方法，结合Po或Vo进行业务操作。

VO（value Object）：值对象。通常用于业务层之间的数据传递，由new创建，由GC回收。

PO(persistant object)：持久层对象。

DTO(data transfer object)：数据传输对象。

Pojo(plian ordinary java object)：传统意义的java对象，最基本的Java Bean，只有属性加上属性的get和set方法。可以转化为PO、DTO、VO；比如POJO在传输过程中就是DTO。

Dao(data access object)

代表数据访问对象的意思，是sun的一个标准j2ee设计模式的接口之一，负责持久层的操作 。这个基本都了解，Dao和上面几个O区别最大，基本没有互相转化的可能性和必要，主要用来封装对数据的访问，注意，是对数据的访问，不是对数据库的访问。

所以实际项目中，一般都是这样应用的：

控制层(controller-action)，业务层/服务层( bo-manager-service)，实体层(po-entity)，dao(dao)，视图对象(Vo-)，视图层(view-jsp/html)

"分层领域模型规约：

DO（Data Object）：与数据库表结构一一对应，通过 DAO 层向上传输数据源对象。

DTO（Data Transfer Object）：数据传输对象， Service 或 Manager 向外传输的对象。

BO（Business Object） ：业务对象。由 Service 层输出的封装业务逻辑的对象。

AO（Application Object） ：应用对象。在 Web 层与 Service 层之间抽象的复用对象模型，极为贴近展示层，复用度不高。

VO（View Object）：显示层对象，通常是 Web 向模板渲染引擎层传输的对象。

Query ：数据查询对象，各层接收上层的查询请求。注意超过 2 个参数的查询封装，禁止使用 Map类来传输。"

# 

# XML编程

## XML基础

## XML进阶

## Web Service

WSDL与SOAP协议

296. 有没有用过定时任务？ （阿里官方面经）

> Java本身提供有定时任务：Time Task、Timer；但是此类操作对于定时很难完成，它只能够做频率，但是这个频率不准，所以在定时开发之中会使用quartz组件，而且Spring里面也提供有自己的定时实现，这个实现的好处是可以在准确的时间上进行触发。

297. 在jQuery里面如何绑定一个事件？ （阿里官方面经）

> 答：on("click",function)

298. 在JQuery里面你使用的Ajax处理函数有哪些？ （阿里官方面经）

> 答：\$. post()、\$.get()、\$.ajax()、\$.jsonp()

299. 在Spring里面控制层的方法返回的是什么？ （阿里官方面经）

> String或ModelAndView

300. 你简单描述一下WebService是什么？ （阿里官方面经）

> Web服务调用，结合WSDL 与SOAP形成远程方法调用；现有两种：CXF、Jersey。

301. 你描述一下什么叫RPC？ （阿里官方面经）

> RPC是一个远程过程调用，实际上WebService就是RPC的一种实现机制，RPC属于最原始的概念。

302. YML格式 （阿里官方面经）

> yml格式是与properties对应的一种格式，基本上可以方便的描述资源的配置。如果现在使用properties，那么定义格式如下：
>
> ![image.png](media/image197.png){width="3.5416666666666665in" height="0.53125in"}
>
> 如果要采用yml配置如下：
>
> ![image.png](media/image198.png){width="2.9895833333333335in" height="1.0833333333333333in"}
>
> 没有必要去考虑具体的格式，转换也很容易，之前SpringBoot有说过。（大家可以点击下方"阿里云大学-面试技巧"去看看）

303. 理论上是抽象类的所有抽象方法必须被覆写，但是为什么HttpServlet的子类中覆写或者不覆写都不会报错？ （阿里官方面经）

> *它们的关系：*
>
> （1） 爷爷类（抽象类）：GenericServlet；
>
> （2） 老子类（抽象类）：HttpServlet；
>
> （3） 类（普通类）：自定义的Servlet
>
> 关键的问题在于HttpServlet抽象类中的所有方法并不完全都是抽象方法，对于抽象类的子类需要覆写的只是抽象方法，而对于非抽象方法是不需要强制覆写的。

304. 在后端向jsp页面传递参数的时候可以使用对象传递，之后用EL表达式，也可以用JSON数据传递，在选择的时候优先选择哪一种好？ （阿里官方面经）

> 如果想玩高档界面，整个页面不直接生成，那么使用JQuery加载最好。
>
> EL工作在服务器端，而JSON操作工作在客户端处理（服务器生成），这两点完全没有可比性。
>
> 当使用JSP处理的时候，必须明确所有的代码是由容器负责生成，生成的是HTML代码，这些代码依靠一些对象生成，生成完成之后才会把生成的代码发送给客户端，客户端要进行整体的解析处理。而JSON只是一个传输的格式，它要求在整个的处理里面需要通过前台的JS来进行数据的控制。
