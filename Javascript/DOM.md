
# DOM API

DOM：文档对象模型，表示一系列操作HTML或者XML文档的基础API集合。

DOM树：当浏览器加载文档的时候，浏览器会根据文档结构，解析出一系列的节点对象，并由这些节点组成的一个树状结构。


## DOM七大节点类型
	
* 文档节点(DOCUMENT_NODE)：代表整个文档，整个文档树的顶层节点
	
* 文档类型节点(DOCUMENT_TYPE_NODE)：代表文档的类型，如<!DOCTYPE html>

* 元素节点(ELEMENT_NODE)：代表文档中的各个元素

* 属性节点(ATTRIBUTE_NODE)：代表元素的属性

* 文本节点(TEXT_NODE)：代表标签与标签或者标签包含的文本

* 注释节点(COMMENT_NODE)：代表文档中的注释

* 文档片段节点(DOCUMENT_FRAGMENT_NODE)：代表文档的片段

>DocumentFragment是一种特殊的Node，它可以作为其他节点的一个临时容器，使得一组节点被当做一个节点看待。其次，它独立的而不是文档的一部分，所以它的parentNode总是为null，但类似ElementNode，它可以有任意多的子节点，也可以使用appendChild()等方法。


## DOM节点遍历全攻略

### 节点之间的关系

* 在一个节点之上的直接节点是其父节点 ，在其下一层的直接节点是其子节点

* 在同一层上具有相同父节点的节点是兄弟节点

* 在一个节点之下的所有层级的一组节点是其后代节点

* 一个节点的任何父节点、祖父节点和其上层的所有节点是其祖先节点

### 作为节点树的遍历

Document对象、Element对象和Text对象等的实例对象都承继于Node对象。
	
* 访问父节点

	* ele.parentNode（父节点永远是元素节点）


* 访问子节点
	* ele.childNodes（返回一个类数组对象）
	
	* ele.firstChild（第一个子节点）
	
	* ele.lastChild（最后子节点）

* 访问兄弟节点

	* ele.nextSibling（后一个兄弟）
	
	* ele.previousSibling（前一个兄弟）
	
* 访问节点文本
	
	* ele.textContent（除了返回该节点的文本内容，还会一并返回后代的所有文本）


* 访问节点类型
	
	* ele.nodeType（元素节点为1，属性节点为2，文本节点为3，注释节点为8，文档节点为9，文档类型节点为10）


* 访问节点名称

	* ele.nodeName（元素节点返回大写HTML，属性节点返回属性名，文本节点返回#text）


* 访问节点值

	* ele.nodeValue（只有文本节点和注释节点能返回自身文本字符串，其他节点都返回 null ）

### 作为元素树的遍历

JavaScript提供了另外一组API，它将文档看做是元素树，忽略部分文档：Text和Comment节点。

* 访问子元素节点
	* ele.children（类似ele.childNodes，返回一个类数组对象，但只包含元素子节点）
	
	* ele.firstElementChild（返回第一个元素子节点）
	
	* ele.lastElementChild（返回最后一个元素子节点）

* 访问兄弟元素节点
	* ele.nextElementSibling（返回后一个元素兄弟）
	
	* ele.previousElementSibling（返回前一个元素兄弟）
	
* 访问定位父节点：

	* ele.offsetParent（返回离元素最近，且有定位机制的父元素）


* 访问子元素节点数组长度：

	* ele.childElementCount（子元素的数量，返回的值和children.length值相等）


## NodeList对象和HTMLCollection对象

### NodeList

NodeList的实例对象是一个类数组对象，它的成员是节点对象。

NodeList接口实例对象提供length属性和数字索引，因此可以像数组那样，使用数字索引取出每个节点。但是它本身并不是数组，不能使用pop或push之类数组特有的方法。
	
比如 ele.childNodes、document.querySelectorAll()返回的都是NodeList的实例对象：

```js		
document.childNodes instanceof NodeList   //true
```

### HTMLCollection

HTMLCollection实例对象与NodeList实例对象类似，也是节点对象的集合，一个类数组对象。

比如 ele.children、document.forms返回的都是HMTLCollection的实例对象：

```js
document.forms instanceof HTMLCollection  //true
```

