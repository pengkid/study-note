* [JSON数据格式](#index1)
* [JSON和JS对象的八卦](#index2)
  * [具体区别](#index2_1)
  * [示例](#index2_2)
* [JSON中的函数](#index3)
  * [JSON.stringify()](#index3_1)
  * [JSON.parse()](#index3_2)
  * [JSON.toJSON()](#index3_3)


## <font color="4590a3">JSON数据格式{#index1}</font>

JSON 是一种基于文本传输的数据格式，在这种格式下，可以衍生出很多 JSON 数据。

在JSON之前，有一个数据格式叫xml，现在还是广泛在用，但是JSON更加轻量，如xml需要用到很多标签。

标签本身占据了很多空间，而JSON比较轻量，即相同数据以JSON的格式占据的带宽更小。

## <font color="4590a3">JSON和JS对象的八卦{#index2}</font>

JSON 跟JS对象不是同一个玩意，JSON是一种数据格式，JS对象是一个存在于内存中的实例。

### <font color="4590a3">具体区别{#index2_1}</font>


|对比|JSON          |JS对象        |
|---------------|-------------|-------------|
|键名| 必须加双引号 | 可以加单引号、双引号，甚至没有 |
|属性值| 只能是数值（10制）、字符串（双引号）、布尔值、null<br/>也可以是数组或者符合要求的JS对象<br/>不能是函数、NaN、undefined、Infinity和-Infinity | 爱啥啥      |
|数值| 前导不能为0，小数点后必须有数字 | 没有限制      |

可以这么说，JSON对象是JS对象的一个子集，只要JS对象符合JSON格式，那么这个JS对象就是JSON对象。

### <font color="4590a3">示例{#index2_2}</font>

```
// 这只是 JS 对象
var obj1 = {}; 

// 这只也是 JS 对象
var obj2 = {
    width:100,
    "height":200,
    'name':"rose",
    say:function(){console.log(this.name)}
};


// 这个称做：JSON 格式的 JavaScript 对象 ，简称 JSON对象			
var obj3 = {
    "width":100,
    "height":200,
    "name":"rose"
};

// 这个称做：JSON 格式的字符串，简称 JSON字符串，这是常见的 JSON 数据格式
var str1 = '{"width":100,"height":200,"name":"rose"}';

// 这个可叫 JSON 格式的数组，是 JSON 的稍复杂一点的形式
var arr = [
    {"width":100,"height":200,"name":"rose"},
    {"width":100,"height":200,"name":"rose"},
    {"width":100,"height":200,"name":"rose"},
];

// 这个可叫稍复杂一点的 JSON 格式的字符串     
var str2='['
    +'{"width":100,"height":200,"name":"rose"},'
    +'{"width":100,"height":200,"name":"rose"},'
    +'{"width":100,"height":200,"name":"rose"},'
    +']';

```


## <font color="4590a3">JSON中的函数{#index3}</font>

### <font color="4590a3">JSON.stringify(){#index3_1}</font>
 
把JSON对象转换成JSON字符串（序列化）。

#### <font color="4590a3">语法</font>
`JSON.stringify(value[, replacer [, space]])`  

##### <font color="4590a3">参数</font>

* value

函数接受的第一个参数为 JSON 格式的JS对象

`JSON.stringify({"name":"pengkid","age":18}) → "{"name":"pengkid","age":18}"`

· undefined、函数 以及 symbol 值 若出现在属性值，则取消该属性，若出现在数组里面，则转换为 null

· NaN、Infinity和-Infinity，不论在数组还是非数组的对象中，都被转化为null

· 键名没有双引号，或者是单引号，则转换为""，字符串是单引号的，会自动变成双引号

· 布尔值、数字、字符串的包装对象会自动转换成对应的原始值，如 new String("bala")会变成"bala"

* replacer

函数接受的第二个参数，为一个匿名函数或数组。

`JSON.stringify(value, function(key, value){} | [])`

· 如果是函数，该函数会遍历对象的键值对，并作出相应的处理

· 如果是数组，则查找原对象中是否含有数组中对应的元素，有则保留，无则删除

* space

函数接受的第三个参数，修饰符，指定缩进用的空白字符。

`JSON.stringify({"age":10},null,"HAHAHAHA");  // "{HAHAHAHA"age":10}"
`

· 是1-10的某个数字，代表用几个空白字符

· 是字符串的话，就用该字符串代替空格，最多取这个字符串的前10个字符

· 没有提供该参数 等于 设置成null 等于 设置一个小于1的数

### <font color="4590a3">JSON.parse(){#index3_2}</font> 

把JSON字符串转换成JS标准对象（反序列化）。

#### <font color="4590a3">语法</font>
`JSON.parse(text[, reviver])`

##### <font color="4590a3">参数</font>

* text

函数接受的第一个参数为 JSON 格式的字符串，如果不是标准的JSON字符串，则会报错。

`JSON.parse('{"age":10}') → {age:10}`

* reviver

函数接受的第二个参数为一个匿名函数，这个函数作用在属性已经被解析但是还没返回前，将属性处理后再返回

`JSON.parse('obj',function(key, value){})`

匿名函数返回 undefined，则当前属性会删除，如果返回其他值，则返回的值会成为当前属性新的属性值。

### <font color="4590a3">JSON.toJSON(){#index3_3}</font>

在一个JS对象上实现了toJSON方法，那么调用 JSON.stringify去序列化这个JS对象时JSON.stringify会把这个对象的toJSON方法返回的值作为参数去进行序列化

```
var info={  
    "msg":"I Love You",
    "toJSON":function(){
        var replaceMsg=new Object();
        replaceMsg["msg"]="Go Die";
        return replaceMsg;
    }
};

JSON.stringify(info);  // '"{"msg":"Go Die"}"'

```