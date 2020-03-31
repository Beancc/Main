### Spring的概述  
* ##### Spring是SE、EE开发的一站式框架  
  > Web层：SpringMVC  
  > Service层：Spring的Bean管理，声明式事务  
  > Dao层：ORM模块，jdbc模板
* ##### Spring优点
  > 方便解耦合：IOC，不用修改源代码就可以切换底层的实现  
  > AOP的开发：对程序进行扩展  
  > 轻量级框架  
  > 方便与其他框架整合  
* ##### Spring的IOC入门
  > 下载Spring的开发包  
  > 引入jar包  
  > 创建接口和实现类  
  > 将接口和实现类交给Spring管理  
  > 编写测试类  
  > IOC和DI  
* ##### Spring的工厂类  
  > BeanFactory：老版本  
  > ApplicationContext：新版本  
  >> ClassPathXmlApplicationContext  
  >> FileSystemXmlApplicationContext  
* ##### Spring的配置  
  > id和name的配置  
  > 声明周期的配置  
  > bean的作用范围的配置  
  >> singleton:默认  
  >> prototype:多例的  
* ##### Spring的Bean管理(XML)  
  > Spring的Bean的实例化方式  
  > Spring的属性注入  
  > P名称空间属性注入  
  > SpEL属性注入  
  > (复杂类型属性注入)  
* ##### Spring的整合Web项目
