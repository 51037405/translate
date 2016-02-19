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
			* [依赖管理和命名规约](#231-依赖管理和命名规约)
				* [Spring依赖和被依赖](#spring的依赖与被依赖)
				* [Maven依赖管理](#maven依赖管理)
				* [MavenBOM依赖](#maven的bom依赖)
				* [Gradle依赖管理](gradle-依赖管理)I
				* [Ivy依赖管理](#ivy依赖管理)
				* [Zip文件](#zip文件)
			* [日志](#232-日志)
				* [没有使用CommonsLogging](#不使用commons-logging)
				* [使用了SLF4J](#使用slf4j)
				* [使用了Log4J](#使用-log4j)
* [Spring 4.x 的新特征](#spring-4x-的新特征)
    * [Spring Framework 4.0 的新特征和优化功能]()
        * [改进开始使用的体验](#31-提升了入门的体验)
        * [删除的包和方法](#32-删除废弃的包和方法)
        * [Java 8 (as well as 6 and 7)](#33-java8以及6和7)
        * [Java EE 6 and 7](#34-javaee6和7)
        * [Groovy Bean Definition DSL](#35-groovy-bean-definition-dsl)
        * [核心容器的改进](#36-核心容器的改进)
        * [Web 改进](#37-web改进)
        * [WebSocket, SockJS, and STOMP Messaging](#38-websocketsockjs和stomp消息)
        * [Testing Improvements](#39-测试改进)
    * [Spring Framework 4.1 的新特征和优化功能](#4-spring-41增强和新功能)
        * [JMS 改进](#41-jms改进)
        * [Caching 改进](#42-caching改进)
        * [Web 改进](#43-web改进)
        * [WebSocket Messaging 改进](#44-websocket-messaging-改进)
        * [Testing 改进](#45-testing-改进)
    * [Spring Framework 4.2 的新特征和优化功能](#5-spring-42增强和新功能)
        * [Core Container 改进](#51-核心容器的改进)
        * [Data Access 改进](#52-数据访问的提升)
        * [JMS 改进](#53-jms改进)
        * [Web 改进](#54-web-改进)
        * [WebSocket Messaging 改进](#55-websocket-messaging-改进)
        * [Testing 改进](#56-testing-改进)
* [核心技术](#核心技术)
    * [IoC容器](#6-IoC容器)
        * [Spring IoC容器和Beans入门](#61-Spring-IoC-容器和Beans入门)
    * [容器](#62-容器)
        * [配置元数据](#621-配置元数据)
        * [实例化容器](#622-实例化容器)
        * [使用容器](#623-使用容器)
    * [Bean](#63-bean)
        * [Bean的命名](#631-bean-的命名)
        * [实例化Bean](#632-实例化bean)
    * [依赖](#64-依赖)
        * [依赖注入](#641-依赖注入)
        * [依赖配置详解](#642-依赖配置详解)

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

> **背景**
	
>	“问题是，[它们]反向控制哪一方面？”，2004年，Martin Fowler在他个人站点提出了这个关于控制反转（IoC）的问题。	Fowler建议重命名这个原则，使得它更好地自我解释，同时提出了依赖注入。要深入了解IoC和DI，可以参考Fowler的文章，地址是：http://martinfowler.com/articles/injection.html

### 2.2 Spring的模块

**图 2.1 Spring-Overview**

![Spring-Overview](../master/Spring/images/spring-overview.png)


以下章节列出了可用模块的功能，以及他们的模块的名称和封装的主题。模块的名称可以和依赖工具中的Artifact ID关联。
#### 2.2.1 Core Container
核心容器由 `spring-core`、`spring-beans`、`spring-context`、`spring-context-support` 和 `spring-expression`(SpringEL)模块组成。

`spring-core` 和 `spring-beans` 是框架的基础，包含IoC和依赖注入。`BeanFactory` 是工厂模式经典的实现。它去掉了编程实现单例的需要，并允许你解除配置信息，以及实际程序逻辑的特定依赖之间的耦合。

Context(`spring-context`)模块建立在 Core 和 Beans模块的坚固基础之上。它可以让你用框架风格来访问数据，就像JNDI注入一样。Context模块继承了Beans模块的特增，并且增加了国际化的支持（使用，例如，资源束）、事件传播、资源加载和显示创建context，例如Servlet容器。Context模块同样也支持Java EE的特征，比如EJB，JMX和基本的远程调用。`ApplicationContext` 接口是Context模块的重点。`spring-context-support` 集成第三方通用函数库，为了Spring应用上下文的缓存（Ehcache、Guava、JCache）、邮件（JavaMail）、调度（CommonJ，Quartz）和模板引擎（FreeMarker, JasperReports, Velocity）提供了支持。

`spring-expression`模块提供了强大的表达式语言在运行时查询和操作对象图。这是JSP 2.1规范中的统一表达式语言（Unified EL）的一个扩展。该表达式语言支持设置和获取属性值，属性定义，方法调用，访问数组，集合以及索引的上下文。支持逻辑和数字运算，命名变量。还支持从Spring的IoC容器中以名称来获取对象。它也支持list的投影和选择操作，还有普通的list聚集。

#### 2.2.2 AOP和检测
`spring-aop`（8.1节）模块提供了AOP联盟-允许的的面向切面的编程实现，允许你定义如方法-拦截器和横切点来整洁地解耦应该被分离的功能实现代码。使用源代码级的元数据功能，也可以混合行为信息到代码中，这个方式和.NET的属性很相似。
分离的`spring-aspects`模块提供对AspectJ的整合。

`spring-instrument` 模块提供了类检测的支持和某些应用服务器类加载的实现。`spring-instrument-tomcat` 模块包含了Tomcat的检测代理。

#### 2.2.3 消息
Spring4 包含了 `spring-messaging` 模块。改模块包含了Spring集成项目，比如Message，MessageChannel、MessageHandle和其他以消息为基础提供服务的应用的关键的抽象类。改模块同样包含一组从消息映射到方法的注解，就想SpringMVC中基于编程模型的注解。

#### 2.2.4 数据访问/集成
数据访问/集成层包含JDBC、ORM、OXM、JMS和事物模块。

`spring-jdbc` 提供了JDBC抽象层，它移除了冗长的JDBC编码，但解析了数据库 提供商定义的特定错误代码。

`spring-tx` 模块支持对实现特定接口的类和所有POJO（普通Java对象）的编程式和声明式的事务管理。

`spring-orm` 模块提供了对流行的对象-实体映射API的整合层，包含JPA，JDO，Hibernate和iBatis。使用`spring-orm` 模块你就可以使用全部的O/R-映射框架并联合其它Spring提供的特性，比如之前所提到的简单声明式的事务管理特性。

`spring-oxm` 模块提供了支持JAXB，Castor，XMLBeans，JiBX，以及Xstream对对象/XML映射实现的抽象层。

`spring-jms` 模块（JMS）模块包含生成和处理消息的特性。Spring 4.1 以后，它还提供了和 spring-messages 模块的整合。

#### 2.2.5 Web
Web层由`spring-web`、`spring-webmvc`、`spring-websocket`、和`spring-webmvc-portlet`组成。

`spring-web` 模块提供了面向web整合的基本特征，比如文件上传功能、使用Servlet监控初始化IoC容器以及面向web的上下文。该模块还包含了Http客户端和对于Spring远程访问中web相关的支持。

`spring-webmvc` 模块（也被称为Web-Servlet模块）有 Spring MVC 和 REST Web Service组成。Spring MVC框架提供了一个在领域模型代码和Web表单之间的整洁分离，并且整合了其它所有Spring框架的特性。

`spring-webmvc-portlet` 模块（也被称为 Web-Portlet模块）提供用于portlet环境和`spring-webmvc`模块功能镜像的MVC实现。

#### 2.2.6 测试
`spring-test` 模块通过JUnit和TestNG提供了Spring的组件的单元测试和集成测试。它提供了Spring 的ApplicationContexts 的一致加载并缓存这些上下文内容。它也提供mock对象，你可以用来单独的测试代码。

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
<repositories>
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

# Spring 4.x 的新特征

## 3 Spring4.0 的新特征和增强

Spring框架在2004年首次发布,之后有几个主要的大版本:Spring 2.0 XML名称空间和AspectJ提供支持;Spring 2.5支持注解驱动配置;Spring 3.0引入了一个强大的Java 5 +基础框架代码库和特性,比如Java的`@Configuration`模型。

4.0版本是最近的一个主要版本，是第一次完全支持Java8的特征。当然你还是可以用旧版本的Java来运行Spring，但是，我们已经把最低的要求提升到了JavaSE 6，我们也趁着这个主要版本的机会，删除了一些废弃的类和方法。

[升级到Spring4.0的迁移手册](https://github.com/spring-projects/spring-framework/wiki/Migrating-from-earlier-versions-of-the-spring-framework)，在 [Spring Framework GitHub Wiki](https://github.com/spring-projects/spring-framework/wiki)。

### 3.1 提升了“入门”的体验

新的[spring.io](https://spring.io)网站提供了一整套的[“入门”](https://spring.io/guides)手册以帮助学习Spring。在[第一章，Spring入门](#1-spring入门)中有更多的介绍。新网站还提供了关于Spring下面额外项目的全面的概述。

Spring现在在每个RELEASE版本中都会发布一个POM文件清单[BOM（bill of materials）](#maven的bom依赖),如果你是个Maven用户可能会对此比较感兴趣。

### 3.2 删除废弃的包和方法

在Spring4.0删除了所有废弃的包和一些废弃的类和方法。升级前请确保对旧API的依赖都已经修改过来了。

完整的差异报告，请查看[API差异报告](http://docs.spring.io/spring-framework/docs/3.2.4.RELEASE_to_4.0.0.RELEASE/)。

注意，依赖的第三方插件的版本已经提升到到了2010/2011期间的最低版本（例如：Spring4一般只支持2010年末以后的版本）：尤其是：Hibernate 3.6+, EhCache 2.1+, Quartz 1.8+, Groovy 1.8+, and Joda-Time 2.0+。有个例外的情况，Spring4 要求 Hibernate Validator 4.3+，Jackson 2.0+（Spring3.2 仍保留对 Jackson 1.8/1.9的支持。现在只是废弃的形式）。

### 3.3 Java8以及6和7

Spring4 支持Java8的一些特征。使用lambda表达式和方法引用Spring的回调接口。完美的支持 `java.time`([JSR-310](https://jcp.org/en/jsr/detail?id=310))，以及使用 `@Repeatable` 重写了一些注解。可以使用Java8的 parameter name discovery 机制（基于 `-parameters` 编译标识）。

Spring仍兼容旧版本的Java JDK:具体地说,Java SE 6(具体来说,最低级别相当于JDK 6更新18日发布2010年1月)及以上仍完全支持。然而,对于基于Spring4刚开始发开的项目,我们建议使用Java 7或8。

### 3.4 JavaEE6和7
JavaEE6以及以上被认为是Spring4的基线，对JAP2.0 和Servlet3.0规范有特殊的意义。为了兼容Google App Engine 和旧版本的应用服务器，可以将Spring4的应用部署到Servlet2.5的环境，但是Servlet3.0+的环境是Spring test和mock包测试步骤的先决条件。

> 如果你是一个WebSphere 7用户,一定要安装JPA 2.0 feature pack。在WebLogic 10.3.4或更高版本,安装的JPA 2.0补丁。这就是可以变成Spring4的部署环境。

更有远见的是Spring4支持JavaEE7级别的适用性规范：尤其是，JMS 2.0, JTA 1.2, JPA 2.1, Bean Validation 1.1, and JSR-236 Concurrency Utilities，像往常一样,这种支持侧重于个人使用的规范,如在Tomcat或在独立的环境中。然而,它可以同样地工作当一个Spring应用程序部署到Java EE 7服务器。

注意,Hibernate 4.3是一个JPA 2.1提供者,因此仅支持4.0的Spring框架。这同样适用于Hibernate Validator 5.0作为Bean Validation 1.1提供者。Spring Framework 3.2是都不支持的。

### 3.5 Groovy Bean Definition DSL

Spring4.0 开始，可以用Groovy DSL定义外部bean的配置，比XML定义bean更简洁。使用Groovy还允许您轻松地将bean定义直接嵌入你的启动代码。例如:

```groovy
def reader = new GroovyBeanDefinitionReader(myApplicationContext)
reader.beans {
    dataSource(BasicDataSource) {
        driverClassName = "org.hsqldb.jdbcDriver"
        url = "jdbc:hsqldb:mem:grailsDB"
        username = "sa"
        password = ""
        settings = [mynew:"setting"]
    }
    sessionFactory(SessionFactory) {
        dataSource = dataSource
    }
    myService(MyService) {
        nestedBean = { AnotherBean bean ->
            dataSource = dataSource
        }
    }
}
```
更多的信息请查阅 `GroovyBeanDefinitionReader` [javadocs](http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/beans/factory/groovy/GroovyBeanDefinitionReader.html)。

### 3.6 核心容器的改进

核心容器的综合改进如下：
* Spring现在把[泛型作为注入Bean的限定符]()。例如：当使用Spring 数据 `Repository`时，你可以注入具体的实现：`@Autowired Repository<Customer> customerRepository`。
* 如果你使用Spring的元注解支持，你现在可以开发自定义注解来[公开源注解的特定属性]()。
* 当[自动装配到lists和arrays]()时，Beans现在可以被 排序 了。支持`@Order`注解和`Ordered`接口两种方式。
* `@Lazy`注解现在可以用在注入点以及`@Bean`定义上。
* [引入]()`@Description`注解,开发人员可以使用基于Java方式的配置。
* 根据[条件筛选Beans]()的广义模型通过`@Conditional`注解加入。这和`@Profile`支持的类似，但是允许以编程式开发用户定义的策略。
* [基于CGLIB的代理类]()不在需要默认的构造方法。这个支持是由 [objenesis]()库提供。这个库重新打包到Spring框架中，作为Spring框架的一部分发布。通过这个策略，针对代理实例被调用没有构造可言了。
* 框架现在支持管理时区。例如`LocaleContext`。

### 3.7 Web改进

现在仍然可以部署到Servlet 2.5服务器，但是Spring4.0现在主要集中在Servlet 3.0+环境。如果你使用[Spring MVC测试框架]()，你需要将Servlet 3.0兼容的JAR包放到 测试的classpath下。

除了稍后会提到的WebSocket支持外，下面的常规改进已经加入到Spring的Web模块：
* 你可以在Spring MVC应用中使用[新的`@RestController`注解]()，不在需要给`@RequestMapping`的方法添加`@ResponseBody`注解。
* `AsyncRestTemplate`类已被添加进来，当开发REST客户端时，允许非阻塞异步支持。
* 当开发Spring MVC应用时，Spring现在提供了[全面的时区支持]() 。

### 3.8 WebSocket、SockJS和STOMP消息

一个新的`spring-websocket`模块提供了全面的基于WebSocket和在Web应用的客户端和服务器之间双向通信的支持。它和Java WebSocket API [JSR-356](https://jcp.org/en/jsr/detail?id=356)兼容，此外还提供了当浏览器不支持WebSocket协议时的基于SockJS的备用选项。

一个新的`spring-messaging`模块添加了支持STOMP作为WebSocket子协议用于在应用中使用注解编程模型路由和处理从WebSocket客户端发送的STOMP消息。由于`@Controller`现在可以同时包含`@RequestMapping`和`@MessageMapping`方法用于处理HTTP请求和来自WebSocket连接客户端发送的消息。新的`spring-messaging`模块还包含了来自以前Spring集成项目的关键抽象，例如`Message`、`MessageChannel`、`MessageHandler`和其他作为基于消息传递的应用程序的基础。

欲知详情以及较全面的介绍，请参见[Chapter 20, WebSocket]() 支持一节。

### 3.9 测试改进

除了精简`spring-test`模块中过时的代码外，Spring4还引入了几个用于单元测试和集成测试的新功能。

* 几乎`spring-test`模块中所有的注解（例如：`@ContextConfiguration`、`@WebAppConfiguration`、`@ContextHierarchy`、`@ActiveProfiles`等等)现在可以用作[元注解]()来创建自定义的composed annotations并且可以减少测试套件的配置。
* 现在可以以编程方式解决Bean定义配置文件的激活。只需要实现一个自定义的`ActiveProfilesResolver`，并且通过`@ActiveProfiles`的`resolver`属性注册。
* 新的`SocketUtils`类被引入到了`spring-core`模块。这个类可以使你能够扫描本地主机的空闲的TCP和UDP服务端口。这个功能不是专门用在测试的，但是可以证明在你使用Socket写集成测试的时候非常有用。例如测试内存中启动的SMTP服务器，FTP服务器，Servlet容器等。
* 从Spring 4.0开始,`org.springframework.mock.web`包中的一套mock是基于Servlet 3.0 API。此外，一些Servlet API mocks（例如：`MockHttpServletRequest`、`MockServletContext`等等）已经有一些小的改进更新，提高了可配置性。

## 4 Spring 4.1增强和新功能

### 4.1 JMS改进

Spring 4.1引入了一个更简单的基础架构，使用 `@JmsListener`注解bean方法来[注册JMS监听端点]()。XML命名空间已经通过增强来支持这种新的方式（`jms:annotation-driven`），它也可以完全通过Java配置( `@EnableJms`, `JmsListenerContainerFactory`)来配置架构。也可以使用 `JmsListenerConfigurer`注解来注册监听端点。

Spring 4.1还调整了JMS的支持，使得你可以从`spring-messaging`在Spring4.0引入的抽象获益，即：
* 消息监听端点可以有更为灵活的签名，并且可以从标准的消息注解获益，例如`@Payload`、`@Header`、`@Headers`和`@SendTo`注解。另外，也可以使用一个标准的消息，以代替`javax.jms.Message`作为方法参数。
* 一个新的可用 `JmsMessageOperations`接口和允许操作使用`Message`抽象的`JmsTemplate`。

最后，Spring 4.1提供了其他各种各样的改进：
* `JmsTemplate`中的同步请求-答复操作支持
* 监听器的优先权可以指定每个`<jms:listener/>`元素
* 消息侦听器容器恢复选项可以通过使用 `BackOff` 实现进行配置
* JMS 2.0消费者支持共享

### 4.2 Caching改进

Spring 4.1 支持[JCache (JSR-107)]()注解使用Spring的现有缓存配置和基础结构的抽象；使用标准注解不需要任何更改。

Spring 4.1也极大地提高了自己的缓存抽象:

* 在运行时使用`CacheResolver`解决缓存，不在强制使用`value`参数定义缓存名称。
* 更多的自定义作业层：缓存解析器、缓存管理器、key生成器。
* 新的[类级别的注解]()`@CacheConfig`，允许在类级别上共享常用配置，不需要启用任何缓存操作。
* 使用`CacheErrorHandler`更好的处理缓存方法的异常。

Spring 4.1为了在`CacheInterface`添加一个新的`putIfAbsent`方法也做了重大的更改。

### 4.3 Web改进

* 通过新的抽象类 `ResourceResolver`, `ResourceTransformer`, 和`ResourceUrlProvider` 扩展了基于 `ResourceHttpRequestHandler` 对资源处理的支持。一些内置的实现提供资源URL版本控制（有效的HTTP缓存），定位gzip压缩的资源，生成一个HTML5 AppCache清单，以及更多的支持。参见[第21.16.9，“服务资源”]()。
* `@RequestParam`, `@RequestHeader`, and `@MatrixVariable` 支持Java 1.8 的`java.util.Optional`。
* 返回`ListenableFuture`类型的底层服务（又或者`AsyncRestTemplate`的调用）支持用`ListenableFuture` 替换`DeferredResult` 作为返回值。
* `@ModelAttribute` 方法可以在循环依赖的顺序中调用。参见 [SPR-6299](https://jira.spring.io/browse/SPR-6299).
* Jackson的 `@JsonView` 可以直接使用在 `@ResponseBody` 和 `ResponseEntity` controller的方法上，序列化同一个POJO对象，返回不同数量的细节（例如概要与详细信息页面）。支持基于视图的渲染通过添加序列化视图类型作为model属性下的特殊的key的方法。详情参见：[Jackson Serialization View Support章节]()。
* 支持Jackson JSONP。详情参见：[Jackson JSONP Support章节]()
* 一个新的可用的生命周期选项拦截在`@ResponseBody` 和 `ResponseEntity` 作用的方法在return之后和response返回之前。在实现`ResponseBodyAdvice`的Bean上声明`@ControllerAdvice`。`@JsonView` 和JSONP利用这个实现的。详情参见：[Intercepting requests with a HandlerInterceptor章节]()。
* 三种新的`HttpMessageConverter` 选项：
    * Gson —较Jackson更轻量级。已经被用在了Spring Android。
    * Google Protocol Buffers — 在一个企业里面，服务间行之有效的通信数据协议，亦可以公开为JSON和XML的浏览器。
    * 通过对[jackson-dataformat-xml](https://github.com/FasterXML/jackson-dataformat-xml)扩展支持基于XML序列化的Jackson。如果jackson-dataformat-xml在classpath中，在使用 `@EnableWebMvc` 或者 `<mvc:annotation-driven/>`的时候，将默认使用这个替代JAXB2。
* 可以通过名称建立Controller 和 View 比如 JSP的联系。默认的名称是每个`@RequestMapping`，比如`FooController` 有个`handleFoo` 方法，命名为“FC#handleFoo”。命名策略是可插拔的。另外，也可以通过其名称属性明确命名一个`@RequestMapping`。在Spring JSP标签库中的一个新的`mvcUrl`功能使这个容易在JSP页面中使用。参见[第21.7.2章，“Building URIs to Controllers and methods from views”]()。
* `ResponseEntity` 提供了一个建造者风格的API，用来指导Controller的method对服务端响应的准备,例如`ResponseEntity.ok()`。
* `RequestEntity`是一种新类型,它提供了一个构建式API来引导客户端代码对HTTP请求的准备。
* MVC Java配置和XML名称空间:
    * 视图解析器现支持配置 content negotiation,参见[21.16.8”视图解析器”]()。
    * 视图控制器有内置了重定向和设置response状态码的支持。一个应用可以使用这个配置重定向url，返回的404页面，发送“无内容”的响应，等等。这里列出一些[用例](https://jira.spring.io/browse/SPR-11543?focusedCommentId=100308&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-100308)。
    * 内置了自定义path matching功能。详见 [第 21.16.11 章， “Path Matching”]()。
* [Groovy支持(基于Groovy 2.3)标记模板]()。见`GroovyMarkupConfigurer` 和 各自的 `ViewResolver` 以及 'View'的实现类。

### 4.4 WebSocket Messaging 改进

* SockJS (Java)的客户端支持。见`SockJsClient` 和同一个包的其他类。
* STOMP客户订阅和退订时新的应用程序上下文事件`SessionSubscribeEvent` 和 `SessionUnsubscribeEvent` 被发布。
* 新的“websocket”作用域，见第 [25.4.14章“WebSocket Scope”]()。
* `@SendToUser` 可以把单个session和不需要身份验证的用户作为目标。
* `@MessageMapping` 可以使用“.”代替“/”作为分隔符。见[SPR-11660]()。
* STOMP/ WebSocket监测信息被收集和记录。见[第25.4.16章 “Runtime Monitoring”]()。
* 显著优化和改进的记录应保持非常可读的和紧凑的甚至在调试水平。
* 优化信息创建包括支持临时消息可变性和避免自动消息id和时间戳的创建。见`MessageHeaderAccessor`的Javadoc。
* 关闭WebSocket会话建立后60秒内没有活动的STOMP/WebSocket连接。见[SPR-11884]()。

### 4.5 Testing 改进

* 现在可以用于配置Groovy脚本加载`ApplicationContext`的集成测试和TestContext框架。
    * 详见：[“Context configuration with Groovy scripts”]()。
* Test-managed事务现在可以通过编程的方式开始和结束事务通过新的`TestTransaction` API测试方法。
    * 详见：[“Programmatic transaction management”]()。
* SQL脚本执行现在可以通过新的`@Sql`和以声明的方式配置`@SqlConfig`注释在每个类、每个方法的基础上。
    * 详见：[14.5.7章 “Executing SQL scripts”]()。
* 通过新的 `@TestPropertySource` 注解配置property sources 。
    * 详见：[“Context configuration with test property sources”]()。
* 现在可以自动发现默认的TestExecutionListeners。
    * 详见： [“Automatic discovery of default TestExecutionListeners”]()。
* 自定义的TestExecutionListeners 可以和默认的listener自动合并。
    * 详见： [“Merging TestExecutionListeners”]() 。
* TestContext框架中事物测试的文档已得到改进。增加了更多的全面的解释和和例子。
    * 详见：[14.5.6章，“Transaction management”]()。
* `MockServletContext`, `MockHttpServletRequest`, 和 其他 Servlet API mock的全方面的改进。
* `AssertThrows` 已被重构，支持 `Throwable` ，替代了原来的`Exception`。
* 在 Spring MVC Test,JSON响应可以用 JSON Assert断言， [JSONPath]() 作为一个额外的选项可以被使用。就像使用XMLUtil断言XML。
* `MockMvcBuilder` 可以在 `MockMvcConfigurer`帮助下创建。他的增加使得Spring Security设置更容易应用，但可以用来封装常见设置任何第三方框架或在一个项目中。
* `MockRestServiceServer` 现在支持 `AsyncRestTemplate` 客户端测试。

## 5 Spring 4.2增强和新功能

### 5.1 核心容器的改进

* 注解`@Bean`可以在Java8的默认方法上被检测和处理，允许使用`@Bean`在默认的方法上组合配置类。
* 配置类现在可以通过声明`@Import`引入常规的组件类，允许混合引入配置类和组件类。
* 配置类现在可以声明`@Order`的值，使其能按预期的顺序来处理, 比如(通过名字来覆盖Bean配置等)。
* `@Resource`注解的元素, 现在可以配合`@Lazy`, 和`@Autowired`一样, 注入代理类, 来代理对应bean的请求。
* application event那套现在提供了[注解支持]()，以及发布任意事件的能力。
    * 被管理的类中的任何一个使用`@EventListener` 注解的public方法，都可以消费事件。
    * `@TransactionalEventListener`提供交易绑定的事件支持。
* Spring4.2引入了对注解属性别名的完美支持。新@AliasFor注释可用于声明一对别名属性在一个注释中或在自定义的注解中声明一个属性的别名是元注解的一个属性。
    * 下面的这些注解为了使value属性的别名更有可读性，使用` @AliasFor` 进行了重写。`@Cacheable`, `@CacheEvict`, `@CachePut`, `@ComponentScan`, `@ComponentScan.Filter`, `@ImportResource`, `@Scope`, `@ManagedResource`, `@Header`, `@Payload`, `@SendToUser`, `@ActiveProfiles`, `@ContextConfiguration`, `@Sql`, `@TestExecutionListeners`, `@TestPropertySource`, `@Transactional`, `@ControllerAdvice`, `@CookieValue`, `@CrossOrigin`, `@MatrixVariable`,`@RequestHeader`, `@RequestMapping`, `@RequestParam`, `@RequestPart`, `@ResponseStatus`, `@SessionAttributes`, `@ActionMapping`, `@RenderMapping`, `@EventListener`, `@TransactionalEventListener`。
    * 比如，`spring-test` 模块中的`@ContextConfiguration` 现在的声明如下：
    ```java
    public @interface ContextConfiguration {

        @AliasFor("locations")
        String[] value() default {};

        @AliasFor("value")
        String[] locations() default {};

        // ...
    }
    ```
    * 同样，使用`@AliasFor`在组合注解的属性上，声明别名是元注解的一个`value`。
    * 例如：
    ```java
    @ContextConfiguration
    public @interface MyTestConfig {

        @AliasFor(annotation = ContextConfiguration.class, attribute = "value")
        String[] xmlFiles();

        // ...
    }
    ```
    * 见 [Spring Annotation Programming Model]() 。
* Spring在搜索元注解的算法上进行了提升，比如局部声明的注解比继承的注解更受到青睐。
* Map类型的的注解属性（和`AnnotationAttributes` 实例）可以被合成（即转换）到一个注解。
* 基于field的数据绑定（`DirectFieldAccessor`）功能已经和基于property的数据绑定（`BeanWrapper`）想符合。尤其是基于field的数据绑定现在支持Collection、 Array 和 Map 的导航。
* `DefaultConversionServic`e 为`Stream`, `Charset`, `Currency`, 和 `TimeZone` 提供了开箱即用的转换器。这种转换器可以单独添加任意`ConversionService`。
* 如果'javax.money'API在classpath中，`DefaultFormattingConversionService`提供了对JSR-354 Money & Currency 值类型的支持，也就是：`MonetaryAmount` 和 `CurrencyUnit`。包含了对`@NumberFormat`应用的支持。
* `@NumberFormat` 现在可以作为元注解使用。
* `JavaMailSenderImpl` 新增了`testConnection()` 方法，测试和服务器的连通性。
* `ScheduledTaskRegistrar` 公开计划任务。
* 支持Apache `commons-pool2` 作为AOP `CommonsPool2TargetSource`池。
* 引入`StandardScriptFactory`作为基于JSR-223的机制脚本化bean，开放XML中的`lang:std`节点。支持JavaScript和JRuby等。（注意：JRubyScriptFactory 和 `lang:jruby` 现在被废弃了。建议使用JSR-223。）

### 5.2 数据访问的提升

* 通过AspectJ支持`javax.transaction.Transactional`。
* `SimpleJdbcCallOperations` 支持名称绑定。
* 完全支持Hibernate ORM 5.0：通过它原生的API（被新的 `org.springframework.orm.hibernate5` 包覆盖）作为JPA的提供者（自动适配）。
* 嵌入式数据库现在可以自动分配独特的名字，并且`<jdbc:embedded-database>`支持新的`database-name` 属性。请参见下面的“Testing Improvements”为进一步的细节。

### 5.3 JMS改进

* 通过`JmsListenerContainerFactory`控制`autoStartup`属性。
* 每个监听容器都可以配置`Destination`应答的类型。
* `@SendTo` 的 value 可以用 SpEL表达式。
* 使用`JmsResponse`在[运行时计算]()响应的目标。
* 在同一个方法上，可是使用重复`@JmsListener`声明多个JMS 容器。（如果没有使用Java8，仍使用最新引入的`@JmsListeners`）

### 5.4 Web 改进

* 支持 HTTP Streaming 和  Server-Sent Events（服务器推送事件），详见[“HTTP Streaming”章节]()。
* 支持包含全局（MVC Java config and XML namespace）和本地（`@CrossOrigin`）配置的CORS（跨域资源共享）。详见[第26章 CORS Support细节]()。
* HTTP 缓存更新：
    * `ResponseEntity`, `WebContentGenerator`, `ResourceHttpRequestHandler`插入了新的`CacheControl`的builder。
    * 提升了对`WebRequest`中ETag/Last-Modified 的支持。
* 使用 `@RequestMapping`作为元注解，自定义映射注解。
* `AbstractHandlerMethodMappin`g 的public方法在运行时完成请求映射的注册和移除注册。
* `AbstractDispatcherServletInitializer` 的protected `createDispatcherServlet`方法，进一步定制化`DispatcherServlet` 实例。
* `HandlerMethod` 作为 `@ExceptionHandler`注解的方法参数,特别是方便了`@ControllerAdvice`组件。
* `java.util.concurrent.CompletableFuture`作为一个`@Controller` 方法的返回值类型。
* `HttpHeaders` 为了保存静态资源支持byte-range请求。
* nested exceptions能检测到`@ResponseStatus` 。
* `UriTemplateHandler` 作为 `RestTemplate` 的扩展点。
    * `DefaultUriTemplateHandler` 开放了 `baseUrl` 的 property 和 path segment 编码选项。
    * 扩展点也可以用来插入任何URI模板库。
* `RestTemplate`集成了[OkHttp]()。
* `MvcUriComponentsBuilder`中的方法可以选择自定义的`baseUrl`。
* 序列化/反序列化的异常信息调整到WARN级别日志。
* 默认的JSON前缀从“{} &&”调整到更安全的“)]}', ”。
* 新的`RequestBodyAdvice` 扩展点和内置的实现都支持Jackson的`@JsonView` 在`@ResponseBody`方法的参数上注解。
* 当使用 GSON 或者 Jackson 2.6+的时候，处理方法返回的类型用于提高参数化类型的序列化，例如 `List<Foo>`。
* 引入`ScriptTemplateView`作为基于JSR-223的机制，与Nashorn (JDK 8)中聚焦于JavaScript 视图的模板，脚本化web视图。

### 5.5 WebSocket Messaging 改进

* 公开已连接用户和订阅服务的状态信息：
    * 新的`SimpUserRegistry`作为名称是“userRegistry”的bean被公开。
    * 服务器集群共享状态信息。详见broker relay 配置选项。
* 服务器集群解决用户目标。详见broker relay 配置选项。
* `StompSubProtocolErrorHandler` 对客户端STOMP ERROR 框架的定制和控制进行了扩展。
* `@ControllerAdvice` 组件可以使用全局的`@MessageExceptionHandler` 方法。
* `SimpleBrokerMessageHandler` 为订阅服务增加了心跳机制和一个SpEL表达式“selector”的header。
* 基于 TCP 和 WebSocket上使用STOMP客户端。详见 [25.4.13 章，“STOMP Client”]()。
* `@SendTo` 和 `@SendToUser` 可以包含目标变量的占位符。
* `@MessageMapping` 和 `@SubscribeMapping`的返回值支持使用 Jackson的`@JsonView`。
* `ListenableFuture` 和 `CompletableFuture` 作为`@MessageMapping` 和 `@SubscribeMapping`的返回值类型。
* `MarshallingMessageConverter` 处理 XML payload。

### 5.6 Testing 改进

* 基于JUnit集成测试现在可以使用JUnit规则替代`SpringJUnit4ClassRunner`执行。这允许基于spring的集成测试可以和其他的runner，比如 JUnit的`Parameterized` 或者第三方的runner，比如`MockitoJUnitRunner`一起运行。
    * 见[“Spring JUnit Rules”章节的细节]()。
* Spring MVC Test框架完美了支撑了HtmlUnit，包括集成Selenium的WebDriver ，允许测试基于页面的web应用，而不需要部署到Servlet容器。
    * 见[14.6.2“HtmlUnit Integration”章节的细节]()。
* `AopTestUtils` 是一个新的测试工具。可以让开发人员获得隐藏在一个或多个Spring代理下面的目标对象的引用。
    * 见[13.2.1, “General testing utilities”章节的细节]()。
* `ReflectionTestUtils`支持 getting 和 setting `static` filed，包括构造器。
* 保留了`@ActiveProfiles` 声明bend定义的顺序的配置，为了支持根据激活的profile的名称加载配置文件的测试用例，比如Spring Boot的 `ConfigFileApplicationListener`。
* `@DirtiesContext` 支持在测试结束之前使用 `BEFORE_METHOD`, `BEFORE_CLASS` 和 `BEFORE_EACH_TEST_METHOD` 这些方法关闭 `ApplicationContext` 。比如一些破坏性（即，有待决定的）测试在一个大的测试集，已经破坏了`ApplicationContext`的原始配置。
* 一个新的注解`@Commit` ，也许可以代替`@Rollback(false)`。
* `@Rollback`可以配置默认的类级别语义。
* 因此，`@TransactionConfiguration` 被废弃，将会在接下来的版本中移除。
* `@Sql`现在支持通过一个新的`statements`属性执行内联SQL语句。
* 用于在测试用例中缓存ApplicationContexts 的缓存`ContextCache`，现在是一个public API 和一个默认的实现，这个实现是可以被用户缓存需求所取代的。
* `DefaultTestContext`, `DefaultBootstrapContext` 和 `DefaultCacheAwareContextLoaderDelegate` 现在是`support` 子包中的public class，允许自定义扩展。
* TestContextBootstrappers 现在负责构造`TestContext`。
* 在Spring MVC Test框架，`MvcResult`的细节，可以被记录为`DEBUG`级别或者输出到自定义的`OutputStream` 或`Writer`。详见`MockMvcResultHandlers`中新的方法 `log()`、`print(OutputStream)` 和 `print(Writer)`。
* JDBC XML 命名空间 `<jdbc:embedded-database>` 支持新的 `database-name` 属性。允许开发人员为嵌入式数据库设置唯一的名称。例如：通过SpEL表达式或占位符属性所影响的当前活动bean定义配置文件。
* 嵌入式数据库，可以被自动分配一个唯一的名称。允许在一个测试集合中复用通用测试数据库配置在不同的ApplicationContext。
    * 详见[18.8.6, “Generating unique names for embedded databases”]() 。
* `MockHttpServletRequest` 和 `MockHttpServletResponse` 通过 `getDateHeader` 和 `setDateHeader` 方法为格式化header中的date提供了更好的支持。

# 核心技术
## 6 IoC容器
### 6.1 Spring IoC 容器和Beans入门
 本章节阐述了Spring框架实现控制翻转（IoC）的原理。IoC也被称为依赖注入（DI）。应用控制反转，对象在被创建的时候，由一个调控系统内所有对象的外界实体，将其所依赖的对象的引用，传递给它。也可以说，依赖被注入到对象中。所以，控制反转是，关于一个对象如何获取他所依赖的对象的引用,这个责任的反转。

 `org.springframework.beans` 和 `org.springframework.context` 是Sprig 框架的 IoC 容器的基础包的。 `BeanFactory` 提供能够管理任何类型的对象的高级配置机制。 `ApplicationContext` 是 `BeanFactory` 的一个子接口。功能得到了进一步增强，更容易与Spring AOP 集成，资源处理，事件传递，各种不同应用层的上下文的实现(如，`WebApplicationContext`)。

 简而言之，`BeanFactory` 提供了配制框架及基本功能，`ApplicationContext` 添加了更多的企业特性的功能。`ApplicationContext` 是本章节中专门用来描述IoC的类，如果你想知道更多关于 `BeanFactory` 的资料，参见[6.16.BeanFactory]()。

 在Spring中，我们把那些被Spring IoC容器管理的关键对象(组成你应用程序的主体)称之为beans.一个Bean实际上是指一个被IOC容器管理，实例，装配的对象(object)。而bean定义以及bean相互间的依赖关系将通过配置元数据来描述。

### 6.2 容器

 `org.springframework.context.ApplicationContext` 对Bean的管理是通过读取配置元数据实现的。这种元数据可以表现为XML，Java注解或者Java代码。她描述了应用程序中复杂的依赖关系。

 Spring提供了一下即插即用的 `ApplicationContext`，如 `ClasspathXmlApplicationContext` 和 `FileSystemXmlApplicationContext`，我们可以用少量的XML配置元数据，其余的在这基础上使用注解或者代码来完成配置元数据。

 在大多数的应用程序中，并不需要用显式的代码去实例化一个或多个的Spring IoC容器实例。例如，在web应用程序中，我们只需要在 `web.xml` 中添加 (大约)8 行简单的XML描述符即可(见[6.15.4.ApplicationContext在WEB应用中的实例化]())，如果你使用[Spring Tool Suite](https://spring.io/tools/sts)，那配置仅仅需要按几下鼠标或者敲几下键盘即可。

 下面的插图解释了Spring是如何工作的：你的应用程序中的类全部结合在元数据配置中，当 `ApplicationContext` 被创建以及实例化后，你就拥有了一个完全配置好的、可执行的应用。

 **图6.1. Spring IoC容器**

 ![](../master/Spring/images/container-magic.png)

#### 6.2.1 配置元数据

 在前面的图中，我们知道IoC容器将读取配置元数据(_configuration metadata_)；并且从配置中读取应用程序各个对象的实例化，配置以及组装。

 通常我们使用简单直观的XML来配置。这是大多数本章使用转达Spring IoC容器的关键概念和功能。

 > 基于xml的元数据不是唯一允许的配置元数据形式。Spring IoC容器本身是完全脱离这个配置元数据的格式写。目前许多开发人员选择基于[java的方式]()配置Spring应用程序。

 使用其他形式的配置Spring容器元数据,见:

 * 注解的方式(Annotation-based)：Spring 2.5 开始支持注解方式配置元数据。
 * Java的方式(Java-based)：从Spring 3.0 开始，Spring JavaConfig项目为Spring框架提供很多特性。因此你可以使用Java定义你的应用之外的bean，而不是用XML文件定义。使用这些新特征，见 `@Configuration`，`@Bean`， `@Import` 和 `@DependsOn` 注解。

 XML配置方式在顶层的<beans/>元素配置一个或多个<bean/>元素。Java配置方式的话需要在类上注解`@Configuration`，同时方法上注解`@Bean`。

 bean定义与应用程序中实际使用的对象一一对应。通常情况下bean的定义包括：服务层对象、数据访问层对象（DAO）、类似Struts `Action`的 表示层对象、Hibernate `SessionFactory`对象、JMS `Queue`对象等等。通常bean的定义并不与容器中的领域 对象相同，因为领域对象的创建和加载必须依赖具体的DAO和业务逻辑。此外你可以通过`AspectJ`去配置那些不在IoC容器内创建的对象。见[使用AspectJ注入域对象]()。

 以下是一个基于XML的配置元数据的基本结构：

 ```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <beans xmlns="http://www.springframework.org/schema/beans"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://www.springframework.org/schema/beans
         http://www.springframework.org/schema/beans/spring-beans.xsd">

     <bean id="..." class="...">
         <!-- collaborators and configuration for this bean go here -->
     </bean>

     <bean id="..." class="...">
         <!-- collaborators and configuration for this bean go here -->
     </bean>

     <!-- more bean definitions go here -->

 </beans>
 ```
 `id`属性是一个用来唯一确认Bean的字符串。`class`属性需要填写类的完整的名称(路径.类)

 id属性的值是指协作对象，指协作对象的XML不是这个示例中所示；有关更多信息，请参见[依赖]()。

#### 6.2.2 实例化容器

 实例化容器实际上非常简单。本地路径或其他路径提供一个给ApplicationContext构造函数，实际上是资源字符串，使容器从本地文件系统、Java类路径等加载配置元数据以及各种各样的外部资源。

 ```java
 ApplicationContext context =
     new ClassPathXmlApplicationContext(new String[] {"services.xml", "daos.xml"});
 ```
 下面的例子展示了服务层的配置文件`(services.xml)`：

 ```xml
<?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd">

      <!-- services -->

      <bean id="petStore" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
          <property name="accountDao" ref="accountDao"/>
          <property name="itemDao" ref="itemDao"/>
          <!-- additional collaborators and configuration for this bean go here -->
      </bean>

      <!-- more bean definitions for services go here -->

  </beans>
  ```
 下面的例子展示了数据连接层的配置文件`(daos.xml)`：

 ```xml
<?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd">

      <bean id="accountDao"
          class="org.springframework.samples.jpetstore.dao.jpa.JpaAccountDao">
          <!-- additional collaborators and configuration for this bean go here -->
      </bean>

      <bean id="itemDao" class="org.springframework.samples.jpetstore.dao.jpa.JpaItemDao">
          <!-- additional collaborators and configuration for this bean go here -->
      </bean>

      <!-- more bean definitions for data access objects go here -->

  </beans>
  ```

  在前面的例子中，服务层的PetStoreServiceImpl注入了JpaAccountDao,JpaItemDao。其中property name指向JavaBean的成员属性，ref链接到JpaAccountDao,JpaItemDao中指定的id。

  **XML配置元数据的结构**

  将XML配置文件分拆成多个部分是非常有用的。通常每个单独的XML文件表示一个逻辑层或者模块。

  您可以使用应用程序上下文构造函数从所有这些 XML 片段加载 bean 定义。此构造函数采用 `Resource` 的多个位置，是上一节所示。或者，使用一个或多个 `<import/>` 元素，从另一个文件或文件加载 bean 定义。例如:

  ```xml
  <beans>
      <import resource="services.xml"/>
      <import resource="resources/messageSource.xml"/>
      <import resource="/resources/themeSource.xml"/>

      <bean id="bean1" class="..."/>
      <bean id="bean2" class="..."/>
  </beans>
  ```

 在上面的例子中，我们从3个外部文件：`services.xml`、 `messageSource.xml`及`themeSource.xml` 来加载bean定义。这里采用的都是相对路径，因此，此例中的`services.xml` 一定要与导入文件放在同一目录或类路径，而`messageSource.xml`和`themeSource.xml`的文件位置必须放在导入文件所 在目录下的`resources`目录中。正如你所看到的那样，开头的斜杠 ‘/’实际上可忽略。因此不用斜杠‘/’可能会更好一点。根据Spring XML配置文件的 Schema(或DTD)，被导入文件必须是完全有效的XML bean定义文件，且根节点必须为`<beans/>`元素。

 > 它是可以的但不是推荐，来引用使用相对的父目录中的文件"../"路径。这样做是在当前的应用程序外部的文件创建一个依赖项。尤其是，这一提法不适合"类路径中:"Url (例如，"类路径:../services.xml")，在运行时解析过程选择"最近"的类路径中根，然后看着它的父目录。类路径配置更改可能会导致选择的不同，不正确的目录。
  你可以使用完全限定的资源位置而不是相对路径: 例如，"file:C:/config/services.xml"或"classpath:/config/services.xml"。然而，要知道你耦合应用程序配置到特定的绝对位置。它一般最好是保持间接为这种绝对的位置，例如，通过对 JVM 系统属性在运行时解析的"${...}"占位符。

#### 6.2.3 使用容器

  在ApplicationContext中调用方法T getBean(String name, Class<T> requiredType)你就可以获得你定义Bean的实例化对象。如下例所示：

  ```java
  // create and configure beans
  ApplicationContext context =
      new ClassPathXmlApplicationContext(new String[] {"services.xml", "daos.xml"});

  // retrieve configured instance
  PetStoreService service = context.getBean("petStore", PetStoreService.class);

  // use configured instance
  List<String> userList = service.getUsernameList();
  ```

  `getBean()` 用于检索您的 bean 的实例。`ApplicationContext`接口有其他几种方法用于检索 bean ，但理想的情况是您的应用程序代码应该永远不会使用它们。事实上，应用程序代码应该根本没有调用 `getBean()` 方法，并因此没有依赖 Spring api。例如，Spring和 web 框架集成提供各种 web 框架类如控制器和 JSF 托管 bean 的依赖注入。

### 6.3 Bean

  Spring IoC容器将管理一个或多个bean，这些bean 将通过配置文件中的bean定义被创建(在XML格式中为`<bean/>`元素)。

  在容器内部，这些bean定义由`BeanDefinition`对象来表示，该定义将包含以下信息：

  * _全限定类名_：这通常就是已定义bean的实际实现类。
  * bean行为的定义，这些定义将决定bean在容器中的行为（作用域、生命周期回调等等）
  * 对其他bean的引用，这些引用bean也可以称之为协作bean（collaborators） 或依赖bean（dependencies）.
  * 创建bean实例时的其他配置设置。比如使用bean来定义连接池，可以通过属性或者构 造参数指定连接数，以及连接池大小限制等。

  上述内容直接被翻译为每个bean定义包含的一组properties。下面的表格列出了部分 内容的详细链接：

  **表 6.1. bean定义**

  | 名称          | 链接           |
  | ------------- |----------------|
  |class	|[6.3.2, “实例化bean”]()|
  |name	|[6.3.1, “bean的命名”]()  |
  |scope	|[6.5, “Bean的作用域”]() |
  |constructor arguments	|[6.4.1, “依赖注入”]()|
  |properties	|[6.4.1, “依赖注入”]()            |
  |autowiring mode	|[6.4.5, “自动装配（autowire）协作者”]()|
  |dependency checking mode	|[6.4.5, “依赖检查”]()     |
  |lazy-initialization mode	|[6.4.4, “延迟初始化bean”]()|
  |initialization method	|[初始化回调]()  |
  |destruction method	|[析构回调]()    |

  除了通过bean定义来描述要创建的指定bean的属性之外，某些`BeanFactory`的实现也允许将那些非`BeanFactory`创建的、已有的用户对象注册到容器中，比如使用`DefaultListableBeanFactory` 的`registerSingleton(..)`方法。不过大多数应用还是采用 元数据定义为主。

  >Bean的元数据和手动单例实例需要尽早注册，为了使容器正确推断它们在自动装配和其他内省的步骤。虽然在某些程度上支持重写元数据和单例，但是在运行时注册新的bean不是官方支持的，可能会导致并发访问的异常并且出现不一致的状态在bean容器中。

#### 6.3.1 Bean 的命名

  每一个Bean都可以注册一个或多个标识符，但这些标识符必须在容器管理的范围内保持唯一。通常我们一个Bean只会注册一个标识符，其他的我们用别名来表示。

  在XML配置文件中，你可以使用`id`或者`name`属性来区分Bean。`id`属性中你有且只能有一个id，以字母数字的方式组成(如：myBean, fooService等)，但如果你想要起多个别名，你可以在`name`属性中使用逗号(`,`)，分号(`;`)或者空格来间隔开。做个历史说明，在Spring 3.1以前`id`属性被定为`xsd:ID`类型，限制可能的字符。3.1以后的版本中定为`xsd:string`类型，虽然不在通过XML解析器解析，但依旧强制要求唯一性。

  id和name不是bean必须的，如果没有显示提供id或者name，容器会自动生成一个唯一的name。但是，如果想通过`ref`或者[服务定位器模式]()根据name查找bean，你必须提供一个name，因为不支持name跟使用中的[内部bean]()和[自动装配的协作对象]()相关。

  ```
  bean命名约定

    bean的命名采用标准的Java命名约定，即小写字母开头，首字母大写间隔 的命名方式。如`accountManager`、`accountService`、`userDao`及`loginController`，等等。
    对bean采用统一的命名约定将会使配置更加简单易懂。而且在使用Spring AOP时 ，如果要发通知(advice)给与一组名称相关的bean时，这种简单的命名方式将会令你受益匪浅。
  ```

  **bean的别名**

  在对bean进行定义时，除了使用`id`属性来指定名称之外，为了提供多个名称，需要通过`name`属性来加以指定。而所有的这些名称都指向同一个bean，在某些情况下提供别名非常有用，比如为了让应用的每一个组件能更容易的对公共组件进行引用。

  然而，在定义bean时就指定所有的别名并不是总是恰当的。有时我们期望 能在当前位置为那些在别处定义的bean引入别名。在XML配置文件中，可用 `<alias/>` 元素来完成bean别名的定义。如：

  ```xml
  <alias name="fromName" alias="toName"/>
  ```

  在这个例子中，bean的name是`fromName`，别名是`toName`。

  考虑一个更为具体的例子，子系统A在XML配置文件中定义了一个名为`subsystemA-dataSource`的DataSource bean。但子系统B却想在其XML文件中以`subsystemB-dataSource`的名字来引用此bean。而且在主程序MyApp的XML配置文件中，希望以`myApp-dataSource`的名字来引用此bean。最后容器加载三个XML文件来生成最终的`ApplicationContext`，在此情形下，可通过在MyApp XML文件中添加下列alias元素来实现：

```xml
<alias name="subsystemA-dataSource" alias="subsystemB-dataSource"/>
<alias name="subsystemA-dataSource" alias="myApp-dataSource" />
```

  这样一来，每个组件及主程序就可通过唯一名字来引用同一个数据源而互不干扰。

  ```
  Java-configuration

  如果使用的是Java-configuration，@Bean注解支持别名，详见[6.12.3，“@Bean注解的应用”]()。
  ```

#### 6.3.2 实例化Bean

  从本质上来说，bean定义描述了如何创建一个或多个对象实例。当需要的时候， 容器会从bean定义列表中取得一个指定的bean定义，并根据bean定义里面的配置元数据 使用反射机制来创建（或取得）一个实际的对象。

  当采用XML描述配置元数据时，将通过`<bean/>`元素的`class`属性来指定实例化对象的类型。`class` 属性 (对应`BeanDefinition`实例的`Class`属性)通常是必须的(不过也有两种例外的情形，见 [使用实例工厂方法实例化]()和 [6.7.bean定义的继承]())。`Class`属性主要有两种用途 ：

  * 在大多数情况下，容器将直接通过反射调用指定类的构造器来创建bean(这有点类似于 在Java代码中使用`new`操作符)。
  * 在极少数情况下，容器将调用 类的静态工厂方法来创建bean实例，class 属性将用来指定实际具有静态工厂方法的类(至于调用静态工厂方法创建的对象类型是当前class还是其他的class则无关紧要)。

  ```
  内部类名

    如果需要你希望将一个静态的内部类配置为一个bean的话，那么内部类的名字需要采用二进制的写法。
    比如说，在`com.example`包下有一个叫`Foo`的类，而`Foo`类有一个静态的内部类叫`Bar`，那么在bean定义的时候，`class`属性必须这样写：
    `com.example.Foo$Bar`
    注意这里我们使用了`$`字符将内部类和外部类进行分隔
  ```

  **用构造器来实例化**

  当采用构造器来创建bean实例时，Spring对class并没有特殊的要求，我们通常使用的class都适用。也就是说，被创建的类并不需要实现任何特定的接口，或以特定的方式编码，只要指定bean的class属性即可。不过根据所采用的IoC类型，class可能需要一个默认的空构造器。

  此外，IoC容器不仅限于管理JavaBean，它可以管理任意的类。不过大多数使用Spring的人喜欢使用实际的JavaBean(具有默认的(无参)构造器及setter和getter方法)，但在容器中使用非bean形式(non-bean style)的类也是可以的。比如遗留系统中的连接池，很显然它与JavaBean规范不符，但Spring也能管理它。

  当使用基于XML的元数据配置文件，可以这样来指定bean类：

  ```xml
  <bean id="exampleBean" class="examples.ExampleBean"/>

  <bean name="anotherExample" class="examples.ExampleBeanTwo"/>
  ```

  给构造函数指定参数以及为bean实例设置属性将在随后的[依赖注入]()中谈及。

  **使用静态工厂方法实例化**

  当采用静态工厂方法创建bean时，除了需要指定`class`属性外，还需要通过`factory-method`属性来指定创建bean实例的工厂方法。Spring将调用此方法(其可选参数接下来介绍)返回实例对象，就此而言，跟通过普通构造器创建类实例没什么两样。

  下面的bean定义展示了如何通过工厂方法来创建bean实例。注意，此定义并未指定返回对象的类型，仅指定该类包含的工厂方法。在此例中，`createInstance()`必须是一个`static`方法。

  ```xml
  <bean id="clientService"
        class="examples.ClientService"
        factory-method="createInstance"/>
  ```

  ```java
  public class ClientService {
        private static ClientService clientService = new ClientService();
        private ClientService() {}

        public static ClientService createInstance() {
            return clientService;
        }
    }
  ```

  给工厂方法指定参数以及为bean实例设置属性将在随后的部份中谈及。

  **使用实例工厂方法实例化**

  与使用静态工厂方法实例化类似，用来进行实例化的非静态实例工厂方法位于另外一个bean中，容器将调用该bean的工厂方法来创建一个新的bean实例。为使 用此机制，`class`属性必须为空，而`factory-bean`属性必须指定为当前(或其祖先)容器中包含工厂方法的bean的名称，而该工厂bean的工厂方法本身必须通过`factory-method`属性来设定。

  ```xml
  <!-- the factory bean, which contains a method called createInstance() -->
  <bean id="serviceLocator" class="examples.DefaultServiceLocator">
      <!-- inject any dependencies required by this locator bean -->
  </bean>

  <!-- the bean to be created via the factory bean -->
  <bean id="clientService"
      factory-bean="serviceLocator"
      factory-method="createClientServiceInstance"/>
  ```

  ```java
  public class DefaultServiceLocator {

      private static ClientService clientService = new ClientServiceImpl();
      private DefaultServiceLocator() {}

      public ClientService createClientServiceInstance() {
          return clientService;
      }
  }
  ```

  一个工厂类同样可以用多个 factory method

  ```xml
  <bean id="serviceLocator" class="examples.DefaultServiceLocator">
      <!-- inject any dependencies required by this locator bean -->
  </bean>

  <bean id="clientService"
      factory-bean="serviceLocator"
      factory-method="createClientServiceInstance"/>

  <bean id="accountService"
      factory-bean="serviceLocator"
      factory-method="createAccountServiceInstance"/>
  ```

  ```java
  public class DefaultServiceLocator {

      private static ClientService clientService = new ClientServiceImpl();
      private static AccountService accountService = new AccountServiceImpl();

      private DefaultServiceLocator() {}

      public ClientService createClientServiceInstance() {
          return clientService;
      }

      public AccountService createAccountServiceInstance() {
          return accountService;
      }

  }
  ```

  虽然设置bean属性的机制仍然在这里被提及，但隐式的做法是由工厂bean自己来管理以及通过依赖注入(DI)来进行配置。

  >Spring文档中的factory bean指的是配置在Spring容器中通过使用 [实例]() 或 [静态工厂方法]()创建对象的一种bean。而文档中的`FactoryBean` （注意首字母大写）指的是Spring特有的 `FactoryBean`。

### 6.4 依赖

  典型的企业应用不会只由单一的对象（或Spring的术语bean)组成。毫无疑问，即使最简单的系统也需要多个对象共同来展示给用户一个整体的应用。接下来的的内容除了阐述如何单独定义一系列bean外，还将描述如何让这些bean对象一起协同工作来实现一个完整的真实应用。

#### 6.4.1 依赖注入

  依赖注入（DI）背后的基本原理是对象之间的依赖关系（即一起工作的其它对象）只会通过以下几种方式来实现：构造器的参数、工厂方法的参数，或给由构造函数或者工厂方法创建的对象设置属性。因此，容器的工作就是创建bean时注入那些依赖关系。相对于由bean自己来控制其实例化、直接在构造器中指定依赖关系或者类似服务定位器（Service Locator）模式这3种自主控制依赖关系注入的方法来说，控制从根本上发生了倒转，这也正是控制反转（Inversion of Control， IoC） 名字的由来。

  应用DI原则后，代码将更加清晰。而且当bean自己不再担心对象之间的依赖关系（甚至不知道依赖的定义指定地方和依赖的实际类）之后，实现更高层次的松耦合将易如反掌。同样的，你的类测试更加容易，尤其是在依赖接口或者抽象类的时候，可同通过部分实现或者模拟实现完成单元测试。

  DI主要有两种注入方式，即[Setter注入]()和[构造器注入]()。

  **构造器注入**

  基于构造器的DI通过调用带参数的构造器来实现，每个参数代表着一个依赖。此外，还可通过给静态工厂方法传参数来构造bean。接下来的介绍将认为给构造器传参与给静态工厂方法传参是类似的。下面展示了只能使用构造器参数来注入依赖关系的例子。请注意，这个类并没有什么特别之处。

  ```java
  public class SimpleMovieLister {

        // the SimpleMovieLister has a dependency on a MovieFinder
        private MovieFinder movieFinder;

        // a constructor so that the Spring container can inject a MovieFinder
        public SimpleMovieLister(MovieFinder movieFinder) {
            this.movieFinder = movieFinder;
        }

        // business logic that actually uses the injected MovieFinder is omitted...

    }
  ```

  **构造器参数解析**

  构造器参数解析根据参数类型进行匹配，如果bean的构造器参数类型定义非常明确，那么在bean被实例化的时候，bean定义中构造器参数的定义顺序就是这些参数的顺序，依次进行匹配，比如下面的代码

  ```java
  package x.y;

    public class Foo {

        public Foo(Bar bar, Baz baz) {
            // ...
        }

    }
  ```

  上述例子中由于构造参数非常明确（这里我们假定`Bar`和`Baz`之间不存在继承关系）。因此下面的配置即使没有明确指定构造参数顺序（和类型）也会工作的很好。

  ```xml
  <beans>
        <bean id="foo" class="x.y.Foo">
            <constructor-arg ref="bar"/>
            <constructor-arg ref="baz"/>
        </bean>

        <bean id="bar" class="x.y.Bar"/>

        <bean id="baz" class="x.y.Baz"/>
    </beans>
  ```

  我们再来看另一个bean，该bean的构造参数类型已知，匹配也没有问题(跟前面的例子一样)。但是当使用简单类型时，比如`<value>true<value>`，Spring将无法知道该值的类型。不借助其他帮助，他将无法仅仅根据参数类型进行匹配，比如下面的这个例子：

  ```java
  package examples;

    public class ExampleBean {

        // Number of years to calculate the Ultimate Answer
        private int years;

        // The Answer to Life, the Universe, and Everything
        private String ultimateAnswer;

        public ExampleBean(int years, String ultimateAnswer) {
            this.years = years;
            this.ultimateAnswer = ultimateAnswer;
        }

    }
  ```

  针对上面的场景可以通过使用`type`属性来显式指定那些简单类型的构造参数的类型，比如：

  ```xml
  <bean id="exampleBean" class="examples.ExampleBean">
        <constructor-arg type="int" value="7500000"/>
        <constructor-arg type="java.lang.String" value="42"/>
    </bean>
  ```

  我们还可以通过`index`属性来显式指定构造参数的索引，比如下面的例子：

  ```xml
  <bean id="exampleBean" class="examples.ExampleBean">
        <constructor-arg index="0" value="7500000"/>
        <constructor-arg index="1" value="42"/>
    </bean>
  ```

  通过使用索引属性不但可以解决多个简单属性的混淆问题，还可以解决有可能有相同类型的2个构造参数的混淆问题了，注意*index*是从0开始。

  我们更可以使用构造器上的参数名来传递：

  ```xml
  <bean id="exampleBean" class="examples.ExampleBean">
        <constructor-arg name="years" value="7500000"/>
        <constructor-arg name="ultimateAnswer" value="42"/>
    </bean>
  ```

  这种注入方法有个风险就是如果你的源代码在编译时关闭了debug标志，那么Spring就无法获取构造器的参数名了。不过可以使用`@ConstructorProperties`属性显式指定构造器参数名称。

  ```java
  package examples;

    public class ExampleBean {

        // Fields omitted

        @ConstructorProperties({"years", "ultimateAnswer"})
        public ExampleBean(int years, String ultimateAnswer) {
            this.years = years;
            this.ultimateAnswer = ultimateAnswer;
        }

    }
  ```

  **Setter注入**

  通过调用无参构造器或无参`static`工厂方法实例化bean之后，调用该bean的setter方法，即可实现基于setter的DI。 下面的例子将展示只使用setter注入依赖。注意，这个类并没有什么特别之处，它就是普通的Java类。

  ```java
  public class SimpleMovieLister {

        // the SimpleMovieLister has a dependency on the MovieFinder
        private MovieFinder movieFinder;

        // a setter method so that the Spring container can inject a MovieFinder
        public void setMovieFinder(MovieFinder movieFinder) {
            this.movieFinder = movieFinder;
        }

        // business logic that actually uses the injected MovieFinder is omitted...

    }
  ```

  `BeanFactory`对于它所管理的bean提供两种注入依赖方式（实际上它也支持同时使用构造器注入和Setter方式注入依赖）。需要注入的依赖将保存在`BeanDefinition`中，它能根据指定的`PropertyEditor`实现将属性从一种格式转换成另外一种格式。然而，大部份的Spring用户并不需要直接以编程的方式处理这些类，而是采用XML的方式来进行定义，在内部这些定义将被转换成相应类的实例，并最终得到一个Spring IoC容器实例。

  ```
  构造器注入还是Setter注入?
  从构造器注入和Setter注入可以混合使用以来，有一个比较的做法，强制性依赖注入的使用构造器注入，可选的使用Setter注入。需要注意，在Setter方法上使用`@Require`注解，可是让这个属性成为必须注入的。

  Spring 团队一般主张构造函数注入，因为它能使一个执行应用程序组件作为不可变的对象，并确保所需的依赖关系都不是 `null`。此外在未完全初始化的状态下，此对象不会返回给客户代码（或被调用）。作为边注，由于大量的构造器参数可能使程序变得笨拙，暗示类可能有太多的责任和应重构为更好地关注地址适当分离。

  Setter注入只用应用于可选的依赖关系，在类中可以分配合理的默认值。否则，在任何使用地方使用依赖都要进行not-null检查。Setter注入还有一个好处是可以通过Setter方法实现重新注入。`JMX MBean`就是一个很好的例子

  对于注入类型的选择并没硬性的规定。只要能适合你的应用，无论使用何种类型的DI都可以。对于那些没有源代码的第三方类，或者没有提供setter方法的遗留代码，我们则别无选择－－构造器注入将是你唯一的选择。
  ```

  **依赖解析过程**

  处理bean依赖关系通常按以下步骤进行：

  * 根据定义bean的配置元数据创建并初始化`ApplicationContext`实例，配置元数据可是XML、Java代码或者注解。
  * 每个bean的依赖将以属性、构造器参数、或静态工厂方法参数的形式出现。当这些bean被实际创建时，这些依赖也将会提供给该bean。
  * 每个属性或构造器参数既可以是一个实际的值，也可以是对该容器中另一个bean的引用。
  * 每个指定的属性或构造器参数值必须能够被转换成特定的格式或构造参数所需的类型。默认情况下，Spring会以String类型提供值转换成各种内置类型，比如`int`、`long`、`String`、`boolean`等。

  Spring会在容器被创建时验证容器中每个bean的配置，包括验证那些bean所引用的属性是否指向一个有效的bean（即被引用的bean也在容器中被定义）。然而，在bean被实际创建之前，bean的属性并不会被设置。对于那些singleton类型和被设置为提前实例化的bean（比如ApplicationContext中的singleton bean）而言，bean实例将与容器同时被创建。而另外一些bean则会在需要的时候被创建，伴随着bean被实际创建，作为该bean的依赖bean以及依赖bean的依赖bean（依此类推）也将被创建和分配。

  ```
  循环依赖

    在采用构造器注入的方式配置bean时，很有可能会产生循环依赖的情况。

    比如说，一个类A，需要通过构造器注入类B，而类B又需要通过构造器注入类A。如果为类A和B配置的bean被互相注入的话，那么Spring IoC容器将检测出循环引用，并抛出 `BeanCurrentlyInCreationException`异常。

    对于此问题，一个可能的解决方法就是修改源代码，将某些构造器注入改为setter注入。另一个解决方法就是完全放弃构造器注入，只使用setter注入。换句话说，除了极少数例外，大部分的循环依赖都是可以避免的，不过采用setter注入产生循环依赖的可能性也是存在的。

    与通常我们见到的非循环依赖的情况有所不同，在两个bean之间的循环依赖将导致一个bean在被完全初始化的时候被注入到另一个bean中（如同我们常说的先有蛋还是先有鸡的情况）。
  ```

  通常情况下，你可以信赖Spring，它会在容器加载时发现配置错误（比如对无效bean的引用以及循环依赖）。Spring会在bean创建时才去设置属性和依赖关系（只在需要时创建所依赖的其他对象）。这意味着即使Spring容器被正确加载，当获取一个bean实例时，如果在创建bean或者设置依赖时出现问题，仍然会抛出一个异常。因缺少或设置了一个无效属性而导致抛出一个异常的情况的确是存在的。因为一些配置问题而导致潜在的可见性被延迟，所以在默认情况下，`ApplicationContext`实现中的bean采用提前实例化的singleton模式。在实际需要之前创建这些bean将带来时间与内存的开销。而这样做的好处就是`ApplicationContext`被加载的时候可以尽早的发现一些配置的问题。不过用户也可以根据需要采用延迟实例化来替代默认的singleton模式。

  如果撇开循环依赖不谈，当协作bean被注入到依赖bean时，协作bean必须在依赖bean之前完全配置好。例如bean A对bean B存在依赖关系，那么Spring IoC容器在调用bean A的setter方法之前，bean B必须被完全配置，这里所谓完全配置的意思就是bean将被实例化（如果不是采用提前实例化的singleton模式），相关的依赖也将被设置好，而且所有相关的lifecycle方法（如IntializingBean的init方法以及callback方法）也将被调用。

  **一些注入的例子**

  首先是一个用XML格式定义的Setter DI例子。相关的XML配置如下：

  ```xml
  <bean id="exampleBean" class="examples.ExampleBean">
        <!-- setter injection using the nested ref element -->
        <property name="beanOne">
            <ref bean="anotherExampleBean"/>
        </property>

        <!-- setter injection using the neater ref attribute -->
        <property name="beanTwo" ref="yetAnotherBean"/>
        <property name="integerProperty" value="1"/>
    </bean>

    <bean id="anotherExampleBean" class="examples.AnotherBean"/>
    <bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
  ```
  ```java
  public class ExampleBean {

        private AnotherBean beanOne;
        private YetAnotherBean beanTwo;
        private int i;

        public void setBeanOne(AnotherBean beanOne) {
            this.beanOne = beanOne;
        }

        public void setBeanTwo(YetAnotherBean beanTwo) {
            this.beanTwo = beanTwo;
        }

        public void setIntegerProperty(int i) {
            this.i = i;
        }

    }
  ```

  正如你所看到的，bean类中的setter方法与xml文件中配置的属性是一一对应的。接着是构造器注入的例子：

  ```xml
  <bean id="exampleBean" class="examples.ExampleBean">
        <!-- constructor injection using the nested ref element -->
        <constructor-arg>
            <ref bean="anotherExampleBean"/>
        </constructor-arg>

        <!-- constructor injection using the neater ref attribute -->
        <constructor-arg ref="yetAnotherBean"/>

        <constructor-arg type="int" value="1"/>
    </bean>

    <bean id="anotherExampleBean" class="examples.AnotherBean"/>
    <bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
  ```

  ```java
  public class ExampleBean {

        private AnotherBean beanOne;
        private YetAnotherBean beanTwo;
        private int i;

        public ExampleBean(
            AnotherBean anotherBean, YetAnotherBean yetAnotherBean, int i) {
            this.beanOne = anotherBean;
            this.beanTwo = yetAnotherBean;
            this.i = i;
        }

    }
  ```

  如你所见，在xml bean定义中指定的构造器参数将被用来作为传递给类`ExampleBean`构造器的参数。

  现在来研究一个替代构造器的方法，采用`static`工厂方法返回对象实例：

  ```xml
  <bean id="exampleBean" class="examples.ExampleBean" factory-method="createInstance">
        <constructor-arg ref="anotherExampleBean"/>
        <constructor-arg ref="yetAnotherBean"/>
        <constructor-arg value="1"/>
    </bean>

    <bean id="anotherExampleBean" class="examples.AnotherBean"/>
    <bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
  ```

  ```java
  public class ExampleBean {

        // a private constructor
        private ExampleBean(...) {
            ...
        }

        // a static factory method; the arguments to this method can be
        // considered the dependencies of the bean that is returned,
        // regardless of how those arguments are actually used.
        public static ExampleBean createInstance (
            AnotherBean anotherBean, YetAnotherBean yetAnotherBean, int i) {

            ExampleBean eb = new ExampleBean (...);
            // some other operations...
            return eb;
        }

    }
  ```

  请注意，传给`static`工厂方法的参数由`constructor-arg`元素提供，这与使用构造器注入时完全一样。而且，重要的是，工厂方法所返回的实例的类型并不一定要与包含`static`工厂方法的类类型一致。尽管在此例子中它的确是这样。非静态的实例工厂方法与此相同（除了使用`factory-bean`属性替代`class`属性外），因而不在此细述。

#### 6.4.2 依赖配置详解

  正如前面章节所提到的，bean的属性及构造器参数既可以引用容器中的其他bean，也可以是内联（inline）bean。在spring的XML配置中使用`<property/>`和`<constructor-arg/>`元素定义。

  **直接变量(基本类型、字符串等)**

  `<property/>`元素中的`<value/>`元素通过人可以理解的字符串来指定属性或构造器参数的值。`Spring`的转换器将用于把字符串从java.lang.String类型转化为实际的属性或参数类型。

  ```xml
  <bean id="myDataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
      <!-- results in a setDriverClassName(String) call -->
      <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
      <property name="url" value="jdbc:mysql://localhost:3306/mydb"/>
      <property name="username" value="root"/>
      <property name="password" value="masterkaoli"/>
  </bean>
  ```

  接下来我们采用[p-namespace]()来演示上面的代码：

  ```xml
  <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:p="http://www.springframework.org/schema/p"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
      http://www.springframework.org/schema/beans/spring-beans.xsd">

      <bean id="myDataSource" class="org.apache.commons.dbcp.BasicDataSource"
          destroy-method="close"
          p:driverClassName="com.mysql.jdbc.Driver"
          p:url="jdbc:mysql://localhost:3306/mydb"
          p:username="root"
          p:password="masterkaoli"/>

  </beans>
  ```

  上面这种形式似乎更有效率一点；当然我们也可以按照下面这种方式配置一个`java.util.Properties`实例：

  ```xml
  <bean id="mappings"
      class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">

      <!-- typed as a java.util.Properties -->
      <property name="properties">
          <value>
              jdbc.driver.className=com.mysql.jdbc.Driver
              jdbc.url=jdbc:mysql://localhost:3306/mydb
          </value>
      </property>
  </bean>
  ```

  看到什么了吗？如果采用上面的配置，Spring容器将使用JavaBean `PropertyEditor`把`<value/>`元素中的文本转换为一个`java.util.Properties`实例。由于这种做法的简单，因此Spring团队在很多地方也会采用内嵌的`<value/>`元素来代替`value`属性。

  **idref元素**

  idref元素用来将容器内其它bean的id传给`<constructor-arg/>` 或 `<property/>`元素，同时提供错误验证功能。

  ```xml
  <bean id="theTargetBean" class="..."/>

  <bean id="theClientBean" class="...">
      <property name="targetName">
          <idref bean="theTargetBean" />
      </property>
  </bean>
  ```
  上述bean定义片段完全地等同于（在运行时）以下的片段：

  ```xml
  <bean id="theTargetBean" class="..." />

  <bean id="client" class="...">
      <property name="targetName" value="theTargetBean" />
  </bean>
  ```

  第一种形式比第二种更可取的主要原因是，使用`idref`标记允许容器在部署时 验证所被引用的bean是否存在。而第二种方式中，传给`client` bean的`targetName`属性值并没有被验证。任何的输入错误仅在`client` bean实际实例化时才会被发现（可能伴随着致命的错误）。如果`client` bean 是[prototype]()类型的bean，则此输入错误（及由此导致的异常）可能在容器部署很久以后才会被发现。

  >`idref`中的`local`属性已经从4.0xsd移除，如果你要从低版本升级到4.0的话，请使用`idref`中的`bean`替代。

  上面的例子中，与在`ProxyFactoryBean` bean定义中使用`<idref/>`元素指定[AOP interceptor]()的相同之处在于：如果使用`<idref/>`元素指定拦截器名字，可以避免因一时疏忽导致的拦截器ID拼写错误。

  **引用其它的bean（协作者）**

  在`<constructor-arg/>`或`<property/>`元素内部还可以使用`ref`元素。该元素用来将bean中指定属性的值设置为对容器中的另外一个bean的引用。如前所述，该引用bean将被作为依赖注入，而且在注入之前会被初始化（如果是singleton bean则已被容器初始化）。尽管都是对另外一个对象的引用，但是通过id/name指向另外一个对象却有三种不同的形式，不同的形式将决定如何处理作用域及验证。

  通过使用`<ref/>`标记指定`bean`属性的目标`bean`，通过该标签可以引用同一容器或父容器内的任何`bean`（无论是否在同一XML文件中）。XML 'bean'元素的值既可以是指定bean的`id`值也可以是其`name`值。

  ```xml
  <ref bean="someBean"/>
  ```

  通过使用`ref`的`parent`属性来引用当前容器的父容器中的bean。`parent`属性值既可以是目标bean的`id`值，也可以是`name`属性值。而且目标bean必须在当前容器的父容器中。使用parent属性的主要用途是为了用某个与父容器中的bean同名的代理来包装父容器中的一个bean(例如，子上下文中的一个bean定义覆盖了他的父bean)。

  ```xml
  <!-- in the parent context -->
    <bean id="accountService" class="com.foo.SimpleAccountService">
        <!-- insert dependencies as required as here -->
    </bean>
  ```
  ```xml
  <!-- in the child (descendant) context -->
    <bean id="accountService" <!-- bean name is the same as the parent bean -->
        class="org.springframework.aop.framework.ProxyFactoryBean">
        <property name="target">
            <ref parent="accountService"/> <!-- notice how we refer to the parent bean -->
        </property>
        <!-- insert other configuration and dependencies as required here -->
    </bean>
  ```

  > 使用`ref`的`local`属性指定目标`bean`，从4.0开始不再支持，如果使用4.0的版本，只需要把这种方式现在更改为`ref bean`而不再是`ref local`（4.0开始）

  **内部bean**

  所谓的内部bean（inner bean）是指在一个bean的`<property/>`或 `<constructor-arg/>`元素中使用`<bean/>`元素定义的bean。内部bean定义不需要有`id`或`name`属性，即使指定`id `或 `name`属性值也将会被容器忽略。

  ```xml
  <bean id="outer" class="...">
        <!-- instead of using a reference to a target bean, simply define the target bean inline -->
        <property name="target">
            <bean class="com.example.Person"> <!-- this is the inner bean -->
                <property name="name" value="Fiona Apple"/>
                <property name="age" value="25"/>
            </bean>
        </property>
    </bean>
  ```

  注意：内部bean中的`scope`标记及`id`或`name`属性将被忽略。内部bean总是匿名的且它们总是prototype模式的。同时将内部bean注入到包含该内部bean之外的bean是不可能的。

  **集合**

  通过`<list/>`、`<set/>`、`<map/>`及`<props/>`元素可以定义和设置与Java `Collection`类型对应`List`、`Set`、`Map`及`Properties`的值。

  ```xml
  <bean id="moreComplexObject" class="example.ComplexObject">
        <!-- results in a setAdminEmails(java.util.Properties) call -->
        <property name="adminEmails">
            <props>
                <prop key="administrator">administrator@example.org</prop>
                <prop key="support">support@example.org</prop>
                <prop key="development">development@example.org</prop>
            </props>
        </property>
        <!-- results in a setSomeList(java.util.List) call -->
        <property name="someList">
            <list>
                <value>a list element followed by a reference</value>
                <ref bean="myDataSource" />
            </list>
        </property>
        <!-- results in a setSomeMap(java.util.Map) call -->
        <property name="someMap">
            <map>
                <entry key="an entry" value="just some string"/>
                <entry key ="a ref" value-ref="myDataSource"/>
            </map>
        </property>
        <!-- results in a setSomeSet(java.util.Set) call -->
        <property name="someSet">
            <set>
                <value>just some string</value>
                <ref bean="myDataSource" />
            </set>
        </property>
    </bean>
  ```
  注意：map的key或value值，或set的value值还可以是以下元素：

  ```
  bean | ref | idref | list | set | map | props | value | null
  ```

  **集合的合并**

  Spring IoC容器将支持集合的合并。这样我们可以定义parent-style和child-style的`<list/>`、`<map/>`、`<set/>`或`<props/>`元素，子集合的值从其父集合继承和覆盖而来；也就是说，父子集合元素合并后的值就是子集合中的最终结果，而且子集合中的元素值将覆盖父集全中对应的值。

  请注意，关于合并的这部分利用了parent-child bean机制。此内容将在后面介绍。

  下面的例子展示了集合合并特性：

  ```xml
  <beans>
      <bean id="parent" abstract="true" class="example.ComplexObject">
          <property name="adminEmails">
              <props>
                  <prop key="administrator">administrator@example.com</prop>
                  <prop key="support">support@example.com</prop>
              </props>
          </property>
      </bean>
      <bean id="child" parent="parent">
          <property name="adminEmails">
              <!-- the merge is specified on the child collection definition -->
              <props merge="true">
                  <prop key="sales">sales@example.com</prop>
                  <prop key="support">support@example.co.uk</prop>
              </props>
          </property>
      </bean>
  <beans>
  ```
  在上面的例子中，`child` bean的`adminEmails`属性的元素上使用了`merge=true`属性。当`child` bean被容器实际解析及实例化时，其`adminEmails`将与父集合的`adminEmails`属性进行合并。

  ```properties
  administrator=administrator@example.com
    sales=sales@example.com
    support=support@example.co.uk
  ```
  注意到这里子bean的`Properties`集合将从父`<props/>`继承所有属性元素。同时子bean的`support`值将覆盖父集合的相应值。

  对于`<list/>`、`<map/>`及`<set/>`集合类型的合并处理都基本类似，在某个方面`<list/>`元素比较特殊，这涉及到`List`集合本身的语义学，就拿维护一个有序集合中的值来说，父bean的列表内容将排在子bean列表内容的前面。对于`Map`、`Set`及`Properties`集合类型没有顺序的概念，因此作为相关的`Map`、`Set`及`Properties`实现基础的集合类型在容器内部没有排序的语义。

  **集合合并的限制**

  你不能合并不同类型的集合(如Map跟List)，如果你尝试这么做的话，将会抛出异常。

  **强类型集合**

  泛型在Java5中被引入，这样你就可以使用强类型集合。比如，声明一个只能包含`String`类型元素的`Collection`。假若使用Spring来给bean注入强类型的`Collection`，那就可以利用Spring的类型转换能，当向强类型`Collection`中添加元素前，这些元素将被转换。

  ```java
  public class Foo {

        private Map<String, Float> accounts;

        public void setAccounts(Map<String, Float> accounts) {
            this.accounts = accounts;
        }
    }
  ```
  ```xml
  <beans>
        <bean id="foo" class="x.y.Foo">
            <property name="accounts">
                <map>
                    <entry key="one" value="9.99"/>
                    <entry key="two" value="2.75"/>
                    <entry key="six" value="3.99"/>
                </map>
            </property>
        </bean>
    </beans>
  ```
  在`foo` bean的`accounts`属性被注入之前，通过反射，利用强类型`Map<String, Float>`的泛型信息，Spring的底层类型转换机制将会把各种`value`元素值转换为`Float`类型，因此字符串`9.99`、`2.75`及`3.99`就会被转换为实际的`Float`类型。

  **Null与空字符串**

  properties中的空参数，Spring将会当做空字符串，如下：

  ```xml
  <bean class="ExampleBean">
        <property name="email" value=""/>
    </bean>
  ```
  以上代码等同于如下的Java代码:

  ```java
  exampleBean.setEmail("")
  ```
  `<null/>`也会作为`null`处理：

  ```xml
  <bean class="ExampleBean">
        <property name="email">
            <null/>
        </property>
    </bean>
  ```
  同：

  ```java
  exampleBean.setEmail(null)
  ```

  **简洁的XML配置-p命名空间**

  我们现在可以使用P命名空间来简化我们的配置：

  ```xml
  <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:p="http://www.springframework.org/schema/p"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd">

        <bean name="classic" class="com.example.ExampleBean">
            <property name="email" value="foo@bar.com"/>
        </bean>

        <bean name="p-namespace" class="com.example.ExampleBean"
            p:email="foo@bar.com"/>
    </beans>
  ```
  上面的代码中，我们用`p:email`替代了property `name="email"`，接下来演示其他情况：

  ```xml
  <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:p="http://www.springframework.org/schema/p"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd">

        <bean name="john-classic" class="com.example.Person">
            <property name="name" value="John Doe"/>
            <property name="spouse" ref="jane"/>
        </bean>

        <bean name="john-modern"
            class="com.example.Person"
            p:name="John Doe"
            p:spouse-ref="jane"/>

        <bean name="jane" class="com.example.Person">
            <property name="name" value="Jane Doe"/>
        </bean>
    </beans>
  ```
  在上面的代码中，我们使用了特殊的格式来声明引用关系`p:spouse-ref="jane"`等同于`<property name="spouse" ref="jane"/>`

  **简洁的XML配置-c命名空间**

  我可以用c命名空间来简化构造器的参数传递，过程类似于p命名空间：

  ```xml
  <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:c="http://www.springframework.org/schema/c"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd">

        <bean id="bar" class="x.y.Bar"/>
        <bean id="baz" class="x.y.Baz"/>

        <!-- traditional declaration -->
        <bean id="foo" class="x.y.Foo">
            <constructor-arg ref="bar"/>
            <constructor-arg ref="baz"/>
            <constructor-arg value="foo@bar.com"/>
        </bean>

        <!-- c-namespace declaration -->
        <bean id="foo" class="x.y.Foo" c:bar-ref="bar" c:baz-ref="baz" c:email="foo@bar.com"/>

    </beans>
  ```
  另外还可以通过指定下标来传递：

  ```xml
  <!-- c-namespace index declaration -->
    <bean id="foo" class="x.y.Foo" c:_0-ref="bar" c:_1-ref="baz"/>
  ```

  **组合属性名称**

  当设置bean的组合属性时，除了最后一个属性外，只要其他属性值不为null，组合或嵌套属性名是完全合法的。例如，下面bean的定义：

  ```xml
  <bean id="foo" class="foo.Bar">
        <property name="fred.bob.sammy" value="123" />
    </bean>
  ```
  `foo` bean有个`fred`属性，此属性有个`bob`属性，而`bob`属性又有个`sammy`属性，最后把`sammy`属性设置为`123`。为了让此定义能工作，`foo`的`fred`属性及`fred`的`bob`属性在bean被构造后都必须非空，否则将抛出`NullPointerException`异常。