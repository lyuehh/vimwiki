
## 层叠的重要度

1. 标为!important的用户样式
2. 标为!important的作者样式
3. 作者样式
4. 用户样式
5. 浏览器/用户代理应用的样式

## CSS选择器的特殊性计算
选择器的特殊性分为四个成分等级，a, b, c, d

1. 如果是行内样式, a = 1
2. b = ID选择器的总数
3. c = 类，伪类，属性选择器的总数
4. d = 类型选择器和伪元素选择器的总数

可以简单解释如下：

1. style属性总比其他属性特殊
2. 有ID的比没ID的特殊
3. 有class的比没class的特殊
4. 如果两个规则特殊性相同，后定义的规则优先

## css hack

```
一、Chrome浏览器

选择器Hack

/* Chrome 24- and Safari 5- */
::made-up-pseudo-element, .selector {
  代码放在这里
}


媒体查询Hacks

/* Chrome, Safari 3+ */
@media screen and (-webkit-min-device-pixel-ratio:0) {
  代码放在这里
}


JavaScript Hack

/* Chrome */
var isChrome = Boolean(window.chrome);


二、Firefox浏览器

属性选择器Hack

/* Firefox 1.5 */
body:empty .selector {
样式代码放这里
}
/* Firefox 2+ */
.selector, x:-moz-any-link {
样式代码放这里
}
/* Firefox 3+ */
.selector, x:-moz-any-link; x:default {
样式代码放这里
}
/* Firefox 3.5+ */
body:not(:-moz-handler-blocked) .selector {
样式代码放这里
}


媒体查询Hack

/* Firefox 3.5+, IE 9/10, Opera */
@media screen and (min-resolution: +72dpi) {
样式代码放这里
}
/* Firefox 3.6+ */
@media screen and (-moz-images-in-menus:0) {
样式代码放这里
}
/* Firefox 4+ */
@media screen and (min--moz-device-pixel-ratio:0) {
样式代码放这里
}


JavaScript Hack

/* Firefox */
var isFF = !!navigator.userAgent.match(/firefox/i);

/* Firefox 2 - 13 */
var isFF = Boolean(window.globalStorage);

/* Firefox 2/3 */
var isFF = /a/[-1]=='a';

/* Firefox 3 */
var isFF = (function x(){})[-5]=='x';


混合型Hack

/* Firefox 3+ */
@-moz-document url-prefix() {
样式代码放这里
}


三、Opera浏览器

属性选择器Hack

/* Opera 9.25, Safari 2/3.1 */
*|html[xmlns*=""] .selector {
样式代码放这里
}

/* Opera 9.27 and below, Safari 2 */
html:first-child .selector {
样式代码放这里
}

/* Opera 9.5+ */
noindex:-o-prefocus, .selector {
样式代码放这里
}


媒体查询Hack

/* Opera 7 */
@media all and (min-width: 0px){
样式代码放这里
}

/* Opera 12- */
@media all and (-webkit-min-device-pixel-ratio:10000), not all and (-webkit-min-device-pixel-ratio:0) {
样式代码放这里
}

/* Opera, Firefox 3.5+, IE 9/10 */
@media screen and (min-resolution: +72dpi) {
样式代码放这里
}

/* Opera, IE 8/9/10 */
@media screen {
样式代码放这里
}


JavaScript Hack

/* Opera 9.64- */
var isOpera = /^function \(/.test([].sort);

/* Opera 12- */
var isOpera = Boolean(window.opera);


四、Safari浏览器

属性选择器Hack

/* Safari 2/3 */
html[xmlns*=""] body:last-child .selector {
样式代码放这里
}
html[xmlns*=""]:root .selector  {
样式代码放这里
}

/* Safari 2/3.1, Opera 9.25 */
*|html[xmlns*=""] .selector {
样式代码放这里
}

/* Safari 5- and Chrome 24- */
::made-up-pseudo-element, .selector {
样式代码放这里
}


媒体查询Hack

/* Safari */
var isSafari = /a/.__proto__=='//';


五、IE浏览器

选择器Hack

/* IE 6 and below */
* html .selector  {
样式代码放这里
}
.suckyie6.selector {
样式代码放这里
} /* .suckyie6 can be any unused class */

/* IE 7 and below */
.selector, {
样式代码放这里
}

/* IE 7 */
*:first-child+html .selector {
  样式代码放这里
}
.selector, x:-IE7 {
样式代码放这里
}
*+html .selector {
样式代码放这里
}

/* Everything but IE 6 */
html > body .selector {
样式代码放这里
}

/* Everything but IE 6/7 */
html > /**/ body .selector {
  样式代码放这里
}
head ~ /* */ body .selector {
样式代码放这里
}

/* Everything but IE 6/7/8 */
:root *> .selector {
样式代码放这里
}
body:last-child .selector {
样式代码放这里
}
body:nth-of-type(1) .selector {
样式代码放这里
}
body:first-of-type .selector {
样式代码放这里
}


属性/属性值 Hack

/* IE 6 */
.selector { _color: blue; }
.selector { -color: blue; }

/* IE 6/7 - any combination of these characters:
! $ & * ( ) = % + @ , . / ` [ ] # ~ ? : <  > | */
.selector { !color: blue; }
.selector { $color: blue; }
.selector { &color: blue; }
.selector { *color: blue; }
/* ... */

