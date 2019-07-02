# input输入框里不记录历史  
今天收到一个需求，就是在我原来的有日历控件的输入框里要求也可以键盘录入。  
* 修改前代码为`<input style="float: left;width:65%;" id="asmBirth" name="asmBirth" value='<s:date name="asmBirth" format="yyyy-MM-dd"/>' readonly="readonly" class="line"/>`  
* 既然需求为可以键盘录入，首先把readonly属性删除了，然后根据需求要有一个参考说明就加了一个placeholder。然后实际测试时又遇到一个问题，就是浏览器的自动记录历史会在输入的时候出现补全框。然后上网查了一下可以手动观点这个自动补全。代码为autocomplete="off"。  
* 修改后的代码`<input style="float: left;width:65%;" id="asmBirth" name="asmBirth" placeholder="1990-01-01" value='<s:date name="asmBirth" format="yyyy-MM-dd"/>' autocomplete="off" class="line"/>`
