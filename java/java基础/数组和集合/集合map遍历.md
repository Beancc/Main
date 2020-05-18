### 说一下集合map的常用遍历方法
* #### 首先创建一个Map集合
```
Map<Integer,String> map = new HashMap<Integer,String>();
map.put(1,"a");
map.put(2,"b");
map.put(3,"c");
```
1. ##### 第一种还是最简单的利用for循环遍历：
```
for (int i = 1; i <= map.size(); i++) {
    System.out.println(map.get(i));
}
```
2. ##### 第二种是利用foreach增强型for循环遍历，但是因为是键值对存储，所以和list遍历稍有不同：
```
for(Integer i : map.keySet()){
    System.out.println("键是："+i+"，对应的值是："+map.get(i));
}
```
 > 注：如果只遍历Map的键的话可以用上面的2方法，但是如果只遍历Map的值的话可以用以下方法
 > 
 ``` 
  for(String s:map.values()){
     System.out.println(s);
  }
 ```
 3. ##### 迭代器迭代，这里也要注意一下和list集合在写法上的区别
 ```
Iterator it = map.entrySet().iterator();
while(it.hasNext()){
    System.out.println(it.next());
}
 ```
