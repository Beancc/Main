### IOC：
* ##### 在Spring中IOC是一个很重要的设计原则，叫做控制反转。啥是控制反转呢，简单的说就是将实现类交给spring管理，将对象的创建权反转给spring。
* ##### 为什么要使用IOC呢，往下看：  
> ##### 最基本的实例化如：`UserDao userDao = new UserDao();`
> ##### 面向接口的实例化：`UserDao userDao = new UserDaoImpl();`
> ##### 使用Spring实例化(工厂+反射+配置applicationContext.xml)：
```
ApplicationContext applcationContext = new ClassPathXmlApplicationContext(applicationContext.xml);
UserDao userDao = (UserDao)applicationContext.getBean("UserDao");
```  
* ##### 可以知道，使用面向接口的好处就是可以多态，和我们最熟悉的`List list = new ArrayList();`一个道理。而使用Spring的好处是减少接口和实现类的耦合，这样可以在切换底层实现类的时候，避免修改源代码。

### DI：
* ##### DI的意思是依赖注入，DI的前提是必须要有IOC
