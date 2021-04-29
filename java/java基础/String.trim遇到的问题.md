#### 简单说一下就是生产遇到一个问题，上传的excel取值后.trim()没有去掉空格。因为trim只能去掉半角空格，所以最初以为是全角空格。后来利用replaceAll的方式替换全角空格也无法去掉这个空格，然后又发现这个空格也不是tab键。
最后的解决方案只能是把这个空格复制过来，用replaceAll的方式去掉。然后我对几种空格做了一下实验如下：
```java
    public static void main(String[] args) {
        String a = "ademo ";//半角空格，可以.trim去掉
        String b = "bdemo　";//全角空格，不可以.trim去掉
        String c = "cdemo ";//tab复制到excel，可以.trim去掉
        String d = "ddemo ";//excel奇怪空格，不可以.trim去掉
    }
```
