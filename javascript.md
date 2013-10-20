## javascript tips

<link type="text/css" rel="stylesheet" href="http://cdn.staticfile.org/twitter-bootstrap/3.0.0/css/bootstrap-theme.min.css"/>
<link type="text/css" rel="stylesheet" href="http://cdn.staticfile.org/twitter-bootstrap/3.0.0/css/bootstrap.min.css"/>

### 常用类库

```
* modernizr
* momentjs
* bower
* https://code.google.com/p/google-code-prettify/
* gruntjs
* yo
```

### jquery json的参数

* `dataType` 参数需要设置为`jsonp`
* jQuery默认生成的url为`?callback=jQuery191xxx`
* `jsonp` 参数设置为url里参数的key
* 比如`jsonp: aa`会生成 `?aa=jQuery191xxx`
* 如果设置为`jsonp: false`,则jquery不会在url里添加`?callback=jQuery191xxx`,你可能需要添加`jsonpCallback`参数
* `jsonpCallback` 参数设置url里参数的value
* 比如`jsonpCallback: bb` 会生成`?callback=bb`
* 以上2个参数需要根据服务器的要求修改,有些服务器返回的格式不是标准的`bb({})`的形式,就不能用jquery封装后的jsonp请求,
* 比如服务端返回`bb && bb({})`, jquery就不能正确处理,这时就需要自己手工写jsonp请求.

### map 和 parseInt

```javascript
["0", "0", "0"].map(parseInt);
// -> [0, NaN, 0]
```

原因:
map方法接收的函数参数会接收到3个参数,分别为item, index, array,
分别为当前元素, 当前元素的索引, 整个array;
而parseInt方法接收2个参数, str, radix,
所以当map方法接受的参数为parseInt时,会调用
`parseInt("0", 0, ["0","0","0"]); // -> 0`
`parseInt("0", 1, ["0", "0", "0"]); // -> NaN`

### jQuery的$用法
From: http://api.jquery.com/jQuery/

```javascript
jQuery( selector [, context ] ); // 在context里选中带有selector的元素
jQuery( element ); // 将element wrap为jQuery对象
jQuery( elementArray ); // An array containing a set of DOM elements to wrap in a jQuery object.
jQuery( object ); // A plain object to wrap in a jQuery object.
jQuery( jQuery object ); // An existing jQuery object to clone.
jQuery(); // 什么都不做...
jQuery( html [, ownerDocument ] ); // A string of HTML to create on the fly. Note that this parses HTML, not XML.
jQuery( html, attributes ); // 根据attribute创建html
jQuery( callback ); // exec the callback when dom is ready
```

### window.open 的参数
`window.open('http://www.qq.com','aa','height=400,width=400,location=no,resizable=no,menubar=no,scrollbars=no,status=no,toolbar=no,fullscreen=no,top=300,left=300')`

### https下资源加载
https下加载http的资源时,浏览器一般都会有提示,或者会默认阻止,
只要是https资源加载就没问题, 不管是不是本域的.

* jQuery 2.0

```
<!--[if lt IE 9]>
    <script src="jquery-1.9.1.js"></script>
<![endif]-->
<!--[if gte IE 9]><!-->
    <script src="jquery-2.0.0b2.js"></script>
<!--<![endif]-->
```

### csrf
1. 第三方页面使用form 会附带cookie，可以提交成功，但是拿不到post的响应，如果用iframe，那么iframe的domain是厂商的，没有权限访问到其中的内容
2. 如果使用ajax发送post请求，浏览器不会附带cookie，不会通过后台的认证
3. get请求的响应和post响应 只有受害者能看到，而攻击者看不到，get如果不更改后台的状态，可以不认证，post都要认证

### why use apply

```javascript
var a = [1,2,3,4,5];
console.log(Math.max(a)); // -> NaN
console.log(Math.max.apply(null, a)); // -> 5 // This is what you want
// ---
function foo(value1, value2, value3) {
    alert("Value 1 is "+value1+".");
    alert("Value 2 is "+value2+".");
    alert("Value 3 is "+value3+".");
}
var anArray=[1, 2, 3];
foo(anArray); // This will not work. value1 will be anArray, and value 2 and 3 will be undefined.
foo.apply(this, anArray); // This works, as anArray will be the arguments to foo.
```

### substr和substring和slice的区别

```javascript
var message = "Hello world!";

message.substring(1, 4)   -> "ell"
message.substring(1)      -> "ello world"
message.substring(1, -4)  -> "H"
message.substring(-1)     -> "Hello world"
message.substring(-1,-4)  -> ""

message.substr(1,4)      -> "ello"
message.substr(1)        -> "ello world"
message.substr(1, -4)    -> ""
message.substr(-1)       -> "d"
message.substr(-1,-4)    -> ""

message.slice(1,4)       -> "ell"
message.slice(1)         -> "ello world"
message.slice(1, -4)     -> "ello w"
message.slice(-1)        -> "d"
message.slice(-1,-4)     -> ""

string.substring(indexA[, indexB])
string.substr(start[, length])
string.slice(beginslice[, endSlice])

substring和substr的区别
substring不包含indexB,substr包含indexB
substr的第1个参数可以是负的,substring的参数不能为负的
```

