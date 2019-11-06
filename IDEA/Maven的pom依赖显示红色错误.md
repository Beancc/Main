### 新手在Maven项目添加pom依赖的时候可能会遇到这样一个问题，就是明明我也是从Maven仓库https://mvnrepository.com/ 找到的依赖，为什么还会报错呢如下图所示：  
![](https://upload-images.jianshu.io/upload_images/17736870-adc36e011a46e63b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 原因的话应该是这个依赖包的版本和idea的版本不匹配，解决的方法很简单，只要设置一下就好了，点开设置，进入Maven的设置，将自动更新版本信息勾选上即可，如下图所示：
![](https://upload-images.jianshu.io/upload_images/17736870-a041654cb4be3436.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 点击确定以后会加载一会，大概十几秒后，可以看到已经不报错了。  
![](https://github.com/Beancc/Main/blob/master/img/333.jpg)
