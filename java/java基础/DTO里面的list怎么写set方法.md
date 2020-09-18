在dto 所在类的文件里面定义个private List<bean> list = new ArrayList<bean>（）;
再写一个公共方法获取这个list
public List<bean> getList()
{
return list;
}


这样，在服务里面如果想给list赋值就可以直接写dto.getList().add();
