### 有时候我们需要提取所有的sheet名做目录等，但是一个一个复制又太麻烦，这里提供一种简单的方法。  
#### 1. 首先要先自己定义一个公式，我们可以自己取名，比如说这里取名为get，引用位置输入=GET.WORKBOOK(1)，点击确定保存即可。如下图所示  
![](https://upload-images.jianshu.io/upload_images/17736870-ae9f49f500b592d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
#### 2.我们随便找个单元格，假设B2，输入=INDEX(get,ROW(A1))回车。没错，这里的get就是你刚才起的名字get，然后向下填充获得你的所有sheet名。  
#### 3.这时候发现会带着工作簿的名字，然后我们在C2输入=MID(B2,FIND("]",B2)+1,100)，下拉填充就可以得到我们想要的sheet名了。这句话的意思是针对B2单元格找到"]",然后从加1位开始，取到第100位。  
![](https://upload-images.jianshu.io/upload_images/17736870-cde917b4dae50b9b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
#### 注意：如果有错误或无法实现，则注意要启用宏。
