# javascript tips

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
