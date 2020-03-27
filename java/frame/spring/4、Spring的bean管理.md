### spring的属性注入
* ##### 给Bean中的属性设置值有三种方式（Spring当中属性注入支持前两种）  
  * ##### 构造方法方式  
  ```
  public class User{
    private String name;
    private String password;
    public User(String name,String password){
      this.name = name;
      this.password = password;
    }
  }
  ```
  ```
  <bean id="" class="">
    <construct-arg name="" value="">
  </bean>
  ```
  * ##### set方法方式
  ```
  public class User{
    private String name;
    public void setName(String name){
      this.name = name;
    }
  }
  ```
  ```
  <bean id="" class="">
    <property name="" value="">
  </bean>
  ```
  * ##### 接口注入
  ```
  public interface Injection{
    public void setName(String name){}
  }
  public class User implements Injection{
    private String name;
    public void setName(String name){
      this.name = name;
    }
  }
  ```
