* ReactDOM.render()

`ReactDOM.render` 是 `React` 的最基本方法，用于将虚拟元素（模板）转为 HTML 元素，并插入指定的 DOM 节点。

```js
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example');
);
```

上面代码将一个 h1 标题，插入 example 节点。

* 虚拟元素

 * 虚拟DOM元素
在上述所有的代码中，出现的 HTML 元素，并不是真正的 HTML 元素。而是一种虚拟元素，具体来说是**虚拟DOM元素**，它对应着原生的DOM元素，由React把它转义为真实 HTML 元素。

  * 组件元素
除此之外，还有一种虚拟元素：**组件元素**，组件元素也称之为**自定义元素**。组件元素需要通过一个类的实例化得到（类中必须有`render()`方法）。从这点上来看，组件元素跟组件是同一个东西。但是狭义来说，它们并不相等，因为组件是在组件元素的基础上，层层嵌套其他虚拟元素，并且拥有处理逻辑的整体。


* JSX 语法

上一节的代码， HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写。

```js
var names = ['Alice', 'Emily', 'Kate'];

ReactDOM.render(
  <div>
  {
    names.map(function (name) {
      return <div>Hello, {name}!</div>
    })
  }
  </div>,
  document.getElementById('example')
);
```

上面代码体现了 JSX 的基本语法规则：遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。

JSX 允许直接在模板插入 JavaScript 变量。如果这个变量是一个数组，则会展开这个数组的所有成员。

```js
var arr = [
  <h1>Hello world!</h1>,
  <h2>React is awesome</h2>,
];
ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('example')
);
```

上面代码的arr变量是一个数组，结果 JSX 会把它的所有成员，添加到模板。



