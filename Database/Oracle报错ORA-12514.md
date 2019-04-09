# 针对使用Navicat连接Oracle数据库时，报错ORA-12514: TNS:listener does not currently know of service requested in connect descriptor  
中文提示为ORA-12514： TNS： 监听程序当前无法识别连接描述符中请求服务  
针对这种情况就我而言是因为下载了Oracle的精简版（XE版）,所以连接的时候默认服务名应该是XE，而不是缺省值ORCL。这一点可以在服务（services.msc）里面看一下Oracle的服务是不是都是XE而不是ORCL 。具体可以查看 listrner.ora 中配置监听的服务名。详细不说了，可查到很多资料，这里只提出解决方案。
