#### 这里记录一下String的各种使用方法

#### 1.如果将多个取值用符号拼接在一起，常规做法是循环拼完了删掉最后一个拼接符，然而JDK1.8可以用StringJoiner直接拼接的方式：
```java
List<String> strList = Arrays.asList("a", "b", "c");
  StringJoiner subStr = new StringJoiner(",");
  for (String strData : strList){
    subStr.add(strData);
  }
```

#### 2.如果对数字补齐位数，如1-20都补齐为两位，用String的format可以非常简单的实现。
```java
String.format("%02d", 8); //8为int型 
// 0代表前面要补的字符 
// 2代表字符串长度 
// d表示参数为整数类型
```
