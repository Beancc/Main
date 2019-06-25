## 如何在input里面限定输入的内容的格式
* input仅限输入中文的写法
`<input type="text" onkeyup="this.value=this.value.replace(/[^\u4e00-\u9fa5]/g,'')">` 
*  input仅限输入英文的写法
`<input type="text" onkeyup="this.value=this.value.replace(/[^a-zA-Z]/g,'')"> `
* input仅限输入数字代码(小数点也不能输入)
`<input onkeyup="this.value=this.value.replace(/\D/g,'')" onafterpaste="this.value=this.value.replace(/\D/g,'')">  `
* inpt onkeyup="this.value=this.value.replace(/\D/g,'')" onafterpaste="this.value=this.value.replace(/\D/g,'')">  `
* inpuut仅限输入数字和小数点的写法
方法一：`<input onkeyup="if(isNaN(value))execCommand('undo')" onafterpaste="if(isNaN(value))execCommand('undo')">`
方法二：`<input name=txt1 onchange="if(/\D/.test(this.value)){alert('仅限输入数字');this.value='';}">`  
方法三：`<input onkeyup="this.value=this.value.replace(/[^\d.]/g,'')" onafterpaste="this.value=this.value.replace(/[^\d.]/g,'')" >`
