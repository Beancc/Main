* #### 启动tomcat `./startup.sh`  
* #### 关闭tomcat `./shutdown.sh`
* #### 查看tomcat是否关闭 `ps -ef|grep java`
#### 如果显示类似如下内容则此时tomcat未关闭，如果执行关闭指令无法关闭则此时可以杀死tomcat
```
root     15060     1  4 15:11 pts/0    00:00:02 /root/jdk1.8.0_231/bin/java -
Djava.util.logging.config.file=/root/apache-tomcat-8.5.47/conf/logging.properties -
Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -
Djdk.tls.ephemeralDHKeySize=2048 -Djava.protocol.handler.pkgs=org.apache.catalina.webresources -
Dorg.apache.catalina.security.SecurityListener.UMASK=0027 -Dignore.endorsed.dirs= -
classpath /root/apache-tomcat-8.5.47/bin/bootstrap.jar:/root/apache-tomcat-8.5.47/bin/tomcat-juli.jar -
Dcatalina.base=/root/apache-tomcat-8.5.47 -Dcatalina.home=/root/apache-tomcat-8.5.47 -
Djava.io.tmpdir=/root/apache-tomcat-8.5.47/temp org.apache.catalina.startup.Bootstrap start

```  
* #### 杀死tomcat `kill -9 15060`
* #### 重新执行命令查看，如果显示类似如下内容则此时tomcat已关闭  
```
root     15187 14735  0 15:13 pts/0    00:00:00 grep java
```
* #### 想要在tomcat部署静态网页，需要打开apache-tomcat-8.5.47/conf/server.xml，在`<Engine></Engine>`之间再添加一个`<Host></Host>`如下：其中`name`输入云服务器的ip地址，`docBase`输入apache-tomcat-8.5.47/webapps下面新建的文件夹名称
```
<Host name="106.13.190.201" debug="0" appBase="webapps" unpackWARs="true" autoDeploy="true" xmlValidation="false" xmlNamespaceAware="false">
<Context path="" docBase="examples" debug="0" reloadable="true" crossContext="true"/>
<Logger className="org.apache.catalina.logger.FileLogger" directory="logs" prefix="tot_log." suffix=".txt" timestamp="true"/>
</Host>
```
