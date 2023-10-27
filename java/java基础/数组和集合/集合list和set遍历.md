### list集合常用三种遍历方式。
#### 首先创建一个list集合并添加数据
```java
 List<String> list = new ArrayList<String>();
 list.add("aa");
 list.add("bb");
 list.add("cc");
```
#### 1.for循环遍历，速度快  
```java
for(int i=0 ;i<list.size();i++){
System.out.println(list.get(i));
}
```
#### 2.foreach增强型for循环遍历，写起来简单  
```java
for(String str :list) {
    System.out.println(str);
}
```
#### 3.迭代器迭代，是集合类的通用遍历方式, 从很早的版本就有
```java
Iterator it =list.iterator();
while(it.hasNext()){
    System.out.println(it.next());
}
```
#### 4.lamda表达式方法。这是jdk1.8新特性的方法
```java
list.forEach(lists -> {
    System.out.println(lists);
});
```

### set集合有以上2、3、4常用的遍历方式，至于为什么没有1普通for循环遍历方式，原因是Set是无序的，不能这样实现遍历。

### 将实体类的集合中的某个字段抽成新的集合：
```java
List<Long> ids = xxDTOList.stream.map(xxDTO::getId).collect(Collectors.toList());
```


### 将实体类的集合中的某个字段抽成新的去重集合：
```java
List<Long> ids = xxDTOList.stream.map(xxDTO::getId).distinct().collect(Collectors.toList());
```

### 根据条件过滤
```java
//要找出的年龄大小
List<Integer> ageList = ...
//需要被过滤的对象
List<StudentDTO> studentDTOList = ...
//根据第一个条件过滤
List<StudentDTO> result = studentDTOList.stream().filter((StudentDTO s) -> ageList.contains(s.getAge())).collect(Collectors.toList());
```

### 排序，实际开发中发现树状结构也可以根据其中一个属性排序，如：
```java
@Data
public class Parent {
    private String id;
    private List<Children> children;
}
@Data
public class Children {
    private String name;
    private Integer age;
}
List<Parent> list = xxxxx;
list = list.stream().sorted(Comparator.comparing(v -> v.getChildren().get(0).getAge())).collect(Collectors.toList());
```

### 判断自定义对象类型的集合中对象的值
```java
if(studentList.stream().filter(s -> s.getStudentName().equals("王聪")).findAny().isPresent()){

}
// 然后用了以上代码idea编辑报黄，提示.filter后面的可以用anyMatch代替，于是查了一下怎么用改为如下语句：
if(studentList.stream().anyMatch(s -> s.getStudentName().equals("王聪"))){

}
```

### list根据主键转换成map
```java
List<TaskTagDictionary> taskTagList = this.listByIds(tagList);
if(CollectionUtils.isEmpty(taskTagList)) {
    return Collections.emptyMap();
}
return taskTagList.stream().collect(Collectors.toMap(TaskTagDictionary::getId, e -> e));
```

### list根据某个属性分组
```java
//根据学生姓名进行分类
public Map<String, List<Student>> groupList(List<Student> students) {
	Map<String, List<Student>> map = students.stream().collect(Collectors.groupingBy(Student::getName));
	return map;
}
//假设需要简单排序（自然排序）
TreeMap<String, List<Student>> sortedMap = students.stream().collect(Collectors.groupingBy(Student::getName, TreeMap::new, Collectors.toList()));

//根据学生姓名进行分类并获取具体的字段(如根据学生姓名获取所有成绩)
Map<String, List<String>> map = students.stream().collect(Collectors.groupingBy(Student::getName, Collectors.mapping(Student::getPrice, Collectors.toList())));
//加入需要简单排序（自然排序）
TreeMap<String, List<String>> sortedMap = students.stream().collect(Collectors.groupingBy(Student::getName, TreeMap::new, Collectors.mapping(Student::getPrice, Collectors.toList())));


```

