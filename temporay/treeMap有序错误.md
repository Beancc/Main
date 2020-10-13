### 这个代码我尝试将Map转换为list进行排序然后再转换回Map，但是转回来用的有序map也没有按插入顺序进行排序，先记录一下代码，有空再看一下。

```java
public class TTTTT {
    public static void main(String[] args) {
        Map<String,Integer> map = new HashMap<>();
        map.put("1",1);
        map.put("1",(Integer)map.get("1")+1);
        System.out.println(map.get("1"));
        Map map1 = new HashMap();
        map1.put("2",1);
        map.putAll(map1);
        for(String s : map.keySet()){
            System.out.println(s + map.get(s));
        }
        map.entrySet();
        System.out.println(map.entrySet());

        List<Map.Entry<String, Integer>> infoIds = new ArrayList<Map.Entry<String, Integer>>(map.entrySet());
        System.out.println(infoIds.toString());

        for (int i = 0; i < infoIds.size(); i++) {
            String id = infoIds.get(i).toString();
            System.out.println(id);
        }
        // 排序
        Collections.sort(infoIds, new Comparator<Map.Entry<String, Integer>>() {
            public int compare(Map.Entry<String, Integer> o1,
                               Map.Entry<String, Integer> o2) {
                return ( o1.getValue()-o2.getValue());
            }
        });
        System.out.println("--------------排序后--------------");
        Map map2 = new TreeMap();
        for (int i = 0; i < infoIds.size(); i++) {
            Map.Entry<String,Integer> ent=infoIds.get(i);

            map2.put(ent.getKey(),ent.getValue());
            System.out.println(ent.getKey()+"="+ent.getValue());
        }
        System.out.println(map2.entrySet());
    }
}
```