在document对象中，有一些快捷属性来访问元素节点，比如：document.images、document.forms和document.links等属性指向类数组的 img、form 和 a 元素集合，这些属性都是返回HTMLCollection实例对象。
	
在HTML5中，加入了document.scripts，它是HTMLCollection类型的 script 元素的集合。

### HTMLCollection与NodeList的区别

二者的实例对象都是类数组对象，但是二者存在某些区别：

 * HTMLCollection实例对象的成员只能是Element节点，NodeList实例对象的成员可以包含其他节点
 
 * HTMLCollection实例对象都是动态集合，节点的变化会实时反映在集合中。NodeList实例对象可以是静态集合
 
 * HTMLCollection实例对象可以用id属性或name属性引用节点元素，NodeList只能使用数字索引引用
		
 * HTMLCollection实例的item方法，可以根据成员的位置参数（从0开始）返回该成员，如果取不到成员或数字索引不合法，则返回null

 * HTMLCollection实例的namedItem方法根据成员的ID属性或name属性，返回该成员，如果没有对应的成员，则返回null。这个方法是NodeList实例不具有的


## DOM元素内容大揭秘

* `ele.innerHTML`：返回该元素的元素内容（可修改）

* `ele.outerHTML`：返回该元素所有HTML代码，包括自身和所有子元素（可修改）

* `ele.insertAdjacentHTML(pos, newNode)`

	* 将任意的HTML标记字符插入到指定的元素“相邻”的位置。
	
	* pos参数：“相邻”的精确含义依赖于第一个参数，第一个参数有以下值一："beforebegin"、"afterbegin"、"beforeend"、"afterend"
	
**上述属性和方法只存在于元素节点，对于其他类型的节点都是 undefined**

* ele.textContent：将指定元素的所有后代Text节点简单的串联在一起并返回。（在IE中，使用innerText替代textContent）


## DOM节点增改删查

### 创建节点（增）
	
* `document.createDoucmentFragment()`: 创建一个文档片段节点

* `document.createComment('comment')`: 创建一个注释节点，参数为注释值

* `document.createElement('ele')`: 创建元素节点，参数为标签名

* `document.createAttribute('att')`: 创建属性节点，参数为属性名

* `document.createTextNode('text')`: 创建文本节点，参数为文本值

* `ele.cloneNode()`: 用来复制已存在的节点。每个节点有该方法，返回该节点的一个全新副本，传递一个可选的布尔值为参数，如果参数true则同时克隆该节点的所有后代节点，否则只克隆该节点，默认为false

### 改造结构（改）

* `parentNode.appendChild(newNode)`: 接受一个节点对象为参数，将它作为最后一个子节点，插入当前节点

* `parentNode.insertBefore(newNode,oldNode)`: 在oldNode节点前，插入一个newNode节点

* `inserAfter(parentNode,newNode,oldNode)`

```js
function inserAfter(parentNode,newNode,oldNode){
	if(oldNode.nextSibling) parentNode.insertBefore(newNode,oldNode.nextSibling)
	else parentNode.appendChild(newNode)
}

// 如果要插入的节点是已存在文档中，那个节点将自动从它当前的位置移除并在新的位置重新插入
```

### 删除节点（删）
		
* `ele.parentNode.removeChild(ele)`: 删除父节点的一个子节点

* `oldEle.parentNode.replaceChild(newEle, oldEle)`: 把父节点的一个子节点替换成另外一个节点

### 查找节点（查）

&nbsp;&nbsp;&nbsp;&nbsp;查找元素节点

	document.getElementById()
	document.getElementsByClassName()
	document.getElementsByTagName()
	document.querySeletor()     //接受一个CSS选择器的字符串参数，返回第一个匹配的元素（以文档顺序），如果没有匹配的元素就返回null
	document.querySelectorAll() //接受一个CSS选择器的字符串参数，返回一个代表文档中匹配选择器的所有元素的NodeList对象。如果没有匹配的元素，则返回一个空的NodeList对象
	
&nbsp;&nbsp;&nbsp;&nbsp;查找属性节点

	eleNode.getAttribute('att')	//可读写
	eleNode.setAttribute('att','newAtt')


## DOM元素的几何尺寸

### 基本概念

文档：即HTML文档，document。

视口：浏览器用来显示文档的区域，除去标签页，滚动条，乱七八糟的，剩下就是视口。

