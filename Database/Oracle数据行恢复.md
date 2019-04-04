此文针对Oracle数据库数据表误删除行提供一种简单可行的恢复方法。首先声明一点，数据库被删除了，应立即停止一切操作。如果是物理文件被删除，那么无能为力，尽快找人做磁盘恢复。如果是语句删除，可以通过本方法进行日志恢复。  
具体步骤和SQL语言如下：  
--1.查询数据库时间，确定数据库时间和本地时间相同，避免接下来执行的语句恢复到错误的时间点
select  to_char(sysdate,'yyyy-mm-dd hh24:mi:ss') from dual;  

--2.查询删除数据时间点之前的数据，如果查询不到，那把时间再提前  
select * from 表名 as of timestamp to_timestamp('2019-04-04 10:30:11','yyyy-mm-dd hh24:mi:ss');  

--3.恢复数据，根据上一句可查询到数据的时间，对数据进行恢复  
flashback table 表名 to timestamp to_timestamp('2019-04-04 10:30:11','yyyy-mm-dd hh24:mi:ss');  

--4.如果运行3报错“ORA-08189：未启用行移动功能，不能闪回表”，这时先执行这句，再回去执行3就能解决  
alter table 表名 enable row movement;

