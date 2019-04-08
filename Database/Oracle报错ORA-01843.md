# 关于执行有日期时间的SQL语句报错ORA-01843: not a valid month  
原因是timestamp类型不一致。timestamp的日期格式为YYYY-MM-DD HH24:MI:SS.FF6  
首先运行下面两句语句，再运行需要执行的语句就OK了。  
```
alter session set nls_date_language='AMERICAN';  
alter session set nls_timestamp_format = 'YYYY-MM-DD HH24:MI:SS.FF';  
```
查看会话参数：
```
select * from nls_session_parameters where parameter='NLS_DATE_LANGUAGE'
```
以上内容来自百度，具体不解释。
