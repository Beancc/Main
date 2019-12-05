# linux作死术  
`sudo rm -rf /`  
#### 递归强制删除根目录下文件以及子目录下所有文件，包括操作系统本身，不可恢复。瑟瑟发抖，不解释。  
#### 今天碰巧看到了一篇执行上述命令后恢复的技术文章，具体用到了两个软件，这里不谈了。但是好奇心的驱使下，我在不用的linux虚拟机尝试执行以上命令，因为本身是root账户，所以执行`rm -rf /`,然后提示如下  
```
rm: it is dangerous to operate recursively on '/'
rm: use --no-preserve-root to override this failsafe
```
#### 意思是
#### rm: 在'/' 进行递归操作十分危险
#### rm: 使用 --no-preserve-root 选项跳过安全模式
#### 原来最新版的linux都不允许执行这个命令了，然而，我又尝试了命令`rm -rf /*`，果然，开始报错并删除，大约五分钟以后删除完毕。我尝试了一些常用命令果然都无法实现，然后当关闭Terminal以后就无法打开，桌面图片变成空白，功能键报错。  
![](https://upload-images.jianshu.io/upload_images/17736870-c0619a118d1f0ea4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 至此，更新最新的linux作死术为
`sudo rm -rf /*`  
