# vim tips

## NERD tree 快捷键

o 在当前tab打开
t 在新tab打开
T 在新tab后台打开

p 切换到parrent
P 切换到root
C 已当前选择文件夹为root
u 将root切换为此文件夹的parent 文件夹
R 刷新root下所有文件夹
cd 将pwd切换到所选文件夹
I 是否显示隐藏文件

## 替换^M
:%s/^M//g 将全部的^M替换成空
需要用ctrl+v 接下来ctrl+m 输入^M

## visual mode下替换文本
先使用`v`,或者`V`,或者`Ctrl+v`选择文本,
然后按`:`,然后输入`s/xxx/yyy/g`即可,
最后的`g`表示替换所有匹配,如果去掉则表示只替换第1次匹配

## 屏幕左右滚动
`zh, zl, zH, zL`
