## 正则表达式

正则表达式（英语：Regular Expression，在代码中常简写为regex、regexp或RE）使用单个字符串来描述、匹配一系列符合某个句法规则的字符串搜索模式。

搜索模式可用于文本搜索和文本替换。

### 什么是正则表达式？

正则表达式是由一个字符序列形成的搜索模式。

当你在文本中搜索数据时，你可以用搜索模式来描述你要查询的内容。

正则表达式可以是一个简单的字符，或一个更复杂的模式。

正则表达式可用于所有文本搜索和文本替换的操作。

### 语法

```js
/正则表达式主体/修饰符(可选)
```

### 使用字符串方法

在 JavaScript 中，正则表达式通常用于两个字符串方法 : search() 和 replace()。

**search() 方法** 用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串，并返回子串的起始位置。

**replace() 方法** 用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。

### 正则表达式修饰符

**修饰符** 可以在全局搜索中不区分大小写:

| 修饰符 | 描述                                                     |
| :----- | :------------------------------------------------------- |
| i      | 执行对大小写不敏感的匹配。                               |
| g      | 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。 |
| m      | 执行多行匹配。                                           |



------

### 正则表达式模式

方括号用于查找某个范围内的字符：

| 表达式 | 描述                       |
| :----- | :------------------------- |
| [abc]  | 查找方括号之间的任何字符。 |
| [0-9]  | 查找任何从 0 至 9 的数字。 |
| (x\|y) | 查找任何以 \| 分隔的选项。 |

元字符是拥有特殊含义的字符：

| 元字符 | 描述                                        |
| :----- | :------------------------------------------ |
| \d     | 查找数字。                                  |
| \s     | 查找空白字符。                              |
| \b     | 匹配单词边界。                              |
| \uxxxx | 查找以十六进制数 xxxx 规定的 Unicode 字符。 |

量词:

| 量词 | 描述                                  |
| :--- | :------------------------------------ |
| n+   | 匹配任何包含至少一个 *n* 的字符串。   |
| n*   | 匹配任何包含零个或多个 *n* 的字符串。 |
| n?   | 匹配任何包含零个或一个 *n* 的字符串。 |

在常规的比较中，数据类型是被忽略的，以下 if 条件语句返回 true：

var x = 10;
var y = "10";
if (x == y)





在严格的比较运算中，=== 为恒等计算符，同时检查表达式的值与类型，以下 if 条件语句返回 false：

switch 语句会使用恒等计算符(===)进行比较:



在 JavaScript 中, **null** 用于对象, **undefined** 用于变量，属性和方法。

对象只有被定义才有可能为 null，否则为 undefined。



## JavaScript 验证 API

------

### 约束验证 DOM 方法

| Property            | Description                                                  |
| :------------------ | :----------------------------------------------------------- |
| checkValidity()     | 如果 input 元素中的数据是合法的返回 true，否则返回 false。   |
| setCustomValidity() | 设置 input 元素的 validationMessage 属性，用于自定义错误提示信息的方法。使用 setCustomValidity 设置了自定义提示后，validity.customError 就会变成true，则 checkValidity 总是会返回false。如果要重新判断需要取消自定义提示，方式如下：`setCustomValidity('')  setCustomValidity(null)  setCustomValidity(undefined)` |

### 约束验证 DOM 属性

| 属性              | 描述                                  |
| :---------------- | :------------------------------------ |
| validity          | 布尔属性值，返回 input 输入值是否合法 |
| validationMessage | 浏览器错误提示信息                    |
| willValidate      | 指定 input 是否需要验证               |

------

#### Validity 属性

input 元素的 **validity 属性**包含一系列关于 validity 数据属性:

| 属性            | 描述                                                       |
| :-------------- | :--------------------------------------------------------- |
| customError     | 设置为 true, 如果设置了自定义的 validity 信息。            |
| patternMismatch | 设置为 true, 如果元素的值不匹配它的模式属性。              |
| rangeOverflow   | 设置为 true, 如果元素的值大于设置的最大值。                |
| rangeUnderflow  | 设置为 true, 如果元素的值小于它的最小值。                  |
| stepMismatch    | 设置为 true, 如果元素的值不是按照规定的 step 属性设置。    |
| tooLong         | 设置为 true, 如果元素的值超过了 maxLength 属性设置的长度。 |
| typeMismatch    | 设置为 true, 如果元素的值不是预期相匹配的类型。            |
| valueMissing    | 设置为 true，如果元素 (required 属性) 没有值。             |
| valid           | 设置为 true，如果元素的值是合法的。                        |

