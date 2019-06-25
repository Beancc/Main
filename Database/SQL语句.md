## 常用数据库操作语言  
### 基础语句  
* 新建数据库 `Create  database  xx;`  
* 查看数据库 `Show databases;`  
* 使用表 Use `xx;  `  
* 查看表目录 `show  tables;`  
* 查看表结构 `Descstudent;`  

* 增  `Insert into  表名 values(‘’,’’,’’,’’,’’,)`  
* 删  `Delete  from  表名 where 条件`  
* 改  `Update  student  set  +修改的新值  where  条件`  
* 查  `select * from 表名 where 条件` 
* 删（表） `Truncate  table  表名`//清空表内容
* 删（表） `Drop  table  表名`//删除表
### 条件语句
* 新建表（设置不为空自动增长空表默认填充） `Create  table 表名(id int not null primary key auto_increament,列名 char(32),列名 char(20),列名 char(32),列名 varchar(32),列名 varchar(32) default “缺省值”);`  
* 选择性插入 `Insert 表名(id,name,adress) values(‘’,’’,’’);`  
* 更改表的属性  
 1.`Alter  table  student  add+列名+列名属性;（after列）`//新增列  
 2.`Alter  table  student  drop + 列名`//删除列  
 3.`Alter  table  student  change+旧列名+新列名+新列名属性`//更改列名  
 4.`Alter  table  student  modify+列名+新列名属性`//更改列属姓  
 5.`Alter  table  student  rename  to+新表名`  //更改表名
* 备份表`Create  table  studentbak  as  select  *  from  student`
* 备份表插入`Insert  into 新表 select  *  from  旧表`
* 查找  
 1.`Select  *  from  student  where  name like"li%"`  //模糊查找名字li某  
 2.`Select  *  from  student  where  name like"li_i"`  //模糊查找名字li某i  
 3.`Select  *  from  student  where  birth>'1990-01-01'`  //生日大于某个区间  
 4.`Select  *  from  student  where  birth  between''and''`  //生日在某个区间内   
 5.`Select  *  from  student  where  birth  is  not""`  //查询不是  
 6.`Select  *  from  student  where  birth  !=""`  //查询不等于  
 7.`Select  *  from  student  where  class=in（5,6,7,8,）`//班级是5,6,7,8班


