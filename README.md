# translate
translate spring framework reference
Spring Framework Reference Documentation
Based on 4.2.1.RELEASE
#目录
* [概述](#概述)
	* [概览](#1-spring入门)
	* [简介](#2-spring简介)
		* [依赖注入和控制反转](#21-依赖注入和控制反转)
		* [模块](#22-spring的模块)
			* [核心容器](#221-core-container)
			* [AOP和检测](#222-aop和检测)
			* [消息](#223-消息)
			* [数据访问/集成](#224-数据访问集成)
			* [网络](#225-web)
			* [测试](#226-测试)
		* [应用场景]()
			* [依赖管理和命名规约]()
				* [Spring依赖和被依赖]()
				* [Maven依赖管理]()
				* [MavenBOM依赖]()
				* [Gradle依赖管理]()I
				* [Ivy依赖管理]()
				* [Zip文件]()
			* [日志]()
				* [没有使用CommonsLogging]()
				* [使用了SLF4J]()
				* [使用了Log4J]()

# 概述
Spring 框架是个轻量级解决方案，在构建一站式企业级应用程序上有很大的潜能。Spring是模块化的，允许你仅使用需要的不分，而不需要引入其余部分。你可以使用IoC容器，和其他Web框架一起使用，而且你可以仅仅使用Hibernate集成代码或者JDBC的抽象层。Spring框架支持声明式事物管理，通过RMI或者Web Service远程访问，以及各种持久化数据的方法。Spring提供了一个功能齐全的Web框架，允许你显示的整合AOP到你的软件中。

Spring 被设计成非侵入式的，也就是说你的业务逻辑代码通常是不会对Spring框架本身产生依赖的。在你的整合层面（比如数据访问层），一些依赖于数据访问技术和Spring的类库是会存在的。但是，也很容易将这些依赖从你剩余的代码中分离出来。
本文档是Spring框架的参考指南功能。如果你有任何请求,评论,或对这个文档的问题,请将它们贴在用户邮件列表。框架的问题，可以在StackOverflow提问(https://spring.io/questions)。

## 1. Spring入门
指南文档提供了Spring框架详细的信息 。提供了所有特征的详细文档，而且还包含一些底层概念的背景（比如依赖注入）。

如果你仅仅是开始使用Spring框架，你可以通过Spring 创建一个基于 application 的 Spring Boot。Spring Boot 提供了一个基于 application 的快捷的（并且配置好的）Spring。它是基于Spring框架，支持覆盖配置，能够让你尽可能的快速启动和运行。

你还可以使用 start.spring.io 自动创建一个基础项目或者依照“Getting Started”的指南，比如 Getting Started 创建一个 RESTful Web Service。这些指南大部分都是基于Spring Boot，除了非常容易理解和吸收外，重点聚焦于任务。它们还涵盖了一些其他Spring项目，当你考虑解决一个特定问题的时候。

## 2. Spring简介
Spring 框架是一个Java平台，它提供了对用Java语言开发应用程序的一种广泛的基础支持。Spring本身来控制这个基础，那么你就可以集中精力于应用程序的开发了。Spring允许你从“普通Java对象（POJO）”来构建应用程序，并且将非侵入地企业级服务应用于POJO中。这种能力不仅适用于JavaSE编程模型，也适用于全部或部分的JavaEE。

作为应用程序的开发人员，下面就是可以使用Spring平台所含优点的例子：
* 编写Java方法来执行数据库事务而不需要处理相关的事务API。
* 编写本地的Java方法来访问远程程序而不需要处理远程访问API。
* 编写本地的Java方法来执行管理操作而不需要处理JMX的API。
* 编写本地的Java方法来处理消息操作而不需要处理JMS的API。

### 2.1 依赖注入和控制反转
Java 应用程序--一个宽松的术语，囊括了从被限制的 application 到n层服务器端的企业级应用程序的全部–典型的应用是，包含了组成独特应用程序的合作对象。那么在应用程序中的这些对象就会有相互依赖关系。

尽管Java平台提供了丰富的应用程序开发功能，但是它也缺乏组织基本模块到整体的方式，而是把这个任务留给了系统架构师和开发人员去解决。也就是说，你可以设计如工厂，抽象工厂，构建者，装饰者和服务定位器等设计模式来组合各个类，以及构成该应用程序的对象的实例。然而，这些模式都是最简单的：最佳的做法是给定一个名称，并且描述这个模式做了些什么，在哪里可以应用它，它所强调的问题是什么等等。模式可以使得你必须自己实现的最佳实践形式化。

Spring框架的控制反转（Inversion of Control，IoC）组件提供了组合不同的组件到完整可用的应用程序的形式化方法。Spring框架编写了形式化的设计模式作为顶级对象，你可以用来整合到你自己的应用程序中。很多组织和研究机构使用Spring的这个方式来设计健壮的，可维护的应用程序。

	背景
	
	“问题是，[它们]反向控制哪一方面？”，2004年，Martin Fowler在他个人站点提出了这个关于控制反转（IoC）的问题。
	Fowler建议重命名这个原则，使得它更好地自我解释，同时提出了依赖注入。要深入了解IoC和DI，可以参考Fowler的文章，
	地址是：http://martinfowler.com/articles/injection.html

### 2.2 Spring的模块

**图 2.1 Spring-Overview**

![Spring-Overview](../master/Spring/images/spring-overview.png)


以下章节列出了可用模块的功能，以及他们的模块的名称和封装的主题。模块的名称可以和依赖工具中的Artifact ID关联。
#### 2.2.1 Core Container
核心容器由 spring-core、spring-beans、spring-context、spring-context-support 和 spring-expression（SpringEL）模块组成。

spring-core 和 spring-beans 是框架的基础，包含IoC和依赖注入。BeanFactory 是工厂模式经典的实现。它去掉了编程实现单例的需要，并允许你解除配置信息，以及实际程序逻辑的特定依赖之间的耦合。

Context模块建立在 Core 和 Beans模块的坚固基础之上。它可以让你用框架风格来访问数据，就像JNDI注入一样。Context模块继承了Beans模块的特增，并且增加了国际化的支持（使用，例如，资源束）、事件传播、资源加载和显示创建context，例如Servlet容器。Context模块同样也支持Java EE的特征，比如EJB，JMX和基本的远程调用。ApplicationContext 接口是Context模块的重点。spring-context-support 集成第三方通用函数库，为了Spring应用上下文的缓存（Ehcache、Guava、JCache）、邮件（JavaMail）、调度（CommonJ，Quartz）和模板引擎（FreeMarker, JasperReports, Velocity）提供了支持。

spring-expression模块提供了强大的表达式语言在运行时查询和操作对象图。这是JSP 2.1规范中的统一表达式语言（Unified EL）的一个扩展。该表达式语言支持设置和获取属性值，属性定义，方法调用，访问数组，集合以及索引的上下文。支持逻辑和数字运算，命名变量。还支持从Spring的IoC容器中以名称来获取对象。它也支持list的投影和选择操作，还有普通的list聚集。

#### 2.2.2 AOP和检测
Spring的AOP（8.1节）模块提供了AOP联盟-允许的的面向切面的编程实现，允许你定义如方法-拦截器和横切点来整洁地解耦应该被分离的功能实现代码。使用源代码级的元数据功能，也可以混合行为信息到代码中，这个方式和.NET的属性很相似。
分离的Aspects模块提供对AspectJ的整合。

spring-instrument 模块提供了类检测的支持和某些应用服务器类加载的实现。spring-instrument-tomcat 模块包含了Tomcat的检测代理。

#### 2.2.3 消息
Spring4 包含了 spring-messaging 模块。改模块包含了Spring集成项目，比如Message，MessageChannel、MessageHandle和其他以消息为基础提供服务的应用的关键的抽象类。改模块同样包含一组从消息映射到方法的注解，就想SpringMVC中基于编程模型的注解。

#### 2.2.4 数据访问/集成
数据访问/集成层包含JDBC、ORM、OXM、JMS和事物模块。

spring-jdbc 提供了JDBC抽象层，它移除了冗长的JDBC编码，但解析了数据库 提供商定义的特定错误代码。

spring-tx 模块支持对实现特定接口的类和所有POJO（普通Java对象）的编程式和声明式的事务管理。

spring-orm 模块提供了对流行的对象-实体映射API的整合层，包含JPA，JDO，Hibernate和iBatis。使用spring-orm 模块你就可以使用全部的O/R-映射框架并联合其它Spring提供的特性，比如之前所提到的简单声明式的事务管理特性。

spring-oxm 模块提供了支持JAXB，Castor，XMLBeans，JiBX，以及Xstream对对象/XML映射实现的抽象层。

spring-jms 模块（JMS）模块包含生成和处理消息的特性。Spring 4.1 以后，它还提供了和 spring-messages 模块的整合。

#### 2.2.5 Web
Web层由spring-web、spring-webmvc、spring-websocket、和spring-webmvc-portlet组成。

spring-web 模块提供了面向web整合的基本特征，比如文件上传功能、使用Servlet监控初始化IoC容器以及面向web的上下文。该模块还包含了Http客户端和对于Spring远程访问中web相关的支持。

spring-webmvc 模块（也被称为Web-Servlet模块）有 Spring MVC 和 REST Web Service组成。Spring MVC框架提供了一个在领域模型代码和Web表单之间的整洁分离，并且整合了其它所有Spring框架的特性。

spring-webmvc-portlet 模块（也被称为 Web-Portlet模块）提供用于portlet环境和Web-Servlet模块功能镜像的MVC实现。

#### 2.2.6 测试
spring-test 模块通过JUnit和TestNG提供了Spring的组件的单元测试和集成测试。它提供了Spring 的ApplicationContexts 的一致加载并缓存这些上下文内容。它也提供mock对象，你可以用来单独的测试代码。

### 2.3 应用场景
前面描述的模块使得Spring可以在很多方案中作为业务逻辑实现的选择，从资源受限的设备上运行的嵌入式应用到以Spring事物管理为基础，通过Web框架整合的功能完善的企业级应用。

**图2.2 典型的功能完善的企业级应用**

![](../master/Spring/images/overview-full.png)


Spring的声明式事务管理特性使得Web应用程序可以全部事务化，就好像使用了EJB容器管理的事务。全部的自定义的业务逻辑可以通过简单的POJO类实现，并通过Spring的IoC容器进行管理。其它的服务包含对发送邮件的支持，验证对Web层独立，这可以让你选择在哪里执行验证规则。Spring的ORM支持对JPA，Hibernate,JDO和iBatis进行了整合；比如，当使用Hibernate时，你可以继续使用已有的映射文件和标准的Hibernate的SessionFactory配置。表单控制器通过业务模型无缝地整合了Web层，去除了对ActionForm的需求以及Http参数转换为业务模型属性值的类。

**图2.3 使用了第三方web框架的Spring中间层**

![](../master/Spring/images/overview-thirdparty-web.png)


有些情况下，不允许你完全切换到不同的框架中。Spring框架并不是一个非此即彼的解决方案，他并不强迫你全都都使用他。通过Struts, Tapestry, JSF 或者其他UI 框架构建的前端同样可以集成以Spring为基础的中间层，可以使用Spring事物管理的功能。你只需要通过ApplicationContext连接你的业务逻辑以及使用WebApplicationContext整合你的web层。

**图2.4 远程使用场景**

![](../master/Spring/images/overview-remoting.png)


当你想通过web服务访问已经存在的代码，你可以使用Spring的Hessian-, Burlap-, Rmi- 或 JaxRpcProxyFactory 类。启用远程访问现有的应用程序并不难。

**图2.5 EJBs 包装现有的POJO**

![](../master/Spring/images/overview-ejb.png)

Spring 框架也提供了EJB的使用通道和EJB的抽象层，这就可以重用已有的POJO，可以扩展、包装它们到无状态会话bean，不安全的Web应用程序可能也需要声明式安全。

#### 2.3.1 依赖管理和命名规约
依赖管理和依赖注入是不同的事情。要在应用程序中添加Spring的优雅特性（比如依赖注入），你需要放置所需的类库（jar文件），并且添加到运行时环境的类路径中，通常在编译时也是需要这些类库文件的。这些依赖不是注入的虚拟组件，而是文件系统（通常来说是这样）上的物理资源。依赖管理的过程包括定位资源，存储它们，并将它们添加到类路径中。依赖可以是直接的（比如应用程序在运行时需要Spring），或者是间接的（比如应用程序需要的commons-dbcp组件还依赖于commons-pool组件）。间接的依赖也被认为是“过度的”，而且那些依赖本身就难以识别和管理。

如果你决定使用Spring，那么你需要获得Spring的jar包，其中要包括你所需要使用的Spring的模块。为了使用的便捷，Spring被打包成各个模块的集合，尽可能地分离其中的相互依赖，那么如果你不想编写Web应用程序，就不需要添加spring-web模块的jar包。要参考Spring模块的库，本指南使用了一个可以速记的命名规约，spring-*或者spring-*.jar，这里的“*”代表了各模块的短名称（比如，spring-core，spring-webmvc，spring-jms等）。实际上jar文件命名或许就是这种形式的（参考下面的示例），但也有可能不是这种情况，通常它的文件名中还包含一个版本号（比如，spring-core-4.2.1.RELEASE.jar）。

每个稳定版本的组件都会被发布到下面的地方：
Maven的中央库，也是Maven默认检索的资源库，它并不会检索特殊的配置来使用。很多Spring所依赖的常用类库也可以从Maven的中央库中获得，同时Spring社区的绝大多数用户都使用Maven作为依赖管理工具，这对于他们来说是很方便的。这里的jar包的命名规则是spring-*-<version>.jar格式的，并且Maven里的groupId是org.springframework。

专门为Spring托管的Maven公共仓库。除了最终的GA版本，还托管了开发中的SNAPSHOT版本和MILESTONE版本。文件命名和Maven仓库命名一样，所以这个获取开发版本非常有用的地方。这个仓库同样包含了zip文件，非常容易下载。

那么，首先你要决定的事情是如何管理这些依赖：我们一般建议使用一个自动化的系统，比如Maven、Gradle 或者 Ivy，当然你也可以自己手动下载所有jar。

一下列表中是你可以找到的Spring的组件，模块的详细描述参加 第2.2章 “模块”。

表2.1 Spring Framework Artifacts（略）

##### Spring的依赖与被依赖

尽管Spring提供对整合的支持，以及对大量企业级应用及其外部工具的支持，那么它也有心保持它的强制依赖在一个绝对小的数目上：你不需要为了简单的使用去定位并下载（甚至是自动地）大量的jar来使用Spring。对于基本的依赖注入那只需要一个必须的外部依赖，就是日志（可以参考下面关于日志的深入介绍）。

下面，我们来概述一下配置一个基于Spring的应用程序所需的基本配置，首先使用Maven，然后是Gradle和Ivy。在所有的示例中，如果有哪一点不清楚，可以参考你所使用的依赖管理系统的相关文档，或者参考一些示例代码 – Spring本身在构建时使用了Gradle 来管理依赖，我们大多数的示例也使用Gradle 或者Maven。

##### Maven依赖管理
如果你正使用Maven来进行依赖管理，那么你就不需要明确地提供日志依赖。比如，要为应用程序配置创建应用上下文并使用依赖注入特性，那么，你的Maven依赖配置文件可以是这样的：
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.2.1.RELEASE</version>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```
就是这么简单。要注意的是，如果你在编译代码时不需要使用Spring的API，那么scope元素可以声明为runtime，这就可以用于典型的依赖注入用例。

在上面的示例中，我们使用了Maven中央仓库。使用Spring Maven仓库，那就需要在Maven的配置文件中明确地指定资源库的位置。对于完整发布版，配置如下：
```xml
 <repositories>
     <repository>
         <id>io.spring.repo.maven.release</id>
         <url>http://repo.spring.io/release/</url>
         <snapshots><enabled>false</enabled></snapshots>
     </repository>
 </repositories>
```
里程碑版本：
```xml
<repositories>
    <repository>
        <id>io.spring.repo.maven.milestone</id>
        <url>http://repo.spring.io/milestone/</url>
        <snapshots><enabled>false</enabled></snapshots>
    </repository>
</repositories>
```
开发快照版本：
```xml
<repositories>                                                                            w
    <repository>
        <id>io.spring.repo.maven.snapshot</id>
        <url>http://repo.spring.io/snapshot/</url>
        <snapshots><enabled>true</enabled></snapshots>
    </repository>
</repositories>
```

##### Maven的BOM依赖

当你使用Maven的时候有可能把Spring不同版本的jar包混合在一起。比如，你找到一个第三方的类库，或者另一个Spring的项目，依赖一个旧的稳定版本。如果你忘记了排除这个依赖，可能会产生让你意向不到的问题。
为了解决这些问题，Maven支持BOM依赖的概念。你可以在你的dependencyManagement节点中引入spring-framework-bom 以确保依赖的组件（直接或者间接的）都是同一个版本。
```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-framework-bom</artifactId>
            <version>4.2.1.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```
使用BOM的另一好处是你在依赖Spring组件的时候，不再需要再指定<version>的属性。
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
    </dependency>
<dependencies>
```
##### Gradle 依赖管理
使用 Gradle 通过Spring中央仓库构建项目，包含appropriate URL 在repositories 节点：
```gradle
repositories {
    mavenCentral()
    // and optionally...
    maven { url "http://repo.spring.io/release" }
}
```
你可以修改repositories 的URL 从 /release 到 /milestone 到 /snapshot 作为恰当的地址，一旦配置好仓库，你就可以通过 Gradle 声明依赖：
```gradle
dependencies {
    compile("org.springframework:spring-context:4.2.1.RELEASE")
    testCompile("org.springframework:spring-test:4.2.1.RELEASE")
}
```
##### Ivy依赖管理
如果你使用Ivy来管理依赖，那么有一些简单的命名规约和配置选项。
要配置Ivy定位到SpringSource EBR中，需要添加如下的解析器元素到你的配置文件 ivysettings.xml中：
```xml
<resolvers>
    <ibiblio name="io.spring.repo.maven.release"
            m2compatible="true"
            root="http://repo.spring.io/release/"/>
</resolvers>
```
你可以修改 root URL 从 /release 到 /milestone 到 /snapshot 作为恰当的地址。
一点你配置好，就可以通过Ivy来添加依赖了，例如（在ivy.xml中）：
```xml
<dependency org="org.springframework"
    name="spring-core" rev="4.2.1.RELEASE" conf="compile->runtime"/>
```

##### Zip文件

尽管推荐使用支持依赖管理的构建系统的获取Spring框架,仍然可以下载zip文件。

zip文件发布在Spring中央仓库（为了方便,你不需要使用Maven或任何其他构建系统就能下载它们）。

通过web浏览器打开  http://repo.spring.io/release/org/springframework/spring ，选择你想要的版本的文件夹。zip文件以 -dist.zip为结尾。比如spring-framework-{spring-version}-RELEASE-dist.zip。zip文件同样有里程碑版本和开发快照版本。

#### 2.3.2 日志

对于Spring来说，日志是一个非常重要的依赖，因为a)这是唯一强制的外部依赖，b) 开发人员都会想看到他们所使用的工具的一些输出内容，而且c)Spring整合了多种实用工具，它们都会选择一种日志依赖包。应用程序开发人员的目标之一就是在核心位置对整个应用程序有一个统一的日志配置，包括对所有的外部组件。因为日志框架有多种选择，那么这就可能有些难以确定了。

Spring中强制的日志依赖包是Jakarta的Commons Logging API（JCL）。我们对Spring的编译是基于JCL的，而且我们使扩展了Spring Framework的类对JCL包的Log对象都是可见的。对于用户来说，所有Spring的版本都使用相同的日志包也是很重要的：因为保留了向后兼容的特性，那么迁移是很容易进行的，同理，扩展Spring的应用程序也是这样。我们这样做就是使得Spring中的模块明确地使用基于commons-logging（JCL的典型实现）的日志实现，在编译时也使得其它模块都基于这个日志包。如果你正在使用Maven的话，同时想知道在哪儿获取到的commons-logging依赖，那就是从Spring中被称作是spring-core的核心模块中获取的。

关于commons-logging比较好的做法是你不需要做其它的步骤就可以使应用程序运行起来。它有一个运行时的查找算法，在我们都知道的类路径下寻找其它的日志框架，并且使用Spring认为是比较合适的（或者告诉Spring你需要使用的具体是哪一个）一个。如果没有找到可用的，那么你会得到一个来自JDK（java.util.logging或者简称为JUL）本身看起来还不错的日志依赖。那么，你会发现在很多时候，Spring应用程序运行中会有日志信息打印到控制台上，这点是很重要的。

##### 不使用Commons Logging

不幸的是，commons-logging的运行时查找算法对最终用户方便是有些问题的。如果我们可以让时光倒流并让Spring从现在开始作为一个新的项目进行，那么我们会使用不同的日志依赖。首选的日志依赖可能就是Java简单的日志门面（SLF4J），SLF4J也被Spring的开发人员在他们其它应用程序中的很多工具所使用。
这有两个非常典型的关闭 commons-logging 的方法：
1、从spring-core模块中排除依赖（因为它是唯一一个明确依赖于 commons-logging 的模块）。
2、用一个空的jar包替代 commons-logging （详细细节参见 SLF4J FAQ）。
不包含 commons-logging ，代码如下：
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.2.1.RELEASE</version>
        <exclusions>
            <exclusion>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>
```
目前这个应用程序可能就不能运行了，因为在类路径中已经没有了JCL API的实现了，所以要修复这个问题的话，就要提供另外一种日志的实现了。在下一节中，我们来说明如何提供一个其它的JCL的实现，这里，我们使用SLF4J作为示例。

##### 使用SLF4J

SLF4J是一个整洁的日志依赖，在运行时的效率也比commons-logging更高，因为 SLF4J使用了编译时构建，而不是运行时去查找其它整合的日志框架。这也就意味着你可以更明确地在运行时去做些什么，并且去声明或配置。SLF4J为很多通用的日志框架提供的绑定，所以通常你可以选择已有的一个，并去绑定配置或管理。

SLF4J为很多通用日志框架提供绑定，包括JCL，并且也可以反向进行：桥接其它的日志框架和SLF4J本身。所以如果要在Spring中使用SLF4J，那么就需要使用SLF4J-JCL桥来代替commons-logging依赖。只要配置好了，那么来自Spring的日志调用就会被翻译成调用SLF4J的API了，如果在应用程序中的其它类库使用了原有的API，那么会有一个单独的地方来进行配置和管理的日志。

一个常用的选择就是桥接Spring到SLF4J API，之后提供从SLF4J到Log4J的明确绑定。你需要提供4种依赖（并排除已经存在的commons-logging依赖）：桥接工具，SLF4J的API，绑定到Log4J的工具，还有Log4J本身的实现。那么在Maven的配置文件中，你就可以这样来做：
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.2.1.RELEASE</version>
        <exclusions>
            <exclusion>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>jcl-over-slf4j</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-log4j12</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.14</version>
    </dependency>
</dependencies>
```
这样，看起来好像很多依赖都需要日志了。情况确实是这样，但SLF4J是可选的，而且它的性能要比含有类加载器问题的commons-logging依赖好很多，尤其是如果你使用了一个严格限制的容器，比如OSGi平台。据称那也会有性能优势，因为绑定是编译时进行的，而不是在运行时。

另外，在SLF4J的用户中一个较为常见的选择是使用很少步骤，同时产生更少的依赖，那也就是直接绑定到Logback上。这会去掉很多额外的绑定步骤，因为Logback本身直接实现了SLF4J，这样的话，你就仅需要两个依赖的类库，而不用原先的是四个了（就是jcl-over-slf4j和logback）。如果你也确实那么来做了，你可能还需要从其它外部依赖（而不是Spring）中去掉slf4j-api的依赖，因为在类路径中只保留一个API的一个版本就行了。

##### 使用 Log4J

很多用户出于配置和管理的目的而使用Log4j作为日志框架。这样也同样很有效率并且易于创建，而且，Log4j也是我们事实上在构建和测试Spring时，和运行时环境中使用的日志框架。Spring本身也提供一些工具来配置和初始化Log4j，所以，在某些模块中它也提供了可选的在编译时对Log4j框架的依赖。

要让Log4j框架和默认的JCL依赖（commons-logging）同时起作用，你所要做的就是要将Log4j的类库放到类路径下，并且提供配置文件（在类路径的根路径下放置log4j.properties或log4j.xml为名的文件）。而对于使用Maven的用户来说，下面的代码可以是对依赖的声明：
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.2.1.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.14</version>
    </dependency>
</dependencies>
```
下面是log4j.properties打印到控制台的日志的配置示例：
```properties
log4j.rootCategory=INFO, stdout

log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %t %c{2}:%L - %m%n

log4j.category.org.springframework.beans.factory=DEBUG
```
运行时容器和本地的JCL

很多用户在容器中运行Spring的应用程序，而该容器本身也提供了JCL的实现。比如IBM 的 Webshphere应用服务器（WAS）就是这种类型的。这通常就会引起问题，而不幸的是没有什么解决的方法；很多情况下仅仅从应用程序中去掉commons-logging依赖是不够的。

我们要清楚地认识这一点：这个问题通常和JCL本身一同报告出来，或者是和commons-logging：而不是绑定commons-logging到另外的框架（这里，通常是Log4J）。这就可能会引发问题，因为commons-logging改变了它们在运行时环境里，在一些容器中查找老版本（1.0）的方式，而现在很多人使用的是新版本（1.1）。Spring不会使用任何不通用的JCL API部分，所以这里不会有问题，但是Spring本身或应用程序尝试去进行日志记录，你可以发现绑定到Log4J是不起作用的。

这种在WAS上的情况，最简单的做法就是颠倒类加载器的层次（IBM称之为“parent last”），那么就是使应用程序来控制，而不是容器来控制JCL的依赖。这种选择并不总是开放的，但是在公共领域中的替代方法也有其它的建议，根据确切的版本和容器的特性集，您所要求的效果可能会有不同。
