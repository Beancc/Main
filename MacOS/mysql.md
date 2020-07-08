### 今天讲一下mysql的安装
##### 第一步找到mysql的安装包，嫌麻烦的老规矩：
```
链接: https://pan.baidu.com/s/1JSH0hKEBNp5ipd7FqyPvJw 提取码: 7ncp
```
##### 安装时无脑下一步即可，只是在设置密码的时候注意默认的强密码要设置8位，这一点和Windows上不太一样。
##### 安装完毕后可以点击“系统偏好设置”最下面找到mysql进行一些具体的配置，这里就不说了，嫌麻烦的没有需求的不用管它。
##### 这时候打开我的神奇iTerm，输入mysql显示`command not found: mysql`，这说明还没有‘添加工作路径’，配置方法如下：
1. ##### `cd /Users/cc`（cc是你home页面的名称）
2. ##### `touch .bash_profile`（创建.bash_profile文件，一般都已经有了，有了的话它就不会再创建，这行敲进去也没啥事）
3. ##### `open -e .bash_profile`（打开.bash_profile文件，是以txt形式打开的）
4. ##### 在打开的txt里面复制进去`alias mysql='/usr/local/mysql/bin/mysql';`（添加别名，将后面这个路径取别名为mysql，mysql安装的时候默认路径就是这个，可以跳转进去看一看）
5. ##### 保存并关闭你的.bash_profile文件,输入`source .bash_profile`（更新刚配置的环境变量）。到此结束配置
6. ##### 此时输入`mysql -u root -p`就会跳出来让你输入密码了，老规矩，输密码的时候没有任何显示。至此就全部OK了。

注：我看了一些教程视频会建议使用mysql5.6，究其原因，在于5.5及之前的版本不能使用集群，而之后的新版本估计也没有研究过，但是既然有了新版本在安全性上更好，理应使用新版本。以上mysql资源版本是8.0版，使用时注意依赖配置的版本如下
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.11</version>
</dependency>
```

参考资料：https://blog.csdn.net/Mart1nn/article/details/85019561  
参考资料：https://blog.csdn.net/w605283073/article/details/88096598

