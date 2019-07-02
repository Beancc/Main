# 如何生成git公钥  
* 首先我们知道，如果想要将本地仓库repository连接到github，首先要有一个本地的公钥。如何创建一个公钥呢。首先打开git bash,查一下是否存在公钥`ls -al ~/.ssh`  
* 如果显示不存在，则输入`ssh-keygen -t rsa -C "这里是邮箱"`
* 接下来的步骤没有仔细研究过，总之可以一直点回车大概三四次，直到出现以下界面则表示生成成功![](https://upload-images.jianshu.io/upload_images/17736870-95ff64448402b7a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
* key的目录也给出了就是在用户目录下面，比如我的是/c/Users/thinkpad/.ssh，进入目录打开文件就可以看到了，复制使用。
