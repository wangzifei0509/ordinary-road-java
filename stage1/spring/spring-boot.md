Springboot 
## 开发环境
- Open JDK 1.8
- Spring Boot 2.5.12
- Maven 3.6.3
## 配置
application.yml   
- 属性上加注解@Value("${lists[0].name}")
- Environment对象，这个对象中封装了所有的配置信息。
- 封装成对象，交给spring容器管理，@ConfigurationProperties(prefix="xxx")
## 整合组件
- Junit
  1. 引入依赖 test依赖中已包含测试可能需要的包，Junit
   ```xml
   <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
    </dependency>
    ```
  2. 增加注解
  3. 自动注入spring容器管理的对象，完成测试。
  ``` java
  package com.wangxiamei;

  import com.wangxiamei.config.BookConfig;
  import org.junit.jupiter.api.Test;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.boot.test.context.SpringBootTest;

  @SpringBootTest
  public class BookTest {

      @Autowired
      private BookConfig bookConfig;

      @Test
      public void test(){
          System.out.println(bookConfig);
      }
  }
  ```
- mybatis
   1. 增加dependency
   2. 增加mapper扫描配置
- mybatis-plus
   1. 增加dependency
   2. 增加mapper扫描配置
   3. 增加分页插件配置
## 运维配置
1. 日志记录
   springboot默认使用的是logback日志组件，使用Slf4j作为统一日志接口。所以我们一般使用的Slf4j包下的类，可插拔配置不同的日志实现。

   日志级别主要使用的是四类：
   - debug 开发测试阶段开发人员调试使用
   - info 
   - warn 
   - error 代码层面的错误信息，能帮助开发人员在prod环境快速定位到为题。
  ``` yml
  # springboot相关的包日志级别调整为debug，一般在查看springboot相关的状态时要用到。
  debug: true 
  logging:
    level:
      root: info # 设置根目录下的日志级别为info（默认设置），如果设置为debug，显示日志肯定比debug=true多，因为这个设置是所有的包日志级别都为debug
      com.wangxiamei.controller: info #设置某个包下的日志级别为info
  # 通过分组设置日志级别（推荐使用这种）
  logging:
    group:
      a: com.wangxiamei.controller,com.wangxiamei.service
      b: com.iservice
    level:
      root: warn
      a: debug
      b: info
  ```  
2. 热部署
   热部署是重启，只是把开发人员自定义的资源重新加载，依赖的jar包没有动。
3. @ConfigurationProperties注解详解
  - 可以放在类上，也可以放在方法上，配置第三方类。
    ``` java
    @Component
    @Data
    @ConfigurationProperties(prefix = "book")
    public class BookConfig {
        private String name;
        private String num;
    }

    
    @SpringBootApplication
    public class Application {

        @Bean
        @ConfigurationProperties(prefix = "datasource")
        public DruidDataSource dataSource(){
            DruidDataSource druidDataSource = new DruidDataSource();
            return druidDataSource;

        }

        public static void main(String[] args) {

            ConfigurableApplicationContext context = SpringApplication.run(Application.class, args);
            //配置在类上，自动获取配置文件配置的对象
            BookConfig bean = context.getBean(BookConfig.class);
            System.out.println(bean);
            //配置在方法上，可以通过配置初始化第三方类
            DruidDataSource druidDataSource = context.getBean(DruidDataSource.class);
            System.out.println(druidDataSource.getDriverClassName());
        }
    }
    ```
    ``` yml
    book:
    name: java进阶
    num: 110
    ```
  - @EnableConfigurationProperties注解
    - 用在Application类
    - 声明哪些类需要使用配置属性的方式获取对象。比较直观的可以看到哪些对象在使用这种方式。
    - 声明中没有包含的类不能使用@ConfigurationProperties
    - 声明中包含的类可以使用@@ConfigurationProperties，但是不需要@Component
    ``` java
    @SpringBootApplication
    @EnableConfigurationProperties(BookConfig.class)
    public class Application {

    
        public static void main(String[] args) {

            ConfigurableApplicationContext context = SpringApplication.run(Application.class, args);
            BookConfig bean = context.getBean(BookConfig.class);
            System.out.println(bean);
        }
    }

    @Data
    @ConfigurationProperties(prefix = "book")
    public class BookConfig {
        private String name;
        private String num;

    }
    ``` 


4. bean字段校验
   javax.validation.api是实现了一套注入字段校验规范的统一接口，hibernate-validator是一套具体的实现。

   spring中有很多这种模式的实现，比如对日志的处理，Slf4J和logback，数据库连接的处理，JDBC和mysql-driver
--- 
5. @SpringBootTest字段详解
6. web层的单元测试
7. 测试域使用Hakiri+mybatis+H2组合进行测试
8. 整合Redis
   https://redis.io/docs/
  - RedisTemplate
  - RedisKeyValueTemplate
  - StringRedisTemplate
9. MogoDB
     适合操作高频、但是对持久性和可靠性要求不高的场景，比如直播间在线人数
10. 整合ES
    - 倒序索引
    - 文档型数据库
    - 分布式集群
    - 支持http API操作数据。
    - 全文检索
11. 缓存是数据临时存储介质
  1.spring-cache
    - simple
    - ehcache
    - redis
    - memcache
  2. Jetcache 也是一种缓存统一接口技术，可以用来替换spring cache，支持本地缓存和远程缓存两种层级的缓存。
12. 定时任务
13. 消息队列
    1.  JMS规范了java项目传递消息使用的标准API
    2.  AMQP规范了各语言间传递消息的格式，使用字节数组
    3.  MQTT用于物联网层面的消息遥测技术。
  - RocketMQ
  localhost: 9876

  - Kafka
14. 自己实现一个spring-boot-starter 
    基于IAM一套权限系统server端和starter
15. 

   

- MockMvc、Json-path
- Vue、Element-UI


