# plsql如果显示中文为???只要配置一下环境变量就好了  
*  变量名称：NLS_LANG  
   变量值：SIMPLIFIED CHINESE_CHINA.ZHS16GBK 
 ![](https://upload-images.jianshu.io/upload_images/17736870-4cf9b8d30ff04de3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 
 这样重新打开plsql再进行查询就可以看到原来显示??的中文部分可以正常显示了
  
* 在安装plsql13的时候发现不存在这个无法显示中文的问题了，就无需上述操作。  
  
* ### 2019年7月26日更新 在执行查询sql语句的时候条件是where creator is '王聪'查询无结果，但是在Navicat里面可以正常查询，想来想去还是加上了以上环境变量，果然可以正常查询。总结：无论安装什么版本，都配置以上环境变量吧。
