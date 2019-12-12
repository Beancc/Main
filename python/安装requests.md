#### 网上down了一段爬虫程序，直接用python自带的IDE运行，报错`ModuleNotFoundError: No module named 'requests'`
#### OK，没有这个模块那就安装这个模块，利用CMD，进入`..\Python\Python37\Scripts`目录下，输入代码`pip install requests`
#### 安装到17%突然出现了一个红色的Exception，后面跟着大量的红色报错，拉到最下面发现有句黄色的提醒，大体是版本太旧，有新版本安装。
![](https://upload-images.jianshu.io/upload_images/17736870-29c35b67dae01e30.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/17736870-32f973a6ee3ad9d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 那好吧，根据它的提醒运行`python -m pip install --upgrade pip`进行安装，很快就安装完成。
#### 安装完成以后重新执行`pip install requests`，发现没有报错，安装完成。重新执行爬虫程序可正常运行。
