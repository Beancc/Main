#### 我印象中记得localstorage的大小是20M，但是百度了一下说5M的也有，说20M的也有。问了一下前端的朋友也都不能非常确定。于是找了一段代码，在浏览器console跑一下就OK。代码如下：

```javaScript
(function() {
    if(!window.localStorage) {
        console.log('当前浏览器不支持localStorage!')
    }    
    var test = '0123456789';
    var add = function(num) {
        num += num;
        if(num.length == 10240) {
            test = num;
            return;
        }
        add(num);
    }
    add(test);
    var sum = test;
    var show = setInterval(function(){
        sum += test;
        try {
            window.localStorage.removeItem('test');
            window.localStorage.setItem('test', sum);
            console.log(sum.length / 1024 + 'KB');
        } catch(e) {
            alert(sum.length / 1024 + 'KB超出最大限制');
            clearInterval(show);
        }
    }, 20)
})()
```

#### 最后得出结论是localstorage是5M大小。
