# web

## 性能测试
```
- Ab
  ab -c 12 -n 20000 localhost/market.htm
– Httpload
  http_load -rate 300 -seconds 120 item-urls
  http_load -parallel 40 -seconds 120 item-urls
```

## reflow
```
当 DOM 元素的属性发生变化 (如 color) 时, 浏览器会通知 render 重新描绘相应的元素, 此过程称为 repaint。
如果该次变化涉及元素布局 (如 width), 浏览器则抛弃原有属性, 重新计算并把结果传递给 render 以重新描绘页面元素, 此过程称为 reflow。
```

## style
```
style只能获取元素的内联样式，内部样式和外部样式使用style是获取不到的。
currentStyle可以弥补style的不足，但是只适用于IE。
getComputedStyle同currentStyle作用相同，但是适用于FF、opera、safari、chrome。
```