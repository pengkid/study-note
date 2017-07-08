##概念

想要拖放某个元素，必须设置该元素的 draggable 属性为 true，当该属性为 false 时，将不允许拖放。

而 img 元素和 a 元素都默认设置了 draggable 属性为 true，可直接拖放，如果不想拖放这两个元素，把属性设为 false 即可。

##拖放事件

拖放事件由不同的元素产生。一个元素被拖放，他可能会经过很多个元素上，最终到达想要放置的元素内。这里，我暂时把被拖放的元素称为源对象，被经过的元素称为过程对象，到达的元素我称为目标对象。不同的对象产生不同的拖放事件。

###源对象

* `dragstart：源对象开始拖放`

* `drag：源对象拖放过程中`

* `dragend：源对象拖放结束`

###过程对象

* `dragenter：源对象开始进入过程对象范围内`

* `dragover：源对象在过程对象范围内移动`

* `dragleave：源对象离开过程对象的范围`

###目标对象

* `drop：源对象被拖放到目标对象内`

```php
<div id="source" draggable="true">a元素</div>
<div id="process">b元素</div>
<div id="target">c元素</div>

<script>
    var source = document.getElementById('source'),     // a元素
        process = document.getElementById('process'),   // b元素
        target = document.getElementById('target');     // c元素
    
    source.addEventListener('dragstart',function(ev){   // dragstart事件由a元素产生
        console.log('a元素开始被拖动');
    },false)

    process.addEventListener('dragenter',function(ev){  // dragenter事件由b元素产生
        console.log('a元素开始进入b元素');
    },false)
    process.addEventListener('dragleave',function(ev){  // dragleave事件由b元素产生
        console.log('a元素离开b元素');
    },false)

    target.addEventListener('drop',function(ev){        // drop事件由c元素产生
        console.log('a元素拖放到c元素了');
        ev.preventDefault();
    },false)
    document.ondragover = function(e){e.preventDefault();}
</script>
```

##dataTransfer 对象

在所有拖放事件中提供了一个数据传递对象 dataTransfer，用于在源对象和目标对象间传递数据。接下来认识一下这个对象的方法和属性，来了解它是如何传递数据的。

### setData()

该方法向 dataTransfer 对象中存入数据。接收两个参数，第一个表示要存入数据种类的字符串，现在支持有以下几种：

* text/plain：文本文字

* text/html：HTML文字

* text/xml：XML文字

* text/uri-list：URL列表，每个URL为一行

第二个参数为要存入的数据。例如：

```
event.dataTransfer.setData('text/plain','Hello World');
```

### getData()

该方法从 dataTransfer 对象中读取数据。参数为在 setData 中指定的数据种类。例如：
```
event.dataTransfer.getData('text/plain');
```

### clearData()

该方法清除 dataTransfer 对象中存放的数据。参数可选，为数据种类。若参数为空，则清空所有种类的数据。例如：
```
event.dataTransfer.clearData();
```

### setDragImage()

该方法通过用img元素来设置拖放图标。接收三个参数，第一个为图标元素，第二个为图标元素离鼠标指针的X轴位移量，第三个为图标元素离鼠标指针的Y轴位移量。例如：

```js
var source = document.getElementById('source'),
    icon = document.createElement('img');

icon.src = 'img.png';

source.addEventListener('dragstart',function(ev){
    ev.dataTransfer.setDragImage(icon,-10,-10)
},false)
```

### effectAllowed 和 dropEffect 属性

这两个属性结合起来设置拖放的视觉效果。

值得注意的是：dataTransfer 对象不支持IE。对，不支持IE。