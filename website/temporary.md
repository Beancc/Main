https://blog.csdn.net/weixin_36380516/article/details/56497508
ava如何实现验证码验证功能呢？日常生活中，验证码随处可见，他可以在一定程度上保护账号安全，那么他是怎么实现的呢？

Java实现验证码验证功能其实非常简单：用到了一个Graphics类在画板上绘制字母，随机选取一定数量的字母随机生成，然后在画板上随机生成几条干扰线。

首先，写一个验证码生成帮助类，用来绘制随机字母：

 
```
import java.awt.Color;
import java.awt.Font;
import java.awt.Graphics;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.io.OutputStream;
import java.util.Random;
 
import javax.imageio.ImageIO;
 
public final class GraphicHelper {
 
    /**
     * 以字符串形式返回生成的验证码，同时输出一个图片
     * 
     * @param width
     *            图片的宽度
     * @param height
     *            图片的高度
     * @param imgType
     *            图片的类型
     * @param output
     *            图片的输出流(图片将输出到这个流中)
     * @return 返回所生成的验证码(字符串)
     */
    public static String create(final int width, final int height, final String imgType, OutputStream output) {
	StringBuffer sb = new StringBuffer();
	Random random = new Random();
 
	BufferedImage image = new BufferedImage(width, height, BufferedImage.TYPE_INT_RGB);
	Graphics graphic = image.getGraphics();
 
	graphic.setColor(Color.getColor("F8F8F8"));
	graphic.fillRect(0, 0, width, height);
 
	Color[] colors = new Color[] { Color.BLUE, Color.GRAY, Color.GREEN, Color.RED, Color.BLACK, Color.ORANGE,
		Color.CYAN };
	// 在 "画板"上生成干扰线条 ( 50 是线条个数)
	for (int i = 0; i < 50; i++) {
	    graphic.setColor(colors[random.nextInt(colors.length)]);
	    final int x = random.nextInt(width);
	    final int y = random.nextInt(height);
	    final int w = random.nextInt(20);
	    final int h = random.nextInt(20);
	    final int signA = random.nextBoolean() ? 1 : -1;
	    final int signB = random.nextBoolean() ? 1 : -1;
	    graphic.drawLine(x, y, x + w * signA, y + h * signB);
	}
 
	// 在 "画板"上绘制字母
	graphic.setFont(new Font("Comic Sans MS", Font.BOLD, 30));
	for (int i = 0; i < 6; i++) {
	    final int temp = random.nextInt(26) + 97;
	    String s = String.valueOf((char) temp);
	    sb.append(s);
	    graphic.setColor(colors[random.nextInt(colors.length)]);
	    graphic.drawString(s, i * (width / 6), height - (height / 3));
	}
	graphic.dispose();
	try {
	    ImageIO.write(image, imgType, output);
	} catch (IOException e) {
	    e.printStackTrace();
	}
	return sb.toString();
    }
 
}
```
接着，创建一个servlet，用来固定图片大小，以及处理验证码的使用场景，以及捕获页面生成的验证码（捕获到的二维码与用户输入的验证码一致才能通过）。

 

 
```
import java.io.IOException;
import java.io.OutputStream;
 
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
 
@WebServlet(urlPatterns = "/verify/regist.do" )
public class VerifyCodeServlet extends HttpServlet {
 
    private static final long serialVersionUID = 3398560501558431737L;
 
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response)
	    throws ServletException, IOException {
 
	// 获得 当前请求 对应的 会话对象
	HttpSession session = request.getSession();
 
	// 从请求中获得 URI ( 统一资源标识符 )
	String uri = request.getRequestURI();
	System.out.println("hello : " + uri);
 
	final int width = 180; // 图片宽度
	final int height = 40; // 图片高度
	final String imgType = "jpeg"; // 指定图片格式 (不是指MIME类型)
	final OutputStream output = response.getOutputStream(); // 获得可以向客户端返回图片的输出流
								// (字节流)
	// 创建验证码图片并返回图片上的字符串
	String code = GraphicHelper.create(width, height, imgType, output);
	System.out.println("验证码内容: " + code);
 
	// 建立 uri 和 相应的 验证码 的关联 ( 存储到当前会话对象的属性中 )
	session.setAttribute(uri, code);
 
	System.out.println(session.getAttribute(uri));
 
    }
 
}
```
接着写一个HTML注册页面用来检验一下：

 

 
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>注册</title>
    <link rel="stylesheet" href="styles/general.css">
    <link rel="stylesheet" href="styles/cell.css">
    <link rel="stylesheet" href="styles/form.css">
	<script type="text/javascript" src="js/ref.js"></script>
    <style type="text/css" >
 
        .logo-container {
            margin-top: 50px ;
        }
        .logo-container img {
            width: 100px ;
        }
 
        .message-container {
            height: 80px ;
        }
 
        .link-container {
            height: 40px ;
            line-height: 40px ;
        }
 
        .link-container a {
            text-decoration: none ;
        }
 
    </style>
 
