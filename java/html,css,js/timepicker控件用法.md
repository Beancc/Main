#### 背景是在做人员档案时候需要输入年龄的input框用的是时间控件，然而默认年份选择是当前年份的前十年和后十年，即点开下拉框会显示2009-2029年。（做这个项目的时候是2019年）显然不能满足年龄的选择，当时查了一些资料发现方法都不太适合这个项目，最终在看控件源码时发现里面用到了一个`yearRange:'c-10:c+10'`,果断判断这个就是原来下拉框的实现，然后在input里面增加如下代码改为下拉框显示的数据是当前日期-60年到当前日期。


```
$('#asmBirth').datepicker({
  changeYear:'true',
  changeMonth:'true',
  yearRange:"c-60:c"
});

```

 #### 在查阅资料时候发现以下博文对时间控件的讲解比较详细可供参考：
https://www.cnblogs.com/SJBlog/p/6479709.html
