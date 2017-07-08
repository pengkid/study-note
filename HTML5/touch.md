##移动端触摸事件

* touchstart

当手指放在屏幕上触发

* touchmove

当手指在屏幕上滑动时，连续触发

* touchend

当手指从屏幕离开时触摸

* touchcancel

当系统停止跟踪时触发(在拖动中断时候触发)，系统什么时候取消，文档没有明确的说明。

>由于触摸会导致屏幕动来动去，所以可以会在这些事件的事件处理函数内使用event.preventDefault()，来阻止屏幕的默认滚动。

触摸事件还包含下列三个用于跟踪触摸的属性：

* touches：表示当前跟踪的触摸操作的touch对象的数组

当一个手指在触屏上时，event.touches.length=1, 当两个手指在触屏上时，event.touches.length=2，以此类推。

* targetTouches：特定于事件目标的touch对象数组。

因为touch事件是会冒泡的，所以利用这个属性指出目标对象。

* changedTouches：表示自上次触摸以来发生了什么改变的touch对象的数组。

每个touch对象都包含下列几个属性：

```js
* clientX：触摸目标在视口中的x坐标。
* clientY：触摸目标在视口中的y坐标。
* clientX/clientY不包括对象滚动而隐藏的偏移量
* identifier：标识触摸的唯一ID。
* pageX：触摸目标在页面中的x坐标。
* pageY：触摸目标在页面中的y坐标。
//pageX/pageY包括对象滚动而隐藏的偏移量。
* screenX：触摸目标在屏幕中的x坐标。
* screenY：触摸目标在屏幕中的y坐标。
//screenX/screenY代表事件发生的位置对于屏幕的偏移量
target：触摸的DOM节点目标。
offsetX/offsetY：触摸目标相对与这个DOM元素左上角的定位，不包含边框。
```

event.touches[0]在touchend事件处理函数中，当该事件发生时，touches里面已经没有任何的touch对象了，此时，就要使用changeTouches集合。

##手势事件

* gesturestart

当一个手指已经按在屏幕上，而另一个手指又触摸在屏幕时触发。

* gesturechange

当触摸屏幕的任何一个手指的位置发生变化时触发。

* gestureend

当任何一个手指从屏幕上面移开时触发。

> 只有两个手指都触摸到事件的接收容器时才触发这些手势事件。
>
>1、当一个手指放在屏幕上时，会触发touchstart事件，如果另一个手指又放在了屏幕上，则会触发gesturestart事件，随后触发基于该手指的touchstart事件。
>
>2、如果一个或两个手指在屏幕上滑动，将会触发gesturechange事件，但只要有一个手指移开，则会触发gestureend事件，紧接着又会触发toucheend事件。

###手势的专有属性

* rotation

表示手指变化引起的旋转角度，负值表示逆时针，正值表示顺时针，从零开始。

* scale

表示两个手指之间的距离情况，向内收缩会缩短距离，这个值从1开始，并随距离拉大而增长。