</head>
<body>
<div class="container form-container">
    <form action="/wendao/regist.do" method="post">
        <div class="form"> <!-- 注册表单开始 -->
 
            <div class="form-row">
                        <span class="cell-1">
                            <i class="fa fa-user"></i>
                        </span>
                        <span class="cell-11" style="text-align: left;">
                            <input type="text" name="username" placeholder="请输入用户名">
                        </span>
            </div>
 
            <div class="form-row">
                        <span class="cell-1">
                            <i class="fa fa-key"></i>
                        </span>
                        <span class="cell-11" style="text-align: left;">
                            <input type="password" name="password" placeholder="请输入密码">
                        </span>
            </div>
 
            <div class="form-row">
                        <span class="cell-1">
                            <i class="fa fa-keyboard-o"></i>
                        </span>
                        <span class="cell-11" style="text-align: left;">
                            <input type="password" name="confirm" placeholder="请确认密码">
                        </span>
            </div>
 
            <div class="form-row">
                        <span class="cell-7">
                            <input type="text" name="verifyCode" placeholder="请输入验证码">
                        </span>
                        <span class="cell-5" style="text-align: center;">
                            <img src="/demo/verify/regist.do" onclick="myRefersh(this)">
                        </span>
            </div>
 
            <div class="form-row" style="border: none;">
                        <span class="cell-6" style="text-align: left">
                           <input type="reset" value="重置">
                        </span>
                        <span class="cell-6"  style="text-align:right;">
                            <input type="submit" value="注册">
                        </span>
            </div>
 
        </div> <!-- 注册表单结束 -->
    </form>
</div>
 
</body>
</html>
```
效果如下图：

 



在控制台接收到的图片中验证码的变化如下：

 




当点击刷新页面的时候，验证码也会随着变化，但我们看不清验证码时，只要点击验证码就会刷新，这样局部的刷新可以用JavaScript来实现。

 

在<img src="/demo/verify/regist.do">中，添加一个问号和一串后缀数字，当刷新时让后缀数字不断改变，那么形成的验证码也会不断变化，我们可以采用的一种办法是后缀数字用date代替，date获取本机时间，时间是随时变的，这样就保证了刷新验证码可以随时变化。

代码如下：

 
```
function myRefersh( e ) {
	
	const source = e.src ; // 获得原来的 src 中的内容
	//console.log( "source : " + source  ) ;
	
	var index = source.indexOf( "?" ) ;  // 从 source 中寻找 ? 第一次出现的位置 (如果不存在则返回 -1 )
	//console.log( "index : " + index  ) ;
	
	if( index > -1 ) { // 如果找到了 ?  就进入内部
		var s = source.substring( 0 , index ) ; // 从 source 中截取 index 之前的内容 ( index 以及 index 之后的内容都被舍弃 )
		//console.log( "s : " + s  ) ;
		
		var date = new Date(); // 创建一个 Date 对象的 一个 实例
		var time = date.getTime() ; // 从 新创建的 Date 对象的实例中获得该时间对应毫秒值
		e.src = s + "?time=" + time ; // 将 加了 尾巴 的 地址 重新放入到 src 上
		
		//console.log( e.src ) ;
	} else {
		var date = new Date();
		e.src = source + "?time=" + date.getTime();
	}
	
}
```

https://www.cnblogs.com/thirteen-zxh/p/8942144.html
所需文件以及技术：

　　· SecurityUtil.java   （后面我会复制给大家）

　　· 图像处理技术

　　· 向客户端输出io流

　一，实现的原理，当视图页面加载的时候通过<img >元素的src属性去请求获得验证码图片，请求控制层验证码生成类随机生成4个字母或数字（验证码长度可以修改），将生成的验证码存储在session对象里面，最后通过ImageIO响应给客户端。

   二，实现的步骤：

　　　　1，html：　　　　　

复制代码
```
 <script type="text/javascript">
      function reloadCode() {           
 
 document.getElementById("imgSignCode").src="../signcode/signcode/get.do?r=" + new Date().getTime();     //这里为什么会加一个时间戳参数呢？  浏览器带有缓存功能
//当一个src中的URL请求一次后，再次请求浏览器就不会再去请求获得新数据，而是直接用
//上次请求返回的数据
    }
      </script>
      <body>
        <img id="imgSignCode" src="../signcode/signcode/get.do" onclick="reloadCode()" title="重新获取" style="cursor:pointer;"/>  
      </body> 
      ```
复制代码
　　2,Controller层方法：

复制代码
```
    /**
     * ajax获取验证码
     */
    @ResponseBody
    @RequestMapping(value = "/getSecurityCode.ajax", produces = {"application/json;charset=UTF-8"})
    public void getSecurityCode(HttpServletResponse response, HttpServletRequest request){
        // 通知浏览器不要缓存  
                response.setHeader("Expires", "-1");  
                response.setHeader("Cache-Control", "no-cache");  
                response.setHeader("Pragma", "-1");  
                SecurityUtil util = SecurityUtil.Instance();  
                // 将验证码输入到session中，用来验证  
                String code = util.getString();  
                request.getSession().setAttribute("code", code);  
                // 输出打web页面  
                try {
            ImageIO.write(util.getImage(), "jpg", response.getOutputStream());
        } catch (IOException e) {
            e.printStackTrace();
        } 
        }
