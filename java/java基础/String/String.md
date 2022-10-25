#### 这里记录一下String的各种使用方法

#### 1.如果将多个取值用符号拼接在一起，常规做法是循环拼完了删掉最后一个拼接符，然而JDK1.8可以用StringJoiner直接拼接的方式：
```java
List<String> strList = Arrays.asList("a", "b", "c");
  StringJoiner subStr = new StringJoiner(",");
  for (String strData : strList){
    subStr.add(strData);
  }
```
以下两种写法，1是使用commons-lang库写法，2是lambda表达式的写法，都更加简单
```java
StringUtils.join(list.toArray(), ",")

list.stream().collect(Collectors.joining(","))

```
今天发现了一个更简单的方法，看了一下源码发现就是上面的1.8的方法的一个封装，直接`String.join(",", list)`就齐活。


#### 2.如果对数字补齐位数，如1-20都补齐为两位，用String的format可以非常简单的实现。
```java
String.format("%02d", 8); //8为int型 
// 0代表前面要补的字符 
// 2代表字符串长度 
// d表示参数为整数类型
```
