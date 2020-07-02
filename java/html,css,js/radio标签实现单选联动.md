# 如何实现<s:radio>标签的单选联动 
### 1.今天遇到一个需求，是页面上两行单选框，一行是中文，一行是英文翻译。虽然需求部门没说，但是这种情况很明显是选中其中一个，对应的中/英文那一个选项也被选中，网上有很多复杂的方法，这里我使用了一个简单的方法。页面代码如下：  
```html
<td colspan="6">
  <s:radio list="#{'是,可以关闭CAPA':'是,可以关闭CAPA','否,需要进一步调查':'否,需要进一步调查'}" theme="simple" name="isClose" onclick="checkradio(this)"/><br>
  <s:radio list="#{'Yes,close CAPA':'Yes,close CAPA','No,conduct further investigation':'No,conduct further investigation'}" theme="simple" name="isCloseEn"onclick="checkradio(this)"/>  
</td>
```
#### 然后js方法实现如下：  
```js
<script>
function checkradio(obj){ 
  var isClose = $(obj).val();
  if(isClose=='是,可以关闭CAPA'){
    document.getElementsByName("isCloseEn")[0].checked=obj.checked 
  }else if(isClose=='否,需要进一步调查'){
    document.getElementsByName("isCloseEn")[1].checked=obj.checked 
  }else if(isClose=='Yes,close CAPA'){
    document.getElementsByName("isClose")[0].checked=obj.checked 
  }else{
    document.getElementsByName("isClose")[1].checked=obj.checked 
  }
} 
</script>
```
##### 很简单的实现了这个功能，因为这里用的struts2的radio的标签，如果是直接input的radio属性，稍微改一下代码就可以实现，具体就不在此赘言。

### 2.上面的方式有一个限制条件，就是两行单选框需要两个字段来保存，否则即使页面出现了单选联动，但是因为没有字段来储存，页面保存刷新后还是不显示单选框被选中。时隔一年又有类似的需求，但这次要求不能添加字段，想了很久才搞定，其实也很简单，同样是相互赋值的方式，但是给他们都增加一个value，显示实际存在的字段的值，就可以实现了。新需求的页面代码简化后如下：
```html
<tr>html
  <td>
  <s:radio list="#{'是':'是','否':'否'}" theme="simple" name="isSettle" onclick="copyis(this)" value="#{isSettle }"/>
  </td>
</tr>
<tr>
  <td>
  <s:radio list="#{'是':'是','否':'否'}" theme="simple" name="isSettle1" onclick="copyis(this)" value="#{isSettle }"/>
  </td>
</tr>
<tr>
  <td>
  <s:radio list="#{'是':'是','否':'否'}" theme="simple" name="isSettle2" onclick="copyis(this)" value="#{isSettle }"/>
  </td>
</tr>
```
#### 然后js方法实现如下：  
```js
function copyis(obj){
    var isSettle = $(obj).val();
    if(isSettle=='是'){
        document.getElementsByName("isSettle")[0].checked=obj.checked 
        document.getElementsByName("isSettle1")[0].checked=obj.checked 
        document.getElementsByName("isSettle2")[0].checked=obj.checked 
    }else if(isSettle=='否'){
        document.getElementsByName("isSettle")[1].checked=obj.checked 
        document.getElementsByName("isSettle1")[1].checked=obj.checked 
        document.getElementsByName("isSettle2")[1].checked=obj.checked 
    }
  }
```
#### 对比第一种方法，就是在radio里面多了一个value，但是这里是` value="#{isSettle }"`，用的是`#`而不是`$`，就这么一个地方，因为没考虑到这一点，卡了良久。
