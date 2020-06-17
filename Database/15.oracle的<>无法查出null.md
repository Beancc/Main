#### 在Oracle数据库中，使用`<>` `!=` `^=`都能表示`不等于`，但是需要注意的是，这样查出来的数据，不包含null，比如有一个包含“是”和“否”以及null的字段，用以下语句：
```
select * from table where is_settle <> '是'
```
查询出来的结果全部是否，却没有null，而正确的查询除了“是”以外的所有结果应该用如下语句
```
select * from table where (is_settle <> '是' or is_settle is null)
```

##### 当然了还有一点，只有`<>`是SQL标准写法，其他的两种在除oracle上不适用，所以在程序里保持用`<>`代表不等于是一个良好的习惯。
