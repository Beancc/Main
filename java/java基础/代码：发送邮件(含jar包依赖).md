## 利用java发送邮件的简单例子  
首先需要两个包JavaMail API 和Java Activation Framework (JAF) 。  
点击 [JavaMail](https://www.oracle.com/technetwork/java/index-138643.html) 下载。  
点击 [JAF](https://www.oracle.com/technetwork/java/jaf11-139815.html)下载。  
网盘地址：链接：https://pan.baidu.com/s/1mRe3-81h24lDtuUUkEy5sw 提取码：7eyk   
以QQ邮箱为例，代码如下  
```package com.cc.mailTest;

import java.util.Properties;
import javax.mail.Message;
import javax.mail.MessagingException;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.AddressException;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;

/**
 * @author 王聪
 * 创建时间：2019年6月18日 上午8:57:22
 *     
 * 利用QQ邮箱发送邮件
 * @version  	 1.0 
 */
public class SendEmail {


    public static void main(String[] args) throws AddressException,MessagingException {
        Properties properties = new Properties();
        properties.put("mail.transport.protocol", "smtp");// 连接协议
        properties.put("mail.smtp.host", "smtp.qq.com");// 主机名
        properties.put("mail.smtp.port", 465);// 端口号
        properties.put("mail.smtp.auth", "true");
        properties.put("mail.smtp.ssl.enable", "true");// 设置是否使用ssl安全连接 ---一般都使用
        properties.put("mail.debug", "true");// 设置是否显示debug信息 true 会在控制台显示相关信息
        // 得到回话对象
        Session session = Session.getInstance(properties);
        // 获取邮件对象
        Message message = new MimeMessage(session);
        // 设置发件人邮箱地址
        message.setFrom(new InternetAddress("dreamlonely@vip.qq.com"));
        // 设置收件人邮箱地址 
        message.setRecipients(Message.RecipientType.TO, new InternetAddress[]{new InternetAddress("407256915@qq.com"),new InternetAddress("1023132153@qq.com")});
        //message.setRecipient(Message.RecipientType.TO, new InternetAddress("xxx@qq.com"));//一个收件人
        // 设置邮件标题
        message.setSubject("邮件发送测试");
        // 设置邮件内容
        message.setText("该邮件由java发送，测试成功");
        // 得到邮差对象
        Transport transport = session.getTransport();
        // 连接自己的邮箱账户
        transport.connect("dreamlonely@vip.qq.com", "xxxxxxxxxxx");// 此处密码为QQ邮箱开通的smtp服务后得到的客户端授权码
        // 发送邮件
        transport.sendMessage(message, message.getAllRecipients());
        transport.close();
    }
	
}
```  
实际测试中使用QQ邮箱和163网易邮箱都可正常发送邮件，但是企业263邮箱测试时把ssl安全连接设置为true则报错“Exception in thread "main" javax.mail.MessagingException: Could not connect to SMTP host: smtp.sunon-china.com, port: 25;
  nested exception is:”，然后检查连接应该没有错误，把ssl安全连接设置为false才行。
