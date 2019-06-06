# Eclipse通过安装Jadclipse插件直接查看class文件的方法  
如果想要查看.class文件，有一个好用的软件是jd-gui，但是使用eclipse进行项目开发时引入的jar包，如果你想查看（我通常习惯使用ctrl+鼠标左键的方式点击方法进入类），这时发现你导入的jar包没有导入source源码包的话，自然是无法查看了。这里推荐一个利用反编译插件实现查看class源码的方法。  
#### 1、下载Jadclipse插件
Jadclipse插件为Eclipse插件，可以在地址下载：Jadclipse  
#### 2、下载Jad反编译工具
Jad反编译工具可以在地址下载：Jad
（注：官网下载时发现3.3版本说明支持eclipse3.3，实际使用时用eclipseMars（4.5版本）可以使用）  
#### 3、将Jadclipse放入Eclipse插件目录下
我下载的版本为net.sf.jadclipse_3.3.0.jar，然后将该jar放到D:\software\eclipse-jee-kepler-R-win32\eclipse\plugins目录下。  
#### 4、将Jad工具放到%JAVA_HOME%/bin目录下
将第二步下载的Jad压缩包解压，然后将jad.exe放入%JAVA_HOME%/bin目录（其实，存放路径无所谓，在eclipse中指名地址即可）  
#### 5、设置Eclipse
上面几步设置好后，重新打开eclipse，然后打开：Window->Preferences->Java->JadClipse，做如下设置：
