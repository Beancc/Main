## Oracle启动的时候需要启动的服务和各服务的意义如下：  
#### 1. OracleServiceSID  
数据库服务，这个服务会自动地启动和停止数据库。如果安装了一个数据库，它的缺省启动类型为自动。服务进程为ORACLE.EXE，参数文件initSID.ora，日志文件SIDALRT.log，控制台SVRMGRL.EXE、SQLPLUS.EXE。  
#### 2. OracleHOME_NAMETNSListener
监听器服务，服务只有在数据库需要远程访问时才需要（无论是通过另外一台主机还是在本地通过 SQL*Net 网络协议都属于远程访问），不用这个服务就可以访问本地数据库，它的缺省启动类型为自动。服务进程为TNSLSNR.EXE，参数文件Listener.ora，日志文件listener.log，控制台LSNRCTL.EXE，默认端口1521、1526。  
#### 3. OracleHOME_NAMEAgent  
OEM代理服务，接收和响应来自OEM控制台的任务和事件请求，只有使用OEM管理数据库时才需要，它的缺省启动类型为自动。服务进程为DBSNMP.EXE，参数文件snmp_rw.ora，日志文件nmi.log，控制台LSNRCTL.EXE，默认端口1748。  
#### 4. OracleHOME_NAMEClientCache  
名字缓存服务，服务缓存用于连接远程数据库的Oracle Names 数据。它的缺省启动类型是手动。然而，除非有一台Oracle Names 服务器，否则没有必要运行这个服务。服务进程为ONRSD.EXE，参数文件NAMES.ORA，日志文件ONRSD.LOG，控制台NAMESCTL.EXE。  
#### 5. OracleHOME_NAMECMAdmin  
连接管理服务，是构建Connection Manager服务器所用，只有服务器作为Connection Manager才需要，它的缺省启动类型是手动。服务进程为CMADMIN.EXE，参数文件CMAN.ORA，日志文件CMADM_PID.TRC，控制台CMCTL.EXE，默认端口1830。  
#### 6. OracleHOME_NAMECMan  
连接网关服务，是构建Connection Manager服务器所用，只有服务器作为Connection Manager才需要，它的缺省启动类型是手动。服务进程为CMGW.EXE，参数文件CMAN.ORA，日志文件CMAN_PID.TRC，控制台CMCTL.EXE，默认端口1630。  
#### 7. OracleHOME_NAMEDataGatherer  
性能包数据采集服务，除非使用Oracle Capacity Planner 和 Oracle Performance Manager，否则不需要启动，它的缺省启动类型是手动。服务进程为VPPDC.EXE，日志文件alert_dg.log，控制台vppcntl.exe。  
#### 8. OracleHOME_NAMEHTTPServer  
Oracle提供的WEB服务器，一般情况下我们只用它来访问Oracle Apache 目录下的Web 页面，比如说JSP 或者modplsql 页面。除非你使用它作为你的HTTP服务，否则不需要启动（若启动它会接管IIS的服务），它的缺省启动类型是手动。服务进程为APACHE.EXE，参数文件httpd.conf，默认端口80。  
#### 9. OracleHOME_NAMEPagingServer  
通过一个使用调制解调器的数字传呼机或者电子邮件发出警告（没试过），它的缺省启动类型是手动。服务进程PAGNTSRV.EXE，日志文件paging.log。  
#### 10. OracleHOME_NAMENames  
Oracle Names服务，只有服务器作为Names Server才需要，它的缺省启动类型是手动。服务进程NAMES.EXE，参数文件NAMES.ORA，日志文件NAMES.LOG，控制台NAMESCTL.EXE，默认端口1575。  
#### 11. OracleSNMPPeerMasterAgent  
SNMP服务代理，用于支持SNMP的网管软件对服务器的管理，除非你使用网管工具监控数据库的情况，否则不需要启动，它的缺省启动类型是手动。服务进程为AGNTSVC.EXE，参数文件MASTER.CFG，默认端口161。  
#### 12. OracleSNMPPeerEncapsulater  
SNMP协议封装服务，用于SNMP协议转换，除非你使用一个不兼容的SNMP代理服务，否则不需要启动，它的缺省启动类型是手动。服务进程为ENCSVC.EXE，参数文件ENCAPS.CFG，默认端口1161。  
#### 13. OracleHOME_NAMEManagementServer  
OEM管理服务，使用OEM时需要，它的缺省启动类型是手动。服务进程为OMSNTSVR.EXE，日志文件oms.nohup。  
#### 一般启动OracleServiceSID和OracleHOME_NAMETNSListener就行了。 
[原文链接](https://zhidao.baidu.com/question/415197146.html)