let 声明的变量只在 let 命令所在的代码块 **{}** 内有效，在 **{}** 之外不能访问。

const 用于声明一个或多个常量，声明时必须进行初始化，且初始化后值不可再修改：

const 的本质: const 定义的变量并非常量，并非不可变，它定义了一个常量引用一个值。使用 const 定义的对象或者数组，其实是可变的。下面的代码并不会报错：

##### 实例

// 创建常量对象 const car = {type:"Fiat", model:"500", color:"white"};  // 修改属性: car.color = "red";  // 添加属性 car.owner = "Johnson";


[尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_const_object)

但是我们不能对常量对象重新赋值：

##### 实例

const car = {type:"Fiat", model:"500", color:"white"}; car = {type:"Volvo", model:"EX60", color:"red"};    // 错误   

JSON 是用于存储和传输数据的格式。

JSON 通常用于服务端向网页传递数据 。



##### 相关函数

| 函数                                                         | 描述                                           |
| :----------------------------------------------------------- | :--------------------------------------------- |
| [JSON.parse()](https://www.runoob.com/js/javascript-json-parse.html) | 用于将一个 JSON 字符串转换为 JavaScript 对象。 |
| [JSON.stringify()](https://www.runoob.com/js/javascript-json-stringify.html) | 用于将 JavaScript 值转换为 JSON 字符串。       |

#### href="#"与href="javascript:void(0)"的区别

**#** 包含了一个位置信息，默认的锚是**#top** 也就是网页的上端。

而javascript:void(0), 仅仅表示一个死链接。

在页面很长的时候会使用 **#** 来定位页面的具体位置，格式为：**# + id**。

如果你要定义一个死链接请使用 javascript:void(0) 。



函数表达式可以 "自调用"。

自调用表达式会自动调用。

如果表达式后面紧跟 () ，则会自动调用。

不能自调用声明的函数。

通过添加括号，来说明它是一个函数表达式：

##### 实例

(function () {
  var x = "Hello!!";   // 我将调用自己
})();



##### 箭头函数

ES6 新增了箭头函数。

箭头函数表达式的语法比普通函数表达式更简洁。

```
(参数1, 参数2, …, 参数N) => { 函数声明 }

(参数1, 参数2, …, 参数N) => 表达式(单一)
// 相当于：(参数1, 参数2, …, 参数N) =>{ return 表达式; }
```

当只有一个参数时，圆括号是可选的：

```
(单一参数) => {函数声明}
单一参数 => {函数声明}
```

没有参数的函数应该写成一对圆括号:

```
() => {函数声明}
```

##### 实例

// ES5 

var x = function(x, y) {     return x * y; }  

// ES6 

const x = (x, y) => x * y;

### JavaScript 闭包

还记得函数自我调用吗？该函数会做什么？

##### 实例

var add = (function () {    var counter = 0;    return function () {return counter += 1;} })();  add(); add(); add();  // 计数器为 3


[尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_function_counter3)

##### 实例解析

变量 **add** 指定了函数自我调用的返回字值。

自我调用函数只执行一次。设置计数器为 0。并返回函数表达式。

add变量可以作为一个函数使用。非常棒的部分是它可以访问函数上一层作用域的计数器。

这个叫作 JavaScript **闭包。**它使得函数拥有私有变量变成可能。

计数器受匿名函数的作用域保护，只能通过 add 方法修改。

> 闭包是一种保护私有变量的机制，在函数执行时形成私有的作用域，保护里面的私有变量不受外界干扰。直观的说就是形成一个不销毁的栈环境。 



## 对事件做出反应

我们可以在事件发生时执行 JavaScript，比如当用户在 HTML 元素上点击时。

如需在用户点击某个元素时执行代码，请向一个 HTML 事件属性添加 JavaScript 代码：

onclick=*JavaScript*

HTML 事件的例子：

- 当用户点击鼠标时
- 当网页已加载时
- 当图像已加载时
- 当鼠标移动到元素上时
- 当输入字段被改变时
- 当提交 HTML 表单时
- 当用户触发按键时

### onload 和 onunload 事件

onload 和 onunload 事件会在用户进入或离开页面时被触发。

onload 事件可用于检测访问者的浏览器类型和浏览器版本，并基于这些信息来加载网页的正确版本。

onload 和 onunload 事件可用于处理 cookie。

### onchange 事件

onchange 事件常结合对输入字段的验证来使用。

下面是一个如何使用 onchange 的例子。当用户改变输入字段的内容时，会调用 upperCase() 函数。

##### 实例

<input type="text" id="fname" **onchange**="upperCase()">

### onmouseover 和 onmouseout 事件

onmouseover 和 onmouseout 事件可用于在用户的鼠标移至 HTML 元素上方或移出元素时触发函数。

### onmousedown、onmouseup 以及 onclick 事件

onmousedown, onmouseup 以及 onclick 构成了鼠标点击事件的所有部分。首先当点击鼠标按钮时，会触发 onmousedown 事件，当释放鼠标按钮时，会触发 onmouseup 事件，最后，当完成鼠标点击时，会触发 onclick 事件。





### addEventListener() 方法

##### 实例

在用户点击按钮时触发监听事件：

document.getElementById("myBtn").addEventListener("click", displayDate);





addEventListener() 方法用于向指定元素添加事件句柄。

addEventListener() 方法添加的事件句柄不会覆盖已存在的事件句柄。

你可以向一个元素添加多个事件句柄。

你可以向同个元素添加多个同类型的事件句柄，如：两个 "click" 事件。

你可以向任何 DOM 对象添加事件监听，不仅仅是 HTML 元素。如： window 对象。

addEventListener() 方法可以更简单的控制事件（冒泡与捕获）。

当你使用 addEventListener() 方法时, JavaScript 从 HTML 标记中分离开来，可读性更强， 在没有控制HTML标记时也可以添加事件监听。

你可以使用 removeEventListener() 方法来移除事件的监听。

------

##### 语法

*element*.addEventListener(*event, function, useCapture*);

第一个参数是事件的类型 (如 "click" 或 "mousedown").

第二个参数是事件触发后调用的函数。

第三个参数是个布尔值用于描述事件是冒泡还是捕获。该参数是可选的。

| ![Note](https://www.runoob.com/images/lamp.jpg) | 注意:不要使用 "on" 前缀。 例如，使用 "click" ,而不是使用 "onclick"。 |
| ----------------------------------------------- | ------------------------------------------------------------ |
|                                                 |                                                              |



------

### 向原元素添加事件句柄

### 

当用户点击元素时弹出 "Hello World!" :

*element*.addEventListener("click", function(){ alert("Hello World!"); });



你可以使用函数名，来引用外部函数:

##### 实例

当用户点击元素时弹出 "Hello World!" :

*element*.addEventListener("click", myFunction);

function myFunction() {
  alert ("Hello World!");
}





------

### 向同一个元素中添加多个事件句柄

addEventListener() 方法允许向同一个元素添加多个事件，且不会覆盖已存在的事件：

##### 实例

*element*.addEventListener("click", myFunction);
*element*.addEventListener("click", mySecondFunction);




你可以向同个元素添加不同类型的事件：

##### 实例

*element*.addEventListener("mouseover", myFunction);
*element*.addEventListener("click", mySecondFunction);
*element*.addEventListener("mouseout", myThirdFunction);

### 事件冒泡或事件捕获？

事件传递有两种方式：冒泡与捕获。

事件传递定义了元素事件触发的顺序。 如果你将 <p> 元素插入到 <div> 元素中，用户点击 <p> 元素, 哪个元素的 "click" 事件先被触发呢？

在 *冒泡* 中，内部元素的事件会先被触发，然后再触发外部元素，即： <p> 元素的点击事件先触发，然后会触发 <div> 元素的点击事件。

在 *捕获* 中，外部元素的事件会先被触发，然后才会触发内部元素的事件，即： <div> 元素的点击事件先触发 ，然后再触发 <p> 元素的点击事件。

addEventListener() 方法可以指定 "useCapture" 参数来设置传递类型：

addEventListener(*event*, *function*, ***useCapture\***);

默认值为 false, 即冒泡传递，当值为 true 时, 事件使用捕获传递。



### removeEventListener() 方法

removeEventListener() 方法移除由 addEventListener() 方法添加的事件句柄:

##### 实例

*element*.removeEventListener("mousemove", myFunction);

### 创建新的 HTML 元素 (节点) - appendChild()

要创建新的 HTML 元素 (节点)需要先创建一个元素，然后在已存在的元素中添加它。

### 创建新的 HTML 元素 (节点) - insertBefore()

以上的实例我们使用了 **appendChild()** 方法，它用于添加新元素到尾部。

如果我们需要将新元素添加到开始位置，可以使用 **insertBefore()** 方法:

### 移除已存在的元素

要移除一个元素，你需要知道该元素的父元素。

### 替换 HTML 元素 - replaceChild()

我们可以使用 replaceChild() 方法来替换 HTML DOM 中的元素。

## nodeType 属性

nodeType 属性返回节点的类型。nodeType 是只读的。

比较重要的节点类型有：

| 元素类型 | NodeType |
| :------- | :------- |
| 元素     | 1        |
| 属性     | 2        |
| 文本     | 3        |
| 注释     | 8        |
| 文档     | 9        |

### element.

* element.id设置或返回元素的idelement.innerHTML设置或者返回元素的内容，可包含节点中的子标签以及内容
* element.innerText设置或者返回元素的内容，不包含节点中的子标签以及内容
* element.className设置或者返回元素的类名
* element.nodeName返回该节点的大写字母标签名
* element.nodeType返回该结点的节点类型，1表示元素节点；2表示属性节点……
* element.nodeValue返回该节点的value值，元素节点的value值为null
* element.childNodes返回元素的子节点的nodeslist对象，nodeslist类似于数组，有length属性，可以使用方括号[index]访问指定索引的值
* element.firstChild/element.lastChild返回元素的第一个/最后一个子节点（包含注释节点和文本节点）
* element.parentNode返回该结点的父节点
* element.previousSibling返回与当前节点同级的上一个节点（包含注释节点和文本节点）
* element.nextSibling返回与当前节点同级的下一个节点（包含注释节点和文本节点）
* element.chileElementCount：返回子元素（不包括文本节点以及注释节点）的个数
* element.firstElementChild /lastElementChild返回第一个/最后一个子元素（不包括文本节点以及注释节点）
* element.previousElementSibling/nextElementSibling返回前一个/后一个兄弟元素（不包括文本节点以及注释节点）
* element.clientHeight/clientWidth返回内容的可视高度/宽度（不包括边框，边距或滚动条）
* element.offsetHeight/offsetWidth /offsetLeft/offsetTop返回元素的高度/宽度/相对于父元素的左偏移/右偏移（包括边框和填充，不包括边距）

# 对象

## Number 对象

###  JavaScript 数字均为 64 位

JavaScript 不是类型语言。与许多其他编程语言不同，JavaScript 不定义不同类型的数字，比如整数、短、长、浮点等等。

在JavaScript中，数字不分为整数类型和浮点型类型，所有的数字都是由 浮点型类型。JavaScript 采用 IEEE754 标准定义的 64 位浮点格式表示数字，它能表示最大值为 ±1.7976931348623157e+308，最小值为 ±5e-324。

### 精度

整数（不使用小数点或指数计数法）最多为 15 位。

小数的最大位数是 17，但是浮点运算并不总是 100% 准确：

### 无穷大（Infinity）

### NaN - 非数字值

### 数字可以是数字或者对象

数字可以私有数据进行初始化，就像 x = 123;

JavaScript 数字对象初始化数据， var y = new Number(123);

### Number 属性

| 属性                     | 描述                                                  |
| :----------------------- | :---------------------------------------------------- |
| Number.MAX_VALUE         | 最大值                                                |
| Number.MIN_VALUE         | 最小值                                                |
| Number.NaN               | 非数字                                                |
| Number.NEGATIVE_INFINITY | 负无穷，在溢出时返回                                  |
| Number.POSITIVE_INFINITY | 正无穷，在溢出时返回                                  |
| Number.EPSILON           | 表示 1 和比最接近 1 且大于 1 的最小 Number 之间的差别 |
| Number.MIN_SAFE_INTEGER  | 最小安全整数。                                        |
| Number.MAX_SAFE_INTEGER  | 最大安全整数。                                        |

### 数字方法

| 方法                   | 描述                                                         |
| :--------------------- | :----------------------------------------------------------- |
| Number.parseFloat()    | 将字符串转换成浮点数，和全局方法 [parseFloat()](https://www.runoob.com/jsref/jsref-parsefloat.html) 作用一致。 |
| Number.parseInt()      | 将字符串转换成整型数字，和全局方法 [parseInt()](https://www.runoob.com/jsref/jsref-parseint.html) 作用一致。 |
| Number.isFinite()      | 判断传递的参数是否为有限数字。                               |
| Number.isInteger()     | 判断传递的参数是否为整数。                                   |
| Number.isNaN()         | 判断传递的参数是否为 isNaN()。                               |
| Number.isSafeInteger() | 判断传递的参数是否为安全整数。                               |

## 字符串（String） 对象

### 在字符串中查找字符串

字符串使用 indexOf() 来定位字符串中某一个指定的字符首次出现的位置：

如果没找到对应的字符函数返回-1

lastIndexOf() 方法在字符串末尾开始查找字符串出现的位置。

### 内容匹配

**match()**函数用来查找字符串中特定的字符，并且如果找到的话，则返回这个字符。

### 替换内容

**replace()** 方法在字符串中用某些字符替换另一些字符。

### 字符串大小写转换

字符串大小写转换使用函数 **toUpperCase()** / **toLowerCase()**:

### 字符串转为数组

字符串使用**split()**函数转为数组:

~~~javascript
txt="a,b,c,d,e"  // String
txt.split(",");  // 使用逗号分隔
txt.split(" ");  // 使用空格分隔
txt.split("|");  // 使用竖线分隔 
~~~

## Date（日期） 对象

使用 Date() 方法获得当日的日期。


使用 getFullYear() 获取年份。


getTime() 返回从 1970 年 1 月 1 日至今的毫秒数。


使用 setFullYear() 设置具体的日期。



使用 toUTCString() 将当日的日期（根据 UTC）转换为字符串。



## RegExp 对象

```javascript
var re = new RegExp("\\w+");
var re = /\w+/;
```

### RegExp 修饰符

修饰符用于执行不区分大小写和全文的搜索。

**i** - 修饰符是用来执行不区分大小写的匹配。

**g** - 修饰符是用于执行全文的搜索（而不是在找到第一个就停止查找,而是找到所有的匹配）。

```javascript
var str = "Visit RUnoob";
var patt1 = /runoob/i;
```



在字符串中不区分大小写找"runoob"



以下**标记**的文本是获得的匹配的表达式：

Visit **RUnoob**

### test()

test()方法搜索字符串指定的值，根据结果并返回真或假。

下面的示例是从字符串中搜索字符 "e" ：

```javascript
var patt1=new RegExp("e"); 
document.write(patt1.test("The best things in life are free"));
```



由于该字符串中存在字母 "e"，以上代码的输出将是：

true

当使用构造函数创造正则对象时，需要常规的字符转义规则（在前面加反斜杠 \）

```javascript
var re = new RegExp("\\w+");
```



### exec()

exec() 方法检索字符串中的指定值。返回值是被找到的值。如果没有发现匹配，则返回 null。

下面的示例是从字符串中搜索字符 "e" ：

```javascript
var patt1=new RegExp("e"); 
document.write(patt1.exec("The best things in life are free"));
```

由于该字符串中存在字母 "e"，以上代码的输出将是：e



# 浏览器BOM

## Window 尺寸

有三种方法能够确定浏览器窗口的尺寸。

- window.innerHeight - 浏览器窗口的内部高度(包括滚动条)
- window.innerWidth - 浏览器窗口的内部宽度(包括滚动条)

## Window Screen

**window.screen**对象在编写时可以不使用 window 这个前缀。

一些属性：

- screen.availWidth - 可用的屏幕宽度
- screen.availHeight - 可用的屏幕高度

## Window Location

**window.location** 对象在编写时可不使用 window 这个前缀。 一些例子：

一些实例:

- location.hostname 返回 web 主机的域名
- location.pathname 返回当前页面的路径和文件名
- location.port 返回 web 主机的端口 （80 或 443）
- location.protocol 返回所使用的 web 协议（http: 或 https:）



location.href 属性返回当前页面的 URL。



location.pathname 属性返回 URL 的路径名。



location.assign() 方法加载新的文档。

## Window History

**window.history**对象在编写时可不使用 window 这个前缀。

为了保护用户隐私，对 JavaScript 访问该对象的方法做出了限制。

一些方法：

- history.back() - 与在浏览器点击后退按钮相同
- history.forward() - 与在浏览器中点击向前按钮相同



## Window Navigator

```javascript
<div id="example"></div>
<script>
txt = "<p>浏览器代号: " + navigator.appCodeName + "</p>";
txt+= "<p>浏览器名称: " + navigator.appName + "</p>";
txt+= "<p>浏览器版本: " + navigator.appVersion + "</p>";
txt+= "<p>启用Cookies: " + navigator.cookieEnabled + "</p>";
txt+= "<p>硬件平台: " + navigator.platform + "</p>";
txt+= "<p>用户代理: " + navigator.userAgent + "</p>";
txt+= "<p>用户代理语言: " + navigator.systemLanguage + "</p>";
document.getElementById("example").innerHTML=txt;
</script>
```

## JavaScript 弹窗

可以在 JavaScript 中创建三种消息框：警告框、确认框、提示框。

### 警告框

警告框经常用于确保用户可以得到某些信息。

当警告框出现后，用户需要点击确定按钮才能继续进行操作。

##### **语法**

window.alert("*sometext*");

**window.alert()** 方法可以不带上window对象，直接使用**alert()**方法。



### 确认框

确认框通常用于验证是否接受用户操作。

当确认卡弹出时，用户可以点击 "确认" 或者 "取消" 来确定用户操作。

当你点击 "确认", 确认框返回 true， 如果点击 "取消", 确认框返回 false。

##### **语法**

window.confirm("*sometext*");

**window.confirm()** 方法可以不带上window对象，直接使用**confirm()**方法。

```javascript
var r=confirm("按下按钮");
if (r==true)
{
  x="你按下了\"确定\"按钮!";
}
else
{
  x="你按下了\"取消\"按钮!";
}
```



### 提示框

提示框经常用于提示用户在进入页面前输入某个值。

当提示框出现后，用户需要输入某个值，然后点击确认或取消按钮才能继续操纵。

如果用户点击确认，那么返回值为输入的值。如果用户点击取消，那么返回值为 null。

##### **语法**

window.prompt("*sometext*","*defaultvalue*");

**window.prompt()** 方法可以不带上window对象，直接使用**prompt()**方法。

## JavaScript 计时事件

通过使用 JavaScript，我们有能力做到在一个设定的时间间隔之后来执行代码，而不是在函数被调用后立即执行。我们称之为计时事件。

在 JavaScritp 中使用计时事件是很容易的，两个关键方法是:

- setInterval() - 间隔指定的毫秒数不停地执行指定的代码。

  clearInterval() 方法用于停止 setInterval() 方法执行的函数代码。



```javascript
myVar=setInterval(function(){alert("Hello")},3000);//设置


window.clearInterval(myVar);//清除
```





- setTimeout() - 在指定的毫秒数后执行指定代码。

  clearTimeout() 方法用于停止执行setTimeout()方法的函数代码。



## 什么是 Cookie？

Cookie 是一些数据, 存储于你电脑上的文本文件中。

当 web 服务器向浏览器发送 web 页面时，在连接关闭后，服务端不会记录用户的信息。

Cookie 的作用就是用于解决 "如何记录客户端的用户信息":

- 当用户访问 web 页面时，他的名字可以记录在 cookie 中。
- 在用户下一次访问该页面时，可以在 cookie 中读取用户访问记录。

Cookie 以名/值对形式存储，如下所示:

username=John Doe

当浏览器从服务器上请求 web 页面时， 属于该页面的 cookie 会被添加到该请求中。服务端通过这种方式来获取用户的信息。

------

### 使用 JavaScript 创建Cookie

JavaScript 可以使用 **document.cookie** 属性来创建 、读取、及删除 cookie。

JavaScript 中，创建 cookie 如下所示：

`document.cookie="username=John Doe";`

您还可以为 cookie 添加一个过期时间（以 UTC 或 GMT 时间）。默认情况下，cookie 在浏览器关闭时删除：

`document.cookie="username=John Doe;`

` expires=Thu, 18 Dec 2043 12:00:00 GMT";`

您可以使用 path 参数告诉浏览器 cookie 的路径。默认情况下，cookie 属于当前页面。

document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";

------

### 使用 JavaScript 读取 Cookie

在 JavaScript 中, 可以使用以下代码来读取 cookie：

var x = document.cookie;



| ![Note](https://www.runoob.com/images/lamp.jpg) | document.cookie 将以字符串的方式返回所有的 cookie，类型格式： cookie1=value; cookie2=value; cookie3=value; |
| ----------------------------------------------- | ------------------------------------------------------------ |
|                                                 |                                                              |



------

### 使用 JavaScript 修改 Cookie

在 JavaScript 中，修改 cookie 类似于创建 cookie，如下所示：

document.cookie="username=John Smith; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";

旧的 cookie 将被覆盖。

------

### 使用 JavaScript 删除 Cookie

删除 cookie 非常简单。您只需要设置 expires 参数为以前的时间即可，如下所示，设置为 Thu, 01 Jan 1970 00:00:00 GMT:

document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT";

注意，当您删除时不必指定 cookie 的值。

------

### Cookie 字符串

document.cookie 属性看起来像一个普通的文本字符串，其实它不是。

即使您在 document.cookie 中写入一个完整的 cookie 字符串, 当您重新读取该 cookie 信息时，cookie 信息是以名/值对的形式展示的。

如果您设置了新的 cookie，旧的 cookie 不会被覆盖。 新 cookie 将添加到 document.cookie 中，所以如果您重新读取document.cookie，您将获得如下所示的数据：

cookie1=value; cookie2=value;



如果您需要查找一个指定 cookie 值，您必须创建一个JavaScript 函数在 cookie 字符串中查找 cookie 值。

------

### JavaScript Cookie 实例

在以下实例中，我们将创建 cookie 来存储访问者名称。

首先，访问者访问 web 页面, 他将被要求填写自己的名字。该名字会存储在 cookie 中。

访问者下一次访问页面时，他会看到一个欢迎的消息。

在这个实例中我们会创建 3 个 JavaScript 函数:

1. 设置 cookie 值的函数
2. 获取 cookie 值的函数
3. 检测 cookie 值的函数

------

### 设置 cookie 值的函数

首先，我们创建一个函数用于存储访问者的名字：

![image-20200428165502300](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200428165502300.png)

**函数解析：**

以上的函数参数中，cookie 的名称为 cname，cookie 的值为 cvalue，并设置了 cookie 的过期时间 expires。

该函数设置了 cookie 名、cookie 值、cookie过期时间。

------

### 获取 cookie 值的函数

然后，我们创建一个函数用户返回指定 cookie 的值：

![image-20200428165443294](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200428165443294.png)

**函数解析：**

cookie 名的参数为 cname。

创建一个文本变量用于检索指定 cookie :cname + "="。

使用分号来分割 document.cookie 字符串，并将分割后的字符串数组赋值给 ca (ca = document.cookie.split(';'))。

循环 ca 数组 (i=0;i<ca.length;i++)，然后读取数组中的每个值，并去除前后空格 (c=ca[i].trim())。

如果找到 cookie(c.indexOf(name) == 0)，返回 cookie 的值 (c.substring(name.length,c.length)。

如果没有找到 cookie, 返回 ""。

------

### 检测 cookie 值的函数

最后，我们可以创建一个检测 cookie 是否创建的函数。

如果设置了 cookie，将显示一个问候信息。

如果没有设置 cookie，将会显示一个弹窗用于询问访问者的名字，并调用 setCookie 函数将访问者的名字存储 365 天：

![image-20200428165337973](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200428165337973.png)

### 实例

![image-20200428165406794](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200428165406794.png)







