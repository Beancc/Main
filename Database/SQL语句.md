## 基础数据库操作语言  
### 常用语句  
* 新建数据库 `Create  database  xx;`  
* 查看数据库 `Show databases;`  
* 使用表 Use `xx;  `  
* 查看表目录 `show  tables;`  
* 查看表结构 `Descstudent;`  

* 增  `Insert into  表名 values(‘’,’’,’’,’’,’’,)`  
* 删  `Delete  from  表名 where 条件`  
* 改  `Update  student  set  +修改的新值  where  条件`  
* 查  `select * from 表名 where 条件`  
* 删（表） `Drop  table  表名` 
### 条件语句
* 新建表（设置不为空自动增长空表默认填充） `Create  table 表名(id int not null primary key auto_increament,列名 char(32),列名 char(20),列名 char(32),列名 varchar(32),列名 varchar(32) default “缺省值”);`  
* 选择性插入 `Insert 表名(id,name,adress) values(‘’,’’,’’);`  
* 更改表的属性  
 >Alter  table  student  add+列名+列名属性;（after列）；//新增列  
 >Alter  table  student  drop + 列名//删除列  
 >Alter  table  student  change+旧列名+新列名+新列名属性；//更改列名  
 >Alter  table  student  modify+列名+新列名属性；//更改列属姓  
 >Alter  table  student  rename  to+新表名；  //更改表名





