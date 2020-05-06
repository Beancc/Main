# `<script>`放在`<body>`中有效果，但是放在`<head>`中没有效果  
>原因是文档还没加载，就读了js，js就不起作用了  
想在head里用的话  
window.onload = function(){  
//这里包裹代码  
}  
就可以啦
