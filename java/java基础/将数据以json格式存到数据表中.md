#### 有一个需求，比如说要在别的表中取很多字段，如名称，国家，公司，邮箱等等，但是我的表中只有一个CLOB类型的字段`Info`来存取这些取到的信息。拼接字符串很明显不是一个明智的方案，最好的方法是用josn保存。
#### 时间有限直接写一下思路：
数据存：
```java
JSONObject json = new JSONObject ();
json.put("name",xxx.getName());
json.put("countryName",xxx.getCountryName());
...
xxxxDTO.setInfo(json.toJSONString());
```
数据取：
```java
(String)JSON.parseObject(xxx.getInfo()).get("name");
```
#### 这种方法有一点蠢的地方是我的json存很多值就要写很多put，其实可以把需要存的值写在DTO里面，方便修改和增加如：
数据存：
```java
xxxxDTO.setName = xxx.getName();
xxxxDTO.setCountryName = xxx.getCountryName();
JSON.toJSONString(xxxxDTO);
```
