* ##### spring的属性注入，给Bean中的属性设置值（Spring当中属性注入支持前两种）  
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
  * ##### set方法方式
  ```
  public class User{
    private String name;
    public void setName(String name){
      this.name = name;
    }
  }
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