```
复制代码
　　三，SecurityUtil代码：

　　

复制代码
```
package cc.royao.utils;

import java.awt.Color;
import java.awt.Font;
import java.awt.Graphics;
import java.awt.image.BufferedImage;
import java.util.Random;

public class SecurityUtil {
    
    private BufferedImage image;// 图像  
    private String str;// 验证码  
    private static char code[] = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ123456789".toCharArray();  
    public static final String SESSION_CODE_NAME="code";  
    private SecurityUtil() {  
        init();// 初始化属性  
    }  

    /* 
     * 取得RandomNumUtil实例 
     */  
    public static SecurityUtil Instance() {  
        return new SecurityUtil();  
    }  
    
    /* 
     * 取得验证码图片 
     */  
    public BufferedImage getImage() {  
        return this.image;  
    }  
    
    /* 
     * 取得图片的验证码 
     */  
    public String getString() {  
        return this.str;  
    }  
    
    private void init() {  
        // 在内存中创建图象  
        int width = 85, height = 20;  
        BufferedImage image = new BufferedImage(width, height, BufferedImage.TYPE_INT_RGB);  
        // 获取图形上下文  
        Graphics g = image.getGraphics();  
        // 生成随机类  
        Random random = new Random();  
        // 设定背景色  
        g.setColor(getRandColor(200, 250));  
        g.fillRect(0, 0, width, height);  
        // 设定字体  
        g.setFont(new Font("Times New Roman", Font.PLAIN, 18));  
        // 随机产生155条干扰线，使图象中的认证码不易被其它程序探测到  
        g.setColor(getRandColor(160, 200));  
        for (int i = 0; i < 155; i++) {  
            int x = random.nextInt(width);  
            int y = random.nextInt(height);  
            int xl = random.nextInt(12);  
            int yl = random.nextInt(12);  
            g.drawLine(x, y, x + xl, y + yl);  
        }  
        // 取随机产生的认证码(4位数字)  
        String sRand = "";  
        for (int i = 0; i < 4; i++) {  
            String rand = String.valueOf(code[random.nextInt(code.length)]);  
            sRand += rand;  
            // 将认证码显示到图象中  
            g.setColor(new Color(20 + random.nextInt(110), 20 + random.nextInt(110), 20 + random.nextInt(110)));  
            // 调用函数出来的颜色相同，可能是因为种子太接近，所以只能直接生成  
            g.drawString(rand, 13 * i + 6, 16);  
        }  
        // 赋值验证码  
        this.str = sRand;  
    
        // 图象生效  
        g.dispose();  
        this.image = image;/* 赋值图像 */  
    }  
    
    /* 
     * 给定范围获得随机颜色 
     */  
    private Color getRandColor(int fc, int bc) {  
        Random random = new Random();  
        if (fc > 255)  
            fc = 255;  
        if (bc > 255)  
            bc = 255;  
        int r = fc + random.nextInt(bc - fc);  
        int g = fc + random.nextInt(bc - fc);  
        int b = fc + random.nextInt(bc - fc);  
        return new Color(r, g, b);  
    }  
}
```

```
<br>
1. 设置request的编码
2. 获取验证码
3.判断程序生成的验证码和用户输入的验证码是否一致（从session中获取程序生成的验证码）
> 不一致：给用户提示信息：验证码错误的request（跳转页面）
> 一致：判断用户名密码是否正确，查询数据库判断。

```
1.图片的接口，get方法
如，将生成的数字计算后放到stringbuilder里面如叫做checkCode_session，然后存入session
如request.getSession().setAttribute("checkCode_session",checkCode_session);
然后在提交的接口里面，进行判断，首先获取这个session
 HttpSession session = request.getSession();
 String checkCode_session = (String)session.getAttribute("checkCode_session");
 为了验证码安全设置为一次性验证码，以获取就删除sesssion的值
 session.removeAttribute("checkCode_session");
 然后获取我后台的输入，如request.getParamer("checkCode");
然后进行判断
if(checkCode_session != null && checkCode_session.equals(checkCode)){

}else{
	request.setAttribute("cc_erroe","验证码错误，请重新输入");
}

```
