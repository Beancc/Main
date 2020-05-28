
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
  > @Autowired ： 设置对象类型的属性的值，但是按照类型完成属性注入。  
  > @Qualifier : 必须让@ Autowired注解和@ Qualifier一起使用完成按照名称属性注入。
  > @Resource(name = "") : 对象属性的注入，按照名称完成属性注入（非spring包的，是spring规范的），替换上面两个。
* ##### Bean的其他属性的注解  
  > @PostStruct : 初始化方法，相当于配置了init-method
  > @PreDestroy : 销毁方法，相当于配置了destroy-method
  > @Scope : 作用范围(默认singleton，还有prototype，request，session，globalsession)
* ### XML开发和注解开发的区别
* ##### 适用场景
  > XML:适用任何场景，好处是结构清晰，维护方便。
  > 注解：有些地方用不了，比如说类不是自己提供的，好处是开发方便速度快。
  > XML和注解整合开发:XML管理Bean，注解完成属性注入。
