#### 这里记录一下String的各种使用方法

#### 1.如果将多个取值用符号拼接在一起，常规做法是循环拼完了删掉最后一个拼接符，然而JDK1.8可以用StringJoiner直接拼接的方式：
```java
List<String> strList = Arrays.asList("a", "b", "c");
  StringJoiner subStr = new StringJoiner(",");
  for (String strData : strList){
    subStr.add(strData);
  }
```
