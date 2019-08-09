# 前台表格标签合并行或列后内容不能居中的解决方法  
### 在写form表单的时候，有时候可能需要合并行或列，如colspan和rowspan。但是发现当使用这两个属性合并单元格的时候，  `style="text-align:center;vertical-align:middle;"`这个居中属性就不起作用了。百度查询一下最终发现可以用这个方法实现：  
### `style="text-align:center;vertical-align: middle !important;"`
