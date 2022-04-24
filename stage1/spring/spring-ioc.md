[Spring Framework](https://spring.io/projects/spring-framework)


spring config
spring dataSources
spring annatotion
spring webMVC


1. 常用注解
<image src="./image/spring-bean-annotation.png">

|注解|说明|
|---|---|
|@Configuration|用于指定当前类是一个配置类，当创建容器时会从该类上加载配置|
|@ComponentScan|用于指定Spring在初始化容器时要扫描的包|
|@Bean|用在方法上，标注将该方法的返回值存储到spring容器中。|
|@PropertySource|用于加载property文件中的配置|
|@Import|用于导入其他配置类|
1. 核心容器源码解析
2. 架构->核心类->核心类组成的架构
 