/* IE 6/7 - acts as an !important */
.selector { color: blue !ie; }
/* string after ! can be anything */

/* IE 8/9 */
.selector { color: blue\0/; }
/* must go at the END of all rules */

/* IE 9/10 */
.selector:nth-of-type(1n) { color: blue\9; }

/* IE 6/7/8/9/10 */
.selector { color: blue\9; }
.selector { color/*\**/: blue\9; }

/* Everything but IE 6 */
.selector { color/**/: blue; }


媒体查询Hack

/* IE 6/7 */
@media screen\9 {
样式代码放这里
}

/* IE 6/7/8 */
@media \0screen\,screen\9 {
样式代码放这里
}

/* IE 8 */
@media \0screen {
样式代码放这里
}

/* IE 8/9/10 & Opera */
@media screen\0 {
样式代码放这里
}

/* IE 9/10, Firefox 3.5+, Opera */
@media screen and (min-resolution: +72dpi) {
样式代码放这里
}

/* IE 9/10 */
@media screen and (min-width:0\0) {
样式代码放这里
}

/* IE 10+ */
@media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {
样式代码放这里
}

/* Everything but IE 6/7/8 */
@media screen and (min-width: 400px) {
样式代码放这里
}


JavaScript Hack

/* IE <= 8 */
var isIE = '\v'=='v';


/* IE 6 */
(checkIE = document.createElement("b")).innerHTML = "<!--[if IE 6]><i></i><![endif]-->";
var isIE = checkIE.getElementsByTagName("i").length == 1;


/* IE 7 */
(checkIE = document.createElement("b")).innerHTML = "<!--[if IE 7]><i></i><![endif]-->";
var isIE = checkIE.getElementsByTagName("i").length == 1;
navigator.appVersion.indexOf("MSIE 7.")!=-1


/* IE 8 */
(checkIE = document.createElement("b")).innerHTML = "<!--[if IE 8]><i></i><![endif]-->";
var isIE = checkIE.getElementsByTagName("i").length == 1;


/* IE 9 */
(checkIE = document.createElement("b")).innerHTML = "<!--[if IE 9]><i></i><![endif]-->";
var isIE = checkIE.getElementsByTagName("i").length == 1;


/* IE 10 */
var isIE = eval("/*@cc_on!@*/false") && document.documentMode === 10;

/* IE 10 */
var isIE = document.body.style.msTouchAction != undefined;


上面列出各个浏览器下hack的写法，当然在实际运用之中并不建议使用hack。如果你的页面需要hack来处理时，请先检查你的css或者js，如果实在无法达到要求，在考虑使用hack来处理。
```
