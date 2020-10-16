#### 简单记录一下用jdk8实现筛选实体类的一种方法

```java
public class Apple {
    private String color;
    private Integer weight;

    private final static String GREEN = "green";

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public Integer getWeight() {
        return weight;
    }

    public void setWeight(Integer weight) {
        this.weight = weight;
    }

    public static boolean isGreenApple(Apple apple){
        return GREEN.equals(apple.getColor());
    }
    public static boolean isHeavyApple(Apple apple){
        return apple.getWeight() > 100;
    }

    @Override
    public String toString() {
        return "Apple{" +
                "color='" + color + '\'' +
                ", weight=" + weight +
                '}';
    }
}

```

#### 测试
```java
public class TTTTT {
    private final static String GREEN = "green";
    public static void main(String[] args) {
        List<Apple> list = new ArrayList();
        Apple apple = new Apple();

        apple.setColor("green");
        apple.setWeight(200);
        list.add(apple);

        Apple apple1 = new Apple();
        apple1.setColor("red");
        apple1.setWeight(100);
        list.add(apple1);

        list.forEach(e->{
            System.out.println(e.toString());
        });
        filter(list,Apple::isGreenApple);

    }

    public interface Condition<T>{
        boolean test(T t);
    }
    static List<Apple> filter(List<Apple> inventory, Condition<Apple> p){
        List<Apple> result = new ArrayList<>();
        for(Apple apple : inventory){
            if(p.test(apple)){
                result.add(apple);
            }
        }
        System.out.println(result.toString());
        return result;
    }
}
```
