```
    public static void main(String[] args) {
        String a = "test";
        int[] b = {1,2,3};
        List c = new ArrayList();
        c.add(a);
        System.out.println(a.length());
        System.out.println(b.length);
        System.out.println(c.size());
    }
```
#### 其实看着一段代码就能知道了，length是判断数组里面元素的个数，length()是用来判断字符串的长度，而size()则用来判断集合的元素个数。其他的不必多说了，运行结果分别是4,3,1。
