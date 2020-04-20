##### split的用法比较简单，最简单的分割字符串的用法如下：  
```
  String str = "aaa,bbb,ccc";
  String strArray = str.split(",");
	System.out.println(Arrays.toString(strArray));
  for(String s : strArray){
    System.out.println(s); 
  }
```
##### 有一点要说明的是split后面跟的是正则表达式，这样就很好理解了，多个条件分割时用|，而有的情况下需要转义（*  ^ | 等符号），例子如下：
```
	String str = "aaa,bbb*ccc^ddd\\eee";
	String[] strArray = str.split(",|\\*|\\^|\\\\");
	for(String s : strArray){
	   System.out.println(s);       
	}
```
