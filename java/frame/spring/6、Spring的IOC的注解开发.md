
### IOC注解开发  

* ##### 创建项目，引入jar包（4个基本包和2个日志包）。注意：在Spring4中，除了要引用Spring3中的开发包以外，还要引用aop的包。  
* ##### 引入Spring的核心配置文件，在src下新建applicationContext.xml  
  > ##### 引入约束：引入Context约束，在Spring包下面找（spring-framework-4.2.4.RELEASE/docs/spring-framework-reference/html/xsd-configuration.html）  
  > ##### 
* ##### 配置组件扫描
* ##### 类上注解
  > @Component组件：有三个衍生注解(功能类似)  
  > @Controller ：Web层  
  > @Service ：Service层  
  > @Repository ：Dao层
* ##### 属性注入的注解  
  > @Value ：普通属性   
  > @Autowired ： 对象属性  
  > @Resource(name = "") : 对象属性的注入，按照名称完成属性注入（非spring包的，是spring规范的）
