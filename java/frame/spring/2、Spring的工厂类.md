### BeanFactory
* ##### 老版本的工厂类，现在很少有用
* ##### 在调用getBean的时候，才会生成类的实例

### ApplicationContext
* ##### 其实是继承了BeanFactory接口
* ##### 加载配置文件的时候，就会将Spring管理的类都实例化  
* ##### 实现类：
> ClassPathXmlApplicationContext 加载类路径下的配置文件  
> FIleSystemXmlApplicationContext 加载文件系统下的配置文件
