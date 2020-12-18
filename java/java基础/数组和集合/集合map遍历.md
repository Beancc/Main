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
> 这种方法基本上没啥用，因为在实际环境中不会按序列添加map
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
4. ##### 利用entry的foreach增强型for循环遍历
```
for(Map.Entry<Integer,String> entry:map.entrySet()){
    System.out.println(entry);
}
```
* ##### 注意比较第2种方法和第4种方法。其中第2种方法利用的是将所有的keys先存入set集合，然后遍历set集合获得key，再通过`value=get(key)`的方法获取，而4中的方法利用的entrySet是将键值对存入到set集合，这时候打印输出entry也可以很明显看出来输出的是键值对。
