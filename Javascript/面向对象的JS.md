## 原型承继

打个意思相近的比方，如果建筑是基于类的系统，则建筑师会先画出房子的蓝图，然后房子都按照该蓝图来建造。如果建筑是基于原型的，建筑师会先建一所房子，然后将房子都建成像这种摸样的。

### 构造函数

所谓`构造函数`，其实就是一个普通函数，但是内部使用了`this`变量。
构造函数使用`new`生成实例对象，`this`变量会绑定在（指向）实例对象上。

```js
function People(name, sex){
	this.name=name;  //name会是生成的实例对象的属性
	this.sex=sex;
}

var pengkid = new People('鹏仔','男');
pengkid.name === ‘鹏仔’;  // true

//实例对象的constructor属性会指向它的构造函数
pengkid.constructor === 'People';   //true

//验证一个实例对象的原型
pengkid instanceof People;  //true
```

###  prototype属性

每个构造函数的`prototype`属性指向一个对象，对象实例会继承其所有的属性与方法。


```js
People.prototype.say = function(){console.log("我的名字是"+this.name)};

pengkid.say(); // 我的名字是鹏仔
```

* `hasOwnProperty()`

用来判断某一个属性到底是本地属性，还是继承自`prototype`对象的属性。

* `in`

判断某个实例是否含有某个属性，不管是不是本地属性。

>由原型属性（对象）构成的一系列（栈），就叫原型链。当访问一个对象的属性和方法的时候，除了会访问它自身外，还会访问它的原型链。原型链的最后总是 object.prototype = null 。


## call与apply函数

```js
obj.call(thisObj, arg1, arg2, ...);
obj.apply(thisObj, [arg1, arg2, ...]);
```

两者作用一致，都是把`obj`(即`this`)绑定到`thisObj`，这时候`thisObj`具备了`obj`的**属性**和**方法**。或者说`thisObj`『**继承**』了`obj`的属性和方法。

也可以当成，把`obj`上的方法，放到`thisObj`上执行。

> 参数是null或者undefined，等于将this绑定到全局对象。


## 绑定函数 bind()

`bind()`方法会创建并返回一个新函数，称为绑定函数。

当调用这个绑定函数时，绑定函数会以创建它时传入 `bind()`方法的第一个参数作为 `this`，传入 `bind()` 方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。

```js
this.num = 9;  
var mymodule = {  
  num: 81,
  getNum: function() { return this.num; }
};

mymodule.getNum(); // 81

var getNum = mymodule.getNum;  
getNum(); // 9, 因为在这个例子中，"this"指向全局对象

// 创建一个'this'绑定到module的函数
var boundGetNum = getNum.bind(module);  
boundGetNum(); // 81  
```

`bind()`函数可以使用预设的初始参数。

```js
function list() {
  return Array.prototype.slice.call(arguments);
}

var list1 = list(1, 2, 3); // [1, 2, 3]

// 创建函数并给函数预设的打头参数
var leadingThirtysevenList = list.bind(undefined, 37);

var list2 = leadingThirtysevenList(); // [37]
var list3 = leadingThirtysevenList(1, 2, 3); // [37, 1, 2, 3]
```

## this的用法

this 指的是它所在的方法被调用时，调用这个方法的对象。

随着`this`的使用场合，`this`的值会发生变化。总共有五种场合：

* 纯粹的函数调用

函数体内调用`this`，代表全局对象`Global`。

```js
var x = 1;
function test(){
　　this.x = 0;
}
test();
alert(x); //0
```

* 作为对象的方法调用

函数还可以作为某个对象的方法调用，这时this就指这个上级对象。

```js
var obj={
	x:10,
	fn:function () {
		console.log(this.x);
	}
}
obj.fn();//10
```

* 作为构造函数调用

所谓构造函数，就是通过这个函数生成一个新对象（`object`）。这时，`this`就指这个新对象。

```js
var x=10;
function test() {
	console.log(this.x);//undefined
	this.x=5;
	console.log(this.x);//5
}
var o=new test();
console.log(x);//10
console.log(o.x);//5
```

* apply和call调用

`apply()`是函数对象的一个方法，用来改变函数的调用对象。`this`指的就是这个参数。

```js
var x = 0;
function test(){
	alert(this.x);
}

var o={};
o.x = 1;
o.m = test;
o.m.apply();  // 0，函数调用时的变量环境是定义时的环境
o.m.apply(o); // 1，this代表对象o
```
`apply()`的参数为空时，默认调用全局对象。因此，这时的运行结果为`0`，证明`this`指的是全局对象。


* 箭头函数中调用

ES6中新增的箭头函数，完美修复了 this 的指向，即箭头函数中的 this 永远指向它的词法作用域（this的外层调用者）。

```js
var x  = 0;
var o1 = {
	x: 1,
	o2: {
		test: () => {
			console.log(this.x);
		}
	}
}

// ES5语法，输出 0
o1.o2.test();


// ES6语法，输出 1
o1.o2.test();
```



