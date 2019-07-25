#### onfocus -> 键盘输入 -> onkeydown -> onkeypress -> onkeyup -> oninput -> 失去焦点 ->  onchange -> onblur  
```
    function handleFocus (event) {
        console.log('onfocus事件', 'value=' + event.target.value, 'keyCode=' + event.keyCode);
    };

    function handleKeyDown (event) {
        console.log('onkeydown事件', 'value=' + event.target.value, 'keyCode=' + event.keyCode);
    }

    function handleKeyPress (event) {
        console.log('onkeypree事件', 'value=' + event.target.value, 'keyCode=' + event.keyCode);
    }

    function handleKeyUp (event) {
        console.log('onkeyup事件', 'value=' + event.target.value, 'keyCode=' + event.keyCode);
    }

    function handleInput (event) {
        console.log('oninput事件', 'value=' + event.target.value, 'keyCode=' + event.keyCode);
    }

    function handleChange (event) {
        console.log('onchange事件...', 'value=' + event.target.value, 'keyCode=' + event.keyCode);
    };

    function handleBlur (event) {
        console.log('onblue事件', 'value=' + event.target.value, 'keyCode=' + event.keyCode)
    }
```

### onfocus
　　　　并没有什么特别的，就是当焦点转移到（点击，tab切换） input 框上边的时候触发；
### onkeydown  
* 键盘按下的时候触发，但是此时按下的值并没有被输入到 input ，所以，此时的 value 没有值，或者说它的值 只能是之前的旧值  
* 另外，此时可以阻止按键的默认事件；
### onkeypress  
* 按键在按下之后，并且是按键松开之前触发的；  
* 和 keydown 一样不能获取新的到 value；此时，也可以阻止按键的默认事件；  
* 但是这个事件对一下按键的支持不好，一些非输入性质的按键（如；delete, backspare）不支持；（除enter）；
### oninput  
* 这个事件很贼，它的触发时机，从上面就可以看到，onpress 之后 onkeyup 之前；  
* 此时，已经可以拿到 value，不能拿到keycode，不可以阻止默认事件了 ；  
* 关键是这货明明是每次输入框的值变化时候出发的，抢了onchange 的饭碗；  
* 另外，这东西是新的，IE9以下不支持，需要使用 onpropertychange；  
* 还有这货，仅仅在input， textarea 支持；
### onkeyup  
* 按键在松开之后触发的；  
* 能获取新的到 value，keycode；此时，不可以阻止按键的默认事件；
### onchange  
* 你敢说这是你认识的onchange吗？反正我是不敢；在失去焦点之后触发的，明明是 onchange 为什么是在失去焦点后触发的，还偏偏比 onblur 快；  
* 能获取新的到 value，不能拿到 keycode；此时，不可以阻止按键的默认事件；
### onblur  
* 失去焦点时候触发，但是还是比 onchange 慢了；  
* 能获取新的到 value，不能拿到 keycode；  

### 原文链接：https://www.cnblogs.com/this-day/p/9087419.html

