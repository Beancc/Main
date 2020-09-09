```java
package com.els.web.servlet;

import com.alibaba.fastjson.JSONObject;
import com.els.dao.CloudApiMapper;
import com.els.service.AccountService;
import com.els.util.Base64;
import com.els.util.BeanUtils;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.web.context.WebApplicationContext;
import org.springframework.web.context.support.SpringBeanAutowiringSupport;
import org.springframework.web.context.support.WebApplicationContextUtils;

import java.awt.Color;
import java.awt.Font;
import java.awt.Graphics2D;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Random;

import javax.imageio.ImageIO;
import javax.servlet.ServletConfig;
import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import javax.ws.rs.core.Response;

/**
 * 生产验证码
 */
@WebServlet("/image/identifyingCode.img")
public class IdentifyingCodeServlet extends HttpServlet {

	private int imgWidth = 105;

	private int imgHeight = 35;

	private int codeCount = 6;

	private int x = 0;

	private int fontHeight;

	private int codeY;

	private String fontStyle = "Times New Roman";
	
	private static Random random=new Random(); 
	
	private String randomString="";

	private static final long serialVersionUID = 128554012633034503L;
	@Autowired
	private  CloudApiMapper cloudApiMapper;
	/**
	 * 初始化配置参数
	 */
	public void init() throws ServletException {
		x = imgWidth / (codeCount + 1);
		fontHeight = imgHeight - 2;
		codeY = imgHeight - 12;
	}

	/**
	 * 
	 * @param request
	 * @param response
	 * @throws ServletException
	 * @throws IOException
	 */
	protected void processRequest(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		response.setContentType("image/jpeg");
		response.setHeader("Pragma", "No-cache");
		response.setHeader("Cache-Control", "no-cache");
		response.setDateHeader("Expires", 0);
		HttpSession session = request.getSession(true);

		// 在内存中创建图象
		BufferedImage image = new BufferedImage(imgWidth, imgHeight, BufferedImage.TYPE_INT_RGB);

		// 获取图形上下文
		Graphics2D g = image.createGraphics();

		// 生成随机类
		Random random = new Random();

		// 设定背景色
		g.setColor(Color.WHITE);
		g.fillRect(0, 0, imgWidth, imgHeight);

		// 设定字体
		g.setFont(new Font(fontStyle, Font.PLAIN + Font.ITALIC, fontHeight));

		// 画边框
		g.setColor(new Color(55, 55, 12));
		g.drawRect(0, 0, imgWidth - 1, imgHeight - 1);

		// 随机产生155条干扰线，使图象中的认证码不易被其它程序探测到
		g.setColor(getRandColor(160, 200));
		for (int i = 0; i < 10; i++) {
			int x = random.nextInt(imgWidth);
			int y = random.nextInt(imgHeight);
			int xl = random.nextInt(12);
			int yl = random.nextInt(12);
			g.drawLine(x, y, x + xl, y + yl);
		}

		// 取随机产生的认证码(4位数字)
		Integer result = getRandomMathString();
		int red = 0, green = 0, blue = 0;
		for (int i = 0; i <= randomString.length(); i++) {
			red = random.nextInt(200);
			green = random.nextInt(200);
			blue = random.nextInt(200);
			g.setColor(new Color(red, green, blue));
			if(i==randomString.length()){
				g.drawString(String.valueOf("="), (i) * x, codeY);
			}else{
				g.drawString(String.valueOf(randomString.charAt(i)), (i) * x, codeY);
			}
		}
		// 将认证码存入SESSION
		session.setAttribute("rand", result.toString());
		// 图象生效
		g.dispose();
		ServletOutputStream responseOutputStream = response.getOutputStream();
		// 输出图象到页面
		ImageIO.write(image, "JPEG", responseOutputStream);

		// 以下关闭输入流！
		responseOutputStream.flush();
		responseOutputStream.close();
	}

	Color getRandColor(int fc, int bc) {// 给定范围获得随机颜色
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

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		processRequest(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		processRequest(request, response);
	}

	private char getSingleNumberChar() {
		Random random = new Random();
		int numberResult = random.nextInt(10);
		int ret = numberResult + 48;
		return (char) ret;
	}

	private char getLowerOrUpperChar(int upper) {
		Random random = new Random();
		int numberResult = random.nextInt(26);
		int ret = 0;
		if (upper == 0) {// 小写
			ret = numberResult + 97;
		} else if (upper == 1) {// 大写
			ret = numberResult + 65;
		}
		return (char) ret;
	}
	
    /**
     * 生成验证码字符串
     * */
    private Integer getRandomMathString(){
        int xx = (int)(Math.random()*9) + 1;//10-99的数
        int yy = (int)(Math.random()*90) + 10;

        Integer xyresult=null;
        StringBuilder suChinese =  new StringBuilder();
		int Randomoperands = (int) Math.round(Math.random() * 2);
		if (Randomoperands == 0) {
			xyresult = yy - xx;
			suChinese.append(yy);
			suChinese.append("-");
			suChinese.append(xx);
		} else if (Randomoperands == 1) {
			if (!(xx == 0) && yy % xx == 0) {
				xyresult = yy + xx;
				suChinese.append(yy);
				suChinese.append("+");
				suChinese.append(xx);
			} else {
				xyresult = yy + xx;
				suChinese.append(yy);
				suChinese.append("+");
				suChinese.append(xx);
			}
		} else if (Randomoperands == 2) {
			xyresult = yy - xx;
			suChinese.append(yy);
			suChinese.append("-");
			suChinese.append(xx);
		} else {
			xyresult = yy + xx;
			suChinese.append(yy);
			suChinese.append("+");
			suChinese.append(xx);
		}
        randomString = suChinese.toString();
        return xyresult;
    }

}

```
