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
