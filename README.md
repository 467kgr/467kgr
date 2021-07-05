
-->
Spring事务管理的两种方式

    编程式事务管理。通常使用TransactionTemplete或PlatformTransactionManager，编程式事务管理回造成代码侵入，但更灵活。
    声明式事务管理。基于AOP实现，有XML配置和注解@Transactional两种方式。对一个类配置声明式事务，该类的所有public方法都会使用此事务，也就是说该方法的执行要嘛成功提交，要嘛回滚失败。
spring管理事务的两种方式: 

1、编程式事务，在代码中硬编码。(不推荐使用) 

2、声明式事务，在配置文件中配置（推荐使用） 

 

声明式事务又分为两种： 

a、基于XML的声明式事务 

b、基于注解的声明式事务

 
spring5种作用域：

1、singleton：单例模式，在整个Spring IoC容器中，使用singleton定义的Bean将只有一个实例

2、prototype：原型模式，每次通过容器的getBean方法获取prototype定义的Bean时，都将产生一个新的Bean实例

3、request：对于每次HTTP请求，使用request定义的Bean都将产生一个新实例，即每次HTTP请求将会产生不同的Bean实例。

4、session：对于每次HTTP Session，使用session定义的Bean豆浆产生一个新实例。

5、globalsession：每个全局的HTTP Session，使用session定义的Bean都将产生一个新实例。
SpringMvc执行流程

    用户发送请求至前端控制器DispatcherServlet
    DispatcherServlet收到请求调用HandlerMapping处理器映射器。
    处理器映射器根据请求url找到具体的handler处理器，返回给DispatcherServlet。
    DispatcherServlet通过HandlerAdapter处理器适配器调用handler处理器
    执行处理器(Controller是handler的一种)。
    Controller执行完成返回ModelAndView
    HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet
    DispatcherServlet将ModelAndView传给ViewReslover视图解析器
    ViewReslover解析后返回具体View
    DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）。
    DispatcherServlet响应用户

SpringMvc的参数绑定(从请求中接收参数)

    默认类型：在controller方法中可以有也可以没有,看自己需求随意添加。包括request，response，session，Model
    基本类型和String：double，float，integer，long，boolean，String
    pojo类型：页面上input框的name属性值必须要等于pojo的属性名称
    vo类型:页面上input框的name属性值必须要等于vo中的属性.属性.属性....
    自定义转换器converter：作用:由于springMvc无法将string自动转换成date所以需要自己手动编写类型转换器。需要编写一个类实现Converter接口在springMvc.xml中配置自定义转换器，在springMvc.xml中将自定义转换器配置到注解驱动上

Spring MVC Framework有这样一些特点:
l 它是基于组件技术的.全部的应用对象,无论控制器和视图,还是业务对象之类的都是java组件.并且和Spring提供的其他基础结构紧密集成.
2 不依赖于Servlet API(目标虽是如此,但是在实现的时候确实是依赖于Servlet的)
3 可以任意使用各种视图技术
4 支持各种请求资源的映射策略
5 易于扩展的
6 在web.xml中的配置

SpringMVC的工作流程:

1. 用户发送请求至前端控制器DispatcherServlet
2. DispatcherServlet收到请求调用HandlerMapping处理器映射器。
3. 处理器映射器根据请求url找到具体的处理器，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。
4. DispatcherServlet通过HandlerAdapter处理器适配器调用处理器
5. 执行处理器(Controller，也叫后端控制器)。
6. Controller执行完成返回ModelAndView
7. HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet
8. DispatcherServlet将ModelAndView传给ViewReslover视图解析器
9. ViewReslover解析后返回具体View
10. DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）。
11. DispatcherServlet响应用户


Mybatis的优点

       传统JDBC的数据库操作存在sql语句在代码中硬编码，不易维护扩展和创建连接对象，加载驱动等操作增加系统开销并降低开发效率这两个问题。Mybatis是对JDBC的封装，使得开发只需要专注sql本身，不需要花精力去处理驱动加载、创建连接对象等操作。

Mybatis工作原理

    Mybatis通过配置文件（sqlMapConfig核心配置文件和mapper文件）创建sqlSessionFactory对象。
    sqlSessionFactory创建sqlSession对象，sqlSession对象包含了执行sql语句的方法，但真正执行数据库操作的是MappedStatement和Executor执行器。
    Executor执行器。是mybatis底层实现的数据库操作接口，有基本执行器和缓存执行器两个实现类。
    MappedStatement也是mybatis的底层封装。Mapper.xml中一个sql对应一个mappedStatement对象，sql的id就是mappedStatement的id，sql输入参数：Executor通过Mapped Statement在执行sql前将输入的java对象映射至sql中，输入参数映射就是jdbc编程中对preparedStatement设置参数；输出参数：Executor通过Mapped Statement在执行sql后将输出结果映射至java对象中，输出结果映射过程相当于jdbc编程中对结果的解析处理过程。
对mybatis的理解:

1. 对mybatis配置
2. SqlMapConfig.xml，此文件作为mybatis的全局配置文件，配置了mybatis的运行环境等信息。
3. mapper.xml文件即sql映射文件，文件中配置了操作数据库的sql语句。此文件需要在SqlMapConfig.xml中加载。

4. 通过mybatis环境等配置信息构造SqlSessionFactory即会话工厂
5. 由会话工厂创建sqlSession即会话，操作数据库需要通过sqlSession进行。
6. mybatis底层自定义了Executor执行器接口操作数据库，Executor接口有两个实现，一个是基本执行器、一个是缓存执行器。
7. Mapped Statement也是mybatis一个底层封装对象，它包装了mybatis配置信息及sql映射信息等。mapper.xml文件中一个sql对应一个Mapped Statement对象，sql的id即是Mapped statement的id。
8. Mapped Statement对sql执行输入参数进行定义，包括HashMap、基本类型、pojo，Executor通过Mapped Statement在执行sql前将输入的java对象映射至sql中，输入参数映射就是jdbc编程中对preparedStatement设置参数。
9. Mapped Statement对sql执行输出结果进行定义，包括HashMap、基本类型、pojo，Executor通过Mapped Statement在执行sql后将输出结果映射至java对象中，输出结果映射过程相当于jdbc编程中对结果的解析处理过程。
MyBatis编程步骤:
1. 创建SqlSessionFactory
2. 通过SqlSessionFactory创建SqlSession
3. 通过sqlsession执行数据库操作
4. 调用session.commit()提交事务
5. 调用session.close()关闭会话
MyBatis的一级缓存和二级缓存:
Mybatis首先去缓存中查询结果集，如果没有则查询数据库，如果有则从缓存取出返回结果集就不走数据库。Mybatis内部存储缓存使用一个HashMap，key为hashCode+sqlId+Sql语句。value为从查询出来映射生成的java对象 Mybatis的二级缓存即查询缓存，它的作用域是一个mapper的namespace，即在同一个namespace中查询sql可以从缓存中获取数据。二级缓存是可以跨SqlSession的。
JDBC编程有哪些不足之处，MyBatis是如何解决这些问题的:
1.数据库链接创建、释放频繁造成系统资源浪费从而影响系统性能，如果使用数据库链接池可解决此问题。
解决：在SqlMapConfig.xml中配置数据链接池，使用连接池管理数据库链接。
2.Sql语句写在代码中造成代码不易维护，实际应用sql变化的可能较大，sql变动需要改变java代码。
解决：将Sql语句配置在XXXXmapper.xml文件中与java代码分离。
3.向sql语句传参数麻烦，因为sql语句的where条件不一定，可能多也可能少，占位符需要和参数一一对应。
解决： Mybatis自动将java对象映射至sql语句。
4.对结果集解析麻烦，sql变化导致解析代码变化，且解析前需要遍历，如果能将数据库记录封装成pojo对象解析比较方便。
解决：Mybatis自动将sql执行结果映射至java对象。
SqlMapConfig.xml中配置的内容和顺序如下:
properties（属性）
settings（配置）
typeAliases（类型别名）
typeHandlers（类型处理器）
objectFactory（对象工厂）
plugins（插件）
environments（环境集合属性对象）
environment（环境子属性对象）
transactionManager（事务管理）
dataSource（数据源）
mappers（映射器）
使用MyBatis的mapper接口调用时有哪些要求:
1.  Mapper接口方法名和mapper.xml中定义的每个sql的id相同
2.  Mapper接口方法的输入参数类型和mapper.xml中定义的每个sql 的parameterType的类型相同
3.  Mapper接口方法的输出参数类型和mapper.xml中定义的每个sql的resultType的类型相同
4.  Mapper.xml文件中的namespace即是mapper接口的类路径。
