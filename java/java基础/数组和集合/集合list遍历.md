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