坐标：元素的X和Y坐标元素自身的左上角是相对于视口或者文档的左上角的距离。

### 查询元素的几何尺寸

eleNode.getBoundingClientRect()：返回当前元素的一个坐标对象
```js
{
	top,	//元素顶部相对于视口的纵坐标，与y属性相等 
	bottom,	//元素底部相对于视口的纵坐标（等于top加上height）
	left,	//元素左上角相对于视口的横坐标，与x属性相等 
	right,	//元素右边界相对于视口的横坐标（等于left加上width）
	width,	//元素实际宽度（等于right减去left)
	height	//元素实际高度（等于y加上height）
}
```

### 具体查询元素的具体几何尺寸

* `ele.clientHeight`

获取当前元素的可视区域高度，即内容区的高度+padding-top+padding-bottom

* `ele.clientWidth`

获取当前元素的可视区域宽度，即内容区的宽度+padding-left+padding-right

* `ele.offsetHeight`

获取当前元素的实际高度，即内容区的高度+padding-top+padding-bottom+border-top+border-bottom

* `ele.offsetWidth`

获取当前元素的实际宽度，即内容区的宽度+padding-left+padding-right+border-left+border-right
	
* `ele.clientLeft`

获取当前元素的左边框，右边框 = (offsetWidth - clientWidth) - clientLeft

* `ele.clientTop`

获取当前元素的上边框，底边框 = (offsetHeight - clientHeight) - clientTop

* `ele.offsetLeft`

获取当前元素相对于父元素的位置，元素左边框到父元素左边框，绝对定位的 left + margin-left

* `ele.offsetTop`

获取当前元素相对于父元素的位置，元素上边框到父元素上边框，绝对定位的 top + margin-top

### 查询滚动元素的几何尺寸

* ele.scrollHeight

获取滚动元素的滚动区域总高度（不含边框）

* ele.scrollWidth

获取滚动元素的滚动区域总宽度（不含边框）

* ele.scrollLeft

获取滚动条被隐藏的区域大小，滚动条左边框距离最左方区域

* ele.scrollTop

获取滚动条被隐藏的区域大小，滚动条上边框距离最上方区域


要让滚动条滚动到最初始的位置，那么可以写一个函数：

```js	
function scrollStart (ele) {
	if ( ele.scrollTop != 0 ) {
		ele.scrollTop = 0;
	}
}
```

如果要查看整张网页的水平的和垂直的滚动距离，要从 document.body元素上读取，这两个属性都可读写，设置该属性的值，会导致浏览器将指定元素自动滚动到相应的位置：
		
```js
document.body.scrollLeft    //网页可见区域宽

document.body.scrollTop	 //网页可见区域宽

```
### 获取页面大小大全

```js
document.body.clientWidth	//网页可见区域宽

document.body.clientHeight   //网页可见区域高

document.body.offsetWidth(包括边线的宽)	//网页可见区域宽

document.body.offsetHeight(包括边线的宽)   //网页可见区域高

document.body.scrollWidth	 //网页正文全文宽

document.body.scrollHeight	//网页正文全文高

document.body.scrollTop       //网页被卷去的高，IE7无效

document.body.scrollLeft      //网页被卷去的左，IE7无效


window.screen.height          //屏幕分辨率的高

window.screen.width           //屏幕分辨率的宽

window.screen.availHeight     //屏幕可用工作区高度

window.screen.availWidth      //屏幕可用工作区宽度
```


## 关于 document 鲜为人知的属性和方法

* `document.documentElement`：返回 html 根元素，即整个文档
* `document.head`：返回 head 头标签
* `document.body`：返回 body 体标签
* `document.domain`：查看当前文档的所在域名
* `document.location`：同window对象的location属性，引用location对象
* `document.cookie`：操作浏览器的cookie
* `document.referrer`：表示文档访问来源，如果无法获取来源或用户直接键入网址，则返回一个空字符串
* `document.URL`：获取文档的URL，该属性值与 location.href 的初始值相同
* `document.readyState`：获取文档的状态，loading：加载HTML代码阶段（尚未完成解析），interactive：加载外部资源阶段时，complete：DOM节点树加载完成时
* `document.getSelection()`：返回一个Selection对象，该对象描述了当前用户选取的一系列对象 
* `document.getSelection().focusNode.data`：获取当前用户选中的内容


