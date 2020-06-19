##### 每个文件都有一个“独一无二”的MD5，我们可以通过判断两个文件的MD5是否相等来判断这两个是否是同一个文件。然而：
##### 不同文件字符串的md5也有可能会相同，其原因很简单，因为MD5是有限的，而字符串是无限的。今天参考了两个网站，用了以下程序比较了两张图片，果然MD5是相同的，感觉有点意思。代码在下面，比较的两张图片可以在代码中找到源网址。
```java
import java.io.File;
import java.io.FileInputStream;
import java.math.BigInteger;
import java.security.MessageDigest;
import java.util.HashMap;
import java.util.Map;

/**
 * 比较两张图片的MD5值是否相等
 */
public class Compare {
    /**
     * 获取单个文件的MD5值！
     *
     * @param file
     * @return
     */
    public static String getFileMD5(File file) {
        if (!file.isFile()) {
            return null;
        }
        MessageDigest digest = null;
        FileInputStream in = null;
        byte buffer[] = new byte[1024];
        int len;
        try {
            digest = MessageDigest.getInstance("MD5");
            in = new FileInputStream(file);
            while ((len = in.read(buffer, 0, 1024)) != -1) {
                digest.update(buffer, 0, len);
            }
            in.close();
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
        BigInteger bigInt = new BigInteger(1, digest.digest());
        String md5 = bigInt.toString(16);
        System.out.println("filePath：" + file.getPath() + "\nmd5：" + md5);
        return md5;
    }
    /**
     * 获取文件夹中文件的MD5值
     *
     * @param file
     * @param listChild ;true递归子目录中的文件
     * @return
     */
    public static Map<String, String> getDirMD5(File file, boolean listChild) {
        if (!file.isDirectory()) {
            return null;
        }
    //<filepath,md5>
        Map<String, String> map = new HashMap<String, String>();
        String md5;
        File files[] = file.listFiles();
        for (int i = 0; i < files.length; i++) {
            File f = files[i];
            if (f.isDirectory() && listChild) {
                map.putAll(getDirMD5(f, listChild));
            } else {
                md5 = getFileMD5(f);
                if (md5 != null) {
                    map.put(f.getPath(), md5);
                }
            }
        }
        return map;
    }
    public static void main(String[] args) {

//  https://crypto.stackexchange.com/questions/1434/are-there-two-known-strings-which-have-the-same-md5-hash-value
        String image1 = "F:\\desktop\\ship.jpg";
        String image2 = "F:\\desktop\\plane.jpg";

        File file1 = new File(image1);
        File file2 = new File(image2);
        System.out.println(getFileMD5(file1).equals(getFileMD5(file2))?"两张图片MD5相同":"两张图片MD5不相同");

    }

}
```
##### 综上所述：
* ##### 相同MD5的两个文件未必是同一个文件
* ##### 盗版别人的图片(?)等文件时用工具修改一下MD5成为自己的伪原创图片

##### 代码参考地址：https://blog.csdn.net/zhijiandedaima/article/details/81331850
##### 图片参考地址：https://crypto.stackexchange.com/questions/1434/are-there-two-known-strings-which-have-the-same-md5-hash-value
##### MD5解密(复杂密码要收费)：https://www.cmd5.com/
##### MD5解密(不收费，每次都验证)：https://www.somd5.com/
