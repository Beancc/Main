因为需求部门提出了两个帆软报表的数据不同（数据报表是别人写的，分析报表是我写的），于是查看了一下SQL。后来发现原因所在是sql的日期区间查询条件他用的是to_date而我用的是to_char。
好了知道了问题所在我们分析一下，这两个的其他用法就不具体分析了，记住一个地方是to_date表示的日期区间不包含后一个日期，而to_char表示的日期区间包含后一个日期。什么意思呢，下面举个例子：
```
TO_CHAR (created_time,'yyyy-mm-dd') 
BETWEEN '2020-03-01'
AND '2020-03-04'
```
和
```
created_time 
BETWEEN to_date('2020-03-01','yyyy-MM-dd')
and to_date('2020-03-04','yyyy-MM-dd')
```
同样都是用的between and进行区间日期查询，但是to_char查询的结果是2020-03-01 00:00:00到2020-03-04 23:59:59之间的日期时间，而to_date查询的结果是2020-03-01 00:00:00到2020-03-03 00:00:00之间的日期时间。
结果显而易见，两个查询条件的结果是差了一天的数据。有的人可能考虑到了用的条件是>= <=，但是这个条件等同于between and。所以看以下两条语句就分别等价于上面的第一条和第二条了。
```
to_char(created_time,'YYYY-MM-DD') >= '2020-03-01' 
and to_char(created_time,'YYYY-MM-DD') <= '2020-03-04'
```
和
```
created_time >=to_date('2020-03-01','yyyy-MM-dd') 
and created_time <=to_date('2020-03-04','yyyy-MM-dd') 
```