### + -

```
1 + '1' -> "11"
1 - '1' -> 0
01 + '01' -> '101'
010 + '010' -> "8010" // 0开头的是八进制
Number.MAX_VALUE -> 1.7976931348623157e+308
Number.MIN_VALUE -> 5e-324
```

### underscore include ,  indexOf
underscore的include和indexOf都是给数组用的, 不是给字符串用的
需要判断是否包含字符串, 需要使用str.indexOf

### js关闭窗口

```html
<script type="text/javascript">
function CloseWebPage() {
  if (navigator.userAgent.indexOf("MSIE") > 0) {
    if (navigator.userAgent.indexOf("MSIE 6.0") > 0) {
      window.opener = null; window.close();
    }
    else {
      window.open('', '_top'); window.top.close();
    }
  }
  else if (navigator.userAgent.indexOf("Firefox") > 0) {
    window.location.href = 'about:blank '; //火狐默认状态非window.open的页面window.close是无效的
    //window.history.go(-2);
  }
  else {
    window.opener = null;
    window.open('', '_self', '');
    window.close();
  }
}
</script>
```

### Event

1. currentTarget 等于this, 是绑定事件的对象, 而target则是事件真正的目标
2. IE取消默认行为, returnValue = false, 相当于其他浏览器的 preventDefault()方法
3. IE阻止事件冒泡, calcelBubble = true, 相当于其他浏览器的stopPropagation()方法
4. mousewheel事件, wheelDelta的值为负, 表示向下滚动 -> 正常浏览器
  DOMMouseScroll事件, detail的值为正表示向下滚动 -> 火狐
5. beforeunload事件, 提示用户的信息, ie和火狐中放在 event.returnValue中,safari和chrome
  中作为函数的返回值返回
6. DOMContentLoaded事件, 在DOM树形成之后触发, 而不管图像js,css等其他资源.IE8以及以前的
  版本不支持此事件
7. readystatechange事件, 很不稳定, 一般监听readystatechange事件,然后判断
  document.readyState,为interactive时表示DOM树加载完毕,IE,firefox 4+, opera支持此事件
8. 除非把动态的元素添加到页面中,否则浏览器不会开始下载外部资源.

### 格式化json
`curl -s 'http://geci.me/api/lyric/part of me' | python -mjson.tool`
`curl -s 'http://geci.me/api/lyric/part of me' | json_reformat`
`json_reformat`在`yajl`包中, `brew install yajl`



<hr />

### 数据类型

Undefined, Null, Boolean, String, Number, Object

### undefined

```javascript
var a;
alert(a); // "undefined"
alert(b); // error

alert(typeof a); // "undefined"
alert(typeof b); // "undefined"
```

### Number

```javascript
var a1 = 070; // 八进制的70等于十进制的56
var a2 = 079; // 无效的八进制，解析为十进制的79
// 进行算数计算时，八进制和十进制都被转换成十进制数值
```
* 默认情况下, 小数点后带有6个0以上的浮点数值转换为科学技术法表示的形式
* 5e-324 < n < 1.79…e+308
* 超出这个范围的负数为 -Infinity, 正数为 Infinity

### NaN

* NaN表示非数值
* NaN参与的操作，都会返回NaN
* isNaN(x)，如果x不能被转换为数值， 返回true，(10, "10", true)都返回false，(NaN, "asdf")返回true
* isNan(x), 如果x是object，则先调用x.valueOf(), 然后根据测试返回值，如果不能，调用x.toString()，测试返回值

### Number(x)

* Boolean true 1, false 0
* 数字 直接返回
* null 0
* undefined NaN
* 字符串, 只包含数字; 包含有效的浮点数; 包含有效的十六进制; 空字符串; 其他的
* 对象 valueOf(), toString()

### parseInt(x, base)

* 忽略空格，然后找到第1个非空格字符，如果不是数字或负号，返回NaN
* 转换数字字符
* 直到遇到非数字字符
* 一般设置base为10
* 会识别八进制，和十六进制, parseInt('070');// 56 in ECMAScript, 70 in ECMAScript

### parseFloat(x)

* 第1个小数点是有效的
* 十六进制字符串会被转换为0
* 会忽略前导的0

### String

* \xnn 以十六进制代码nn表示一个字符
* \unnnn 已十六进制nnnn表示一个字符
* toString(2), toString(10)
* null和undefined没有 toString()方法
* 如果x可能是null或undefined, 可以使用 String(x)，null -> 'null', undefined -> 'undefined'

### 操作符

* 一元操作符，++, --
* 一元加减操作符，+, -
* 位操作符，-18.toString(2); -> -10010

### 位操作符

* 非, ~, ~25 = -26, 操作数的负值 - 1
* 与, &, 25&3 = 1, 11为1,其他为0
* 或, |, 25|3 = 17, 有1为1, 其他为0
* 异或, ^, 25^3 = 26, 不同为1,相同为0
* 左移, <<, 2<<5 = 64, 不影响符号位
* 右移, >>, 64>>5 = 2, 不影响符号位
* 无符号右移, >>>, -64>>>5 = 134217726, 影响符号位
* 没有无符号左移

### 逻辑非

* !x
* !object -> false
* !"" -> true
* !"asdf" -> false
* !0 -> true
* !12 -> false
* !Infinity -> false
* !null -> true
* !NaN -> true
* !undefined -> true
* !!x 会返回x本身对应的布尔值,相当于 Boolean(x)

### 逻辑与

* x && y
* x是对象,返回y
* y是对象,则当x是true是才会返回此对象
* x,y都是对象,返回y
* 有1个是null,返回null
* 有1个是NaN,返回NaN
* 有1个是undefined,返回undefined
* 短路,如果x是false,则不会计算y

### 逻辑或

* x || y
* x是对象,返回x
* x求值结果为false,返回y
* x,y均为对象,返回x
* x,y都是null,返回null
* x,y都是naN,返回NaN
* x,y都是undefined,返回undefined
* 短路,x求值为true,则不会计算y

### 乘法 *

* x * y
* x,y都是数字,按照正常的计算,如果结果超过表示范围,则返回Infinity或-Infinity
* 如果有1个是NaN,返回NaN
* Infinity * 0 = NaN
* Infinity 乘以 非0,结果是Infinity或-Infinity,取决于另一个数的符号
* 如果有1个不是数字,则调用 Number(x),转换为数字

### 除法 /

* x / y
* x,y都是数字,按照正常的计算,如果结果超过表示范围,则返回Infinity或-Infinity
* 如果有1个是NaN,返回NaN
* Infinity / Infinity = NaN
* 0 / 0 = NaN
* 如果非0的有限数被0除,结果为Infinity或-Infinity,取决于那个数的符号
* 如果Infinity被任何非0数除,结果为Infinity或-Infinity,取决于那个数的符号
* 如果有1个不是数字,则调用 Number(x),转换为数字

### 求模 %

* x % y
* x,y都是数字,按照正常的计算,返回余数
* 如果被除数是无穷大值,而除数是有限大值,结果是NaN
* 如果被除数是有限大值,而除数是0,则结果是NaN
* 如果是Infinity 被 Infinity除,结果是NaN
* 如果被除数是有限大值,而除数是无穷大值,结果是被除数 ? 23 % Infinity = 0
* 如果被除数是0,结果是0
* 如果有1个不是数字,则调用 Number(x),转换为数字

### 加法 +

* x + y
* 有1个是NaN,返回NaN
* Infinity + Infinity = Infinity
* -Infinity + -Infinity = -Infinity
* Infinity + -Infinity = NaN
* +0 + +0 = +0
* -0 + -0 = -0
* +0 + -0  = +0
* 如果2个都是字符串, 则拼起来
* 如果只有1个是字符串,则将另一个转换为字符串,然后拼起来
* 如果有1个是对象,数值后者布尔,则调用他们的toString(),取得相应的字符串,然后应用前面的规则
* null和undefined会调用String()方法得到'null'和'undefined'

### 减法 -

* x - y
* 有1个是NaN,返回NaN
* Infinity - Infinity = NaN
* -Infinity - -Infinity = NaN
* Infinity - -Infinity = Infinity
* -Infinity - Infinity = -Infinity
* +0 - +0 = +0
* +0 - -0 = -0
* -0 - -0 = +0
* 如果有1个是字符串,布尔,null或undefined,则调用Number(x),转换为数值,然后在计算,如果转换得到NaN,则结果是NaN
* 如果有1个是对象,则调用valueOf(x),已取得数值,如果得到NaN,结果就是NaN,如果没有valueOf方法,则调用toString()方法,并将得到的字符串转化为数值

### 关系操作符 <, >, <=, >=

* 如果都是数字，则执行数字比较
* 如果都是字符串，比较字符串对应的字符编码值
* 如果1个是数字，则把另一个转化为数字，然后执行比较
* 如果1个是对象，则调用valueOf()方法，用得到的结果比较，如果没有valueOf()方法，则调用toString()方法，然后用得到的结果比较
* 如果有1个是布尔值，则先转换为数值，然后比较
* NaN参与比较，结果都是false
* null > 0; //false
* null >= 0; // true

### 相等操作符 ==,!=

* 如果有1个是布尔，则先转换为数值，true为1，false为0
* 如果1个是字符串，另一个是数值，则先将字符串转换为数字
* 如果1个是对象，另一个不是，则调用valueOf()，转化为基本类型然后再比较
* null和undefined是相等的
* 比较前，不能将null和undefined转化为其他值
* 如果1个是NaN,则判断相等时返回false，判断不相等时返回true，如果2个都是NaN，判断相等时也返回false
* 如果都是对象，则判断是不是同一对象，如果都指向同一对象，则相等，否则不相等

### 全等操作符 ===， !==

* 不进行转换，直接比较