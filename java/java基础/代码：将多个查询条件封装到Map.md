#### 今天有个excel下载耗时太久的优化需求。读代码，最耗时的部分是明明通过list取出了所有数据行，但是又对这个list进行了遍历，遍历的过程中又根据其中的字段进行数据库查询操作。这样的结果是这个不到1w行的list，里面有两个字段对数据库进行了查询，也就是循环下来对数据库查询操作了接近两万次。
#### 优化思路就是把这两个字段对数据库的操作拿到循环外面，一次性查询出所有的结果，将查询条件作为key，需要的结果作为value。
#### 优化前ServiceImpl代码如下：
```java
public list<XXXDTO> getInfomation(String id,String name,String xxx){
  List<XXXDTO> list = xxxDao.getXXX(id,name,xxx);
  for(XXXDTO item : list){
    ...
    Long num = xxDao.getxx(item.getyy(),item.getzz());
    ...
  }
}
```
#### 以上这个代码的特点就是对数据库的操作放在了for循环里面，导致非常耗时，那么根据优化思路我们就是把上面的item.getyy()和item.getzz()拼接作为key，num作为value，封装成map放到for循环外用来传值：
### ServiceImpl：
```java
public list<XXXDTO> getInfomation(String id,String name,String xxx){
  ...
  Map<String, Long> map = getTestMap(xxxDao.getTestNum(id));
  List<XXXDTO> list = xxxDao.getXXX(id,name,xxx);
  for(XXXDTO item : list){
    ...
    String key = item.getyy()+"-"+item.getzz()
    Long num = mep.get(key);
    ...
  }
  ...
}
public Map<String, Long> getInfomation(List<Map<String, Object>> itemMap){
  Map<String,Long> resultMap = new HashMap();
  for(Map<String,Long> map : itemMap){
    String countKey = null;
    Long countvalue = null;
    for(Map.Entry<String,Object> entry : map.entrySet()){
      if("COUNTKEY".equals(entry.getKey())) {
        countKey = (String) entry.getValue();
      }else if ("COUNTVALUE".equals(entry.getKey())) {
        countValue = ((BigDecimal)entry.getValue()).longValue();
      }
    }
    resultMap.put(countKey,countValue);
  }
  return resultMap;
}
```
### Dao
```java
  List<Map<String, Object>> getTestNum(@Param("id") String id);
```
### Mapper
```xml
<select id="getTestNum" resultMap="java.util.HashMap">
  select yy<![CDATA[||'-'||]]>zz as countKey，
  num as countValue
  from table 
  where id = #{userSapId,jdbcType=VARCHAR}
</select>
```
