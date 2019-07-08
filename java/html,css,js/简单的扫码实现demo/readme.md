## html5-qrcode 使用文档

------

因为有一个BS架构的使用pad扫描二维码输入到input框的需求，找了很多资料最后用了这个实现。又因为是一个只用到js实现的简单的demo，所以实际测试中有两点不足，一个是使用时调出摄像头后需要拍照才能识别，另一个是识别精度还有待提高，只能拍正方形的二维码，如果你斜着拍二维码，那么对不起，error。其他细节不说了，因为忘了是在哪里看的这篇文章了所以无法注明出处，见谅。

对了，实际使用的时候只用到了index.html和lib包，至于src包里的东西全都没有用到就没有具体研究，不在这里深究。原作者说明如下：

首先我们应该知道使用h5新提供的属性getUserMedia这个属性，是可以调取系统的摄像头进行拍照或者是摄像的，但是兼容性支持的不好，所以当我们需要获取系统的多媒体权限时我们都不会采用这个属性。

使用<input type="file">标签我们可以间接的呼起系统选择文件的窗口，来读取系统文件。但是在WebView中，因为安卓权限的问题，我们是没办法直接获取读取文件这个操作的。而在原生的浏览器中是不存在这个问题的。所以选择使用这个input的时候一定要注意自己的页面是主要运行在webview中还是浏览器中。如果主要运行在客户端的webvie中，是需要客户端的同学支持的。

在IOS的某些系统版本中也会出现这个问题。具体的可以参考下面的参考文章。
参考文章：
http://blog.csdn.net/hvkcoder/article/details/51365191

https://forums.developer.apple.com/thread/22726

http://www.cnblogs.com/soaringEveryday/p/4495221.html

http://stackoverflow.com/questions/25942676/ios-8-sdk-modal-uiwebview-and-camera-image-picker



### 功能：

**1.**h5页面在微博客户端中呼起摄像头扫描二维码并且解析。
**2.**h5页面在非微博客户端中（原生浏览器或者微信客户端）呼起系统拍照或者上传图片按钮，拍照二维码或者上传二维码并且解析

### demo演示地址：

[http://test.qrcode.weibo.com/zhiqiang/WebComponent/html5-Qrcode/](http://test.qrcode.weibo.com/zhiqiang/WebComponent/html5-Qrcode/)

需要配置 hosts :
`xx.xxx.xxx.233 test.qrcode.weibo.com`

### 说明：

此插件需要配合`zepto.js` 或者 `jQuery.js`使用

### 使用方法：

**1.**在需要使用的页面按照下面顺序引入`lib`目录下的 js 文件

```javascript
    <script src="lib/zepto.js"></script>
    <script src="lib/qrcode.lib.min.js"></script>
    <script src="lib/qrcode.js"></script>
```

**2.**自定义按钮的 html 样式
为自定义的按钮添加自定义属性，属性名称为`node-type`
为 input 按钮添加自定义的属性, 属性名称为`node-type`

> 因为该插件需要使用`<input type="file" />` ，该 html 结构在网页上面是有固定的显示样式，为了能够自定义按钮样式，我们可以按照下面的示例代码结构嵌套代码

```html
    <div>
        <div class="qr-btn" node-type="qr-btn">扫描二维码1
            <input node-type="jsbridge" type="file" name="myPhoto" value="扫描二维码1" />
        </div>
    </div>
```

然后设置 `input` 按钮的 `css` 隐藏按钮，比如我使用的是属性选择器

```css
input[node-type=jsbridge]{
    display:none;
}
```

这里我们只需要按照自己的需要定义`class="qr-btn"`的样式即可。

**3.**在页面上初始化 Qrcode 对象

```javascript
    //初始化扫描二维码按钮，传入自定义的 node-type 属性
    $(function() {
        Qrcode.init($('[node-type=qr-btn]'));
    });
```
