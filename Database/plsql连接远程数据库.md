# 如何用plsql连接远程Oracle数据库  
------
### 如果本地安装了Oracle数据库的话就很简单，网上查一下配置一下就好了，问题是如果本地没有安装Oracle，然后想直接连接远程数据库怎么办，期间走了很多弯路，现在记下来。  
1.首先下载安装plsql以后，打开不登录，点击取消(cancel)直接进入plsql  
2.这时要下载oci，推荐直接下载instantclient_11_2文件夹，其中包含了oci。Oracle官网可以直接下载，但是因为速度比较慢，下载还要登录，推荐百度找一个，或者惯例百度云链接：https://pan.baidu.com/s/1525fdg4DJ7IJpL5ssP5tHQ  提取码：1df1   
3.将这个文件夹放到一个固定的地方，推荐在plsql的安装目录下如D:\plsql\instantclient_11_2  
4.点击如图所示的首选项，或者英文版的找到tools/preferrence
![](https://upload-images.jianshu.io/upload_images/17736870-4d68c4eb919fc9fd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
5.根据安装的instantclient_11_2位置，在如下位置进行配置  
![](https://upload-images.jianshu.io/upload_images/17736870-96996f6543ee63af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
6.此时关闭plsql再重新输入用户名/用户密码/ip/端口号/SID就可以登录成功了。格式如下  
![](https://upload-images.jianshu.io/upload_images/17736870-c7032e9fed1e4134.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
