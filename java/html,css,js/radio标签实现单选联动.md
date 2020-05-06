# 如何实现<s:radio>标签的单选联动 
#### 今天遇到一个需求，是页面上两行单选框，一行是中文，一行是英文翻译。虽然需求部门没说，但是这种情况很明显是选中其中一个，对应的中/英文那一个选项也被选中，网上有很多复杂的方法，这里我使用了一个简单的方法。页面代码如下：  
```
<td colspan="6">
  <s:radio list="#{'是,可以关闭CAPA':'是,可以关闭CAPA','否,需要进一步调查':'否,需要进一步调查'}" theme="simple" name="isClose" onclick="checkradio(this)"/><br>
  <s:radio list="#{'Yes,close CAPA':'Yes,close CAPA','No,conduct further investigation':'No,conduct further investigation'}" theme="simple" name="isCloseEn"onclick="checkradio(this)"/>  
</td>
```
#### 然后js方法实现如下：  
```
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
