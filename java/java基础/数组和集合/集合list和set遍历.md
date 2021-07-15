### list集合常用三种遍历方式。
#### 首先创建一个list集合并添加数据
```
 List<String> list = new ArrayList<String>();
 list.add("aa");
 list.add("bb");
 list.add("cc");
```
#### 1.for循环遍历，速度快  
```
for(int i=0 ;i<list.size();i++){
System.out.println(list.get(i));
}
```
#### 2.foreach增强型for循环遍历，写起来简单  
```
for(String str :list) {
    System.out.println(str);
}
```
#### 3.迭代器迭代，是集合类的通用遍历方式, 从很早的版本就有
```
Iterator it =list.iterator();
while(it.hasNext()){
    System.out.println(it.next());
}
```
#### 4.lamda表达式方法。这是jdk1.8新特性的方法
```
list.forEach(lists -> {
    System.out.println(lists);
});
```

### set集合有以上2、3、4常用的遍历方式，至于为什么没有1普通for循环遍历方式，原因是Set是无序的，不能这样实现遍历。

### 将实体类的集合中的某个字段抽成新的集合：
```
List<Long> ids = xxDTOList.stream.map(xxDTO::getId).collect(Collectors.toList());
```

### 根据条件过滤
```
//要找出的年龄大小
List<Integer> ageList = ...
//需要被过滤的对象
List<StudentDTO> studentDTOList = ...
//根据第一个条件过滤
List<StudentDTO> result = studentDTOList.stream().filter((StudentDTO s) -> ageList.contains(s.getAge())).collect(Collectors.toList());
```


