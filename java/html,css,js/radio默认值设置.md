#### 有一个坑，是在用radio的时候通过value设置默认值不能正常显示，百度了才知道，如果radio中的key是字符串的话，在双引号里面还要再放单引号，如下：
`		【选择环节流向】：<s:radio list="#{'实时处理':'实时处理','会签':'会签','库存处理':'库存处理'}" theme="simple" name="badFlow" value="'会签'" onclick="beforeSubmitForm()"/>`
#### 以上是struts2的radio，radio同理。
