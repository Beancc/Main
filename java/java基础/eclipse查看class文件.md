# Eclipse通过安装Jadclipse插件直接查看class文件的方法  
如果想要查看.class文件，有一个好用的软件是jd-gui，但是使用eclipse进行项目开发时引入的jar包，如果你想查看（我通常习惯使用ctrl+鼠标左键的方式点击方法进入类），这时发现你导入的jar包没有导入source源码包的话，自然是无法查看了。这里推荐一个利用反编译插件实现查看class源码的方法。  
#### 1、下载Jadclipse插件
Jadclipse插件为Eclipse插件，可以在地址下载：  [Jadclipse](http://jadclipse.sourceforge.net/wiki/index.php/Main_Page) 
#### 2、下载Jad反编译工具
Jad反编译工具可以在地址下载：[Jad](https://varaneckas.com/jad/)  
依照惯例放上两个工具的网盘地址链接：https://pan.baidu.com/s/1G1SxMeJTkZE2CNPvZqU2-g  提取码：3xrp   
（注：官网下载时发现3.3版本说明支持eclipse3.3，实际使用时用eclipseMars（4.5版本）可以使用）  
#### 3、将Jadclipse放入Eclipse插件目录下
我下载的版本为net.sf.jadclipse_3.3.0.jar，然后将该jar放到D:\software\eclipse-jee-kepler-R-win32\eclipse\plugins目录下。  
#### 4、将Jad工具放到%JAVA_HOME%/bin目录下
将第二步下载的Jad压缩包解压，然后将jad.exe放入%JAVA_HOME%/bin目录（其实，存放路径无所谓，在eclipse中指名地址即可）  
#### 5、设置Eclipse
上面几步设置好后，重新打开eclipse，然后打开：Window->Preferences->Java->JadClipse，做如下设置：
<img alt="错误提示" src="https://upload-images.jianshu.io/upload_images/17736870-d1d6a9c33237e1b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240">    
#### 6、设置class文件默认打开方式
将下图中两项的默认打开方式设置为：JadClipse Class FileViewer （default）
<img alt="错误提示" src="https://upload-images.jianshu.io/upload_images/17736870-e58a8e0f7117bbe1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240">   
至此，反编译插件工具安装完毕，可以在eclipse里面直接查看.class文件了。
