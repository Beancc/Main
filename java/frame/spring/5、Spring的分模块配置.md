### 分模块配置时的引用  
* ##### 加载配置文件时，加载多个 
  ```
  public void demo1(){
    ApplicetionContext applicationCpntext 
    = new ClassPathXmlApplicationContext("applicationContext.xml","applicationContext2.xml");
    ·
    ·
  }
  ```
* ##### 在一个配置文件中引入多个配置文件(如在applicationContext.xml里面引入如下：)
  ```
  <import resource = "applicationContext2.xml" />
  ```
