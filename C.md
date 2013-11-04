## C

### GDB表示基本语法 

```
list l 显示源代码
l 15
l main
l - 上10行

run r 运行

break b 设置断点
b main
b 15

continue c 继续运行

next n 执行当前行，如果是函数，则作为整理执行完毕

step s 执行当前行，如果是函数，则进入函数

enter 回车 再次执行上一条命令

until u 让程序运行到指定位置
u 9 执行到第9行
u doit 执行到doit函数的开头位置

print p 打印变量的值

info locals i lo 显示所有的局部变量

display disp 
info display info disp 

clear cl 删除断点

b 11 在11行设置断点，假设编号为2
cond 2 i==5 该断点仅在i等于5时有效

watch a wa a 在修改变量a时停下来
awatch a 在变量a读写时都会停下来
rwatch a 在变量a读取时停下来
```