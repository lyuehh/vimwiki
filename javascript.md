# javascript tips

## 常用类库
* modernizr

## jquery json的参数

* `dataType` 参数需要设置为`jsonp`
* jQuery默认生成的url为`?callback=jQuery191xxx`
* `jsonp` 参数设置为url里参数的key
* 比如`jsonp: aa`会生成 `?aa=jQuery191xxx`
* 如果设置为`jsonp: false`,则jquery不会在url里添加`?callback=jQuery191xxx`,你可能需要添加`jsonpCallback`参数
* `jsonpCallback` 参数设置url里参数的value
* 比如`jsonpCallback: bb` 会生成`?callback=bb`
* 以上2个参数需要根据服务器的要求修改,有些服务器返回的格式不是标准的`bb({})`的形式,就不能用jquery封装后的jsonp请求,
* 比如服务端返回`bb && bb({})`, jquery就不能正确处理,这时就需要自己手工写jsonp请求.

## map 和 parseInt
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

## jQuery的$用法
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

## window.open 的参数
`window.open('http://www.qq.com','aa','height=400,width=400,location=no,resizable=no,menubar=no,scrollbars=no,status=no,toolbar=no,fullscreen=no,top=300,left=300')`

## https下资源加载
https下加载http的资源时,浏览器一般都会有提示,或者会默认阻止,
只要是https资源加载就没问题, 不管是不是本域的.

## jQuery 2.0
```
<!--[if lt IE 9]>
    <script src="jquery-1.9.1.js"></script>
<![endif]-->
<!--[if gte IE 9]><!-->
    <script src="jquery-2.0.0b2.js"></script>
<!--<![endif]-->
```

## csrf
1. 第三方页面使用form 会附带cookie，可以提交成功，但是拿不到post的响应，如果用iframe，那么iframe的domain是厂商的，没有权限访问到其中的内容
2. 如果使用ajax发送post请求，浏览器不会附带cookie，不会通过后台的认证
3. get请求的响应和post响应 只有受害者能看到，而攻击者看不到，get如果不更改后台的状态，可以不认证，post都要认证

## why use apply
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

## substr和substring和slice的区别
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

## + -
```
1 + '1' -> "11"
1 - '1' -> 0
01 + '01' -> '101'
010 + '010' -> "8010" // 0开头的是八进制
Number.MAX_VALUE -> 1.7976931348623157e+308
Number.MIN_VALUE -> 5e-324
```

## underscore include ,  indexOf
underscore的include和indexOf都是给数组用的, 不是给字符串用的
需要判断是否包含字符串, 需要使用str.indexOf

## js关闭窗口
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

## Event
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

## 格式化json
`curl -s 'http://geci.me/api/lyric/part of me' | python -mjson.tool`
`curl -s 'http://geci.me/api/lyric/part of me' | json_reformat`
`json_reformat`在`yajl`包中, `brew install yajl`
