Spring架构
- spring-context
- spring-jdbc
- spring-mvc

[Spring官方文档](https://docs.spring.io/spring-framework/docs/5.2.1.RELEASE/spring-framework-reference/)

1. 请求转发和重定向
   - 请求转发，forward，将请求转发到一个页面，地址栏URL不变。
   - 重定向，Redirect，重定向到另一个页面，地址栏url会变。
   - 
2. MVC三层
 - spring webMVC
 - spring context
 - spring jdbc  
3. mybatis

spring web MVC spring context mybatis SSM 
Spring Boot Spring Cloud

## homework
1. SpEL（Spring Expression Language） ,Spring表达式语言，使用$
 $中可以写表达式，#中不能写表达式，会将表达式原样输出。
2. 参数自动注入的modelAndView是不是在ioc对象，是不是单例的，多线程下什么表现？
3. spring context，spring mvc 核心组件流程和细节解析。
4. Spring IOC,Interceptor,Filter,
5. spring IOC、spring MVC 、spring jdbc、spring AOP、spring tx常用注解
6. 架构->核心组件详解->总结&最佳实践，总分总
7. 请求转发和重定向等Servlet常用知识点
8. mybatis使用哪种动态代理机制来实现Mapper接口的增强的。 $中可以写表达式，#中不能写表达式，会将表达式原样输出
9. 一般使用#。
10. JDK动态代理和Cglib动态代理的区别和特性。
11. https://baomidou.com/pages/24112f/#%E7%89%B9%E6%80%A
12. mybatis插件，实现mybatis-plus中的全部功能，还有逻辑删除。这两个功能。
13. springboot统一解决了开发SSM项目的配置复杂和依赖混乱的问题。
    怎么解决的呢？只默认核心流程，其他的组件通过配置加入，推荐了最佳版本组合。
    其实在很多地方面临这种问题，业务复杂，每个人的需求都一样。
14. spring boot 的yml文件是怎么解析出来注入到对象的属性中的。我猜测是先将yml专为json再通过层级关系获取。





