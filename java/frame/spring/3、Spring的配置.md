### scheme

* ##### Bean标签的相关配置
  * ##### <bean>标签的id和name的配置
  > id:使用了唯一约束，不能使用特殊字符  
  > name:未使用唯一约束，可以使用特殊字符  
  > class:类的全路径  
* ##### 声明周期的配置
  * ##### init-method和destroy-method
  > init-method:Bean被初始化时执行的方法  
  > destroy-method:Bean被销毁时执行的方法(Bean是单例创建，工厂关闭时)
* ##### 作用范围的配置(重点)  
  * ##### scope：bean的作用范围
  > singleton：默认，Spring用单例模式创建对象  
  > prototype：多例模式(在和struts2整合时使用，因为struts2是多例，spring帮其管理action)  
  > request：应用Web，Spring创建类并将类存入到request范围中  
  > session：应用Web，Spring创建类并将类存入到session范围中  
  > globalsession：应用Web，必须在porlet环境下使用，如果没有这个环境则等同于session
