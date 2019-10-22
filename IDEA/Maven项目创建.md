## Maven项目创建其实很简单，这里只简单说一下需要注意的地方。  
#### 第一步要注意的是创建项目的时候需要选择以下模板，免得创建完后还要进行一系列设置。
![](https://upload-images.jianshu.io/upload_images/17736870-6056ab6037c6c9b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
#### 第二个要注意的地方是在如下图所示的地方记得要配置一个archetypeCatalog=internal，否则创建完成的Maven项目就没有src目录哦。
![](https://upload-images.jianshu.io/upload_images/17736870-17d62e698ffe657e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 好了，那么问题来了，为什么会这样子呢。其实之所以创建了没有src目录是因为项目实际还没有创建完成，仔细看一下idea下方就看到它自己一直在下载插件。等一会下载完了自然就会有src目录了，不过这个一会儿可能需要十几分钟。而加了这一步就是配置了本地库，自然不需要下载过程就直接创建完成，正常显示src及以下的java和resource目录了。  
