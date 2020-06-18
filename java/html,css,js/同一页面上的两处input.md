#### 标题说的有点模糊，具体描述一下需求。
* ##### 页面操作：
在一个流程页面，当用户选择不同的处理方式（单选框选择，如选择实时处理，会签还是库存处理），会流向不同的部门处理，所以页面也会不同。
* ##### 历史存留方式：
根据原来的开发人员写的是在同一个input-form.jsp的页面中，写了所有的相关表单，给所有的`<tr>`增加了name，然后根据需要用show和hide进行页面调整。我一个后端人员也没研究过这样写会好一点还是说写多个页面好一点，就不管他这一点了。
* ##### 开发前调整：
这里我首先把需要show和hide的`<tr>`，能同时显示和隐藏的，在外面包裹了一层`<tbody>`,然后给它个name，这样修改以后隐藏和显示大大减少了语句量。比如说下面的代码的页面
```html
<tr name="test1">
  <td></td><td></td><td></td><td></td>
</tr>
<tr name="test2">
  <td></td><td></td><td></td><td></td>
</tr>
```
隐藏需要以下两句
```JavaScript
$("tr[name=test1]").hide();
$("tr[name=test2]").hide();
```
但是在外面包裹一层`<tbody name="test"></tbodt>`以后，只需要下面一句
```js
$("#test").show();
```
* ##### 开发需求：
其次因为这次需求要再新增加两个流程页面，而且页面要做相应调整，这里就牵扯到一个我需要写新的`<input>`框，也就是正常情况下要新增字段，但是要求不能新增字段，而不新增字段却又两个同名的input的时候，每次保存都会保存两个input框里面的东西，造成的后果就是重复保存。这里想了一个办法就是这两个输入框互相赋值，但是显示的还是显示有保存的字段值。简化后的页面如下：
```html
  <input placeholder="接收数量" id="acceptNum" name="acceptNum" value="${acceptNum}" onkeyup="copyan();"/>
  <input placeholder="接收数量" id="acceptNum1" name="acceptNum1" value="${acceptNum}" onkeyup="copyan1();"/>
```
js实现如下：
```javascript
function copyan(){
  document.getElementById("acceptNum1").value=document.getElementById("acceptNum").value;
}
function copyan1(){
  document.getElementById("acceptNum").value=document.getElementById("acceptNum1").value;
}
```
然后想了想优化了一页面和js代码改为如下：
```html
  <input placeholder="接收数量" id="acceptNum" name="acceptNum" value="${acceptNum}" onkeyup="copyan(this);"/>
  <input placeholder="接收数量" id="acceptNum1" name="acceptNum1" value="${acceptNum}" onkeyup="copyan(this);"/>
```
```javascript
function copyan(obj){
  var acceptNum = $(obj).val();
  document.getElementById("acceptNum1").value=acceptNum;
  document.getElementById("acceptNum").value=acceptNum;
}
```
* ##### 总结：
上述代码很容易看出来，后台其实只有一个字段`acceptNum`，而我写的`acceptNum1`其实不是字段，只是给input增加的名字，然后用相互赋值的方法，把值赋给有字段的输入框然后保存，而现实的话也是显示的那个字段的值。
