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

## surround
<https://github.com/tpope/vim-surround>
```
   Old text               Command     New text ~
  "Hello *world!"           ds"         Hello world!
  [123+4*56]/2              cs])        (123+456)/2
  "Look ma, I'm *HTML!"     cs"<q>      <q>Look ma, I'm HTML!</q>
  if *x>3 {                 ysW(        if ( x>3 ) {
  my $str = *whee!;         vllllS'     my $str = 'whee!';
```

## Tabularize
<https://github.com/godlygeek/tabular>
```
;Hit Cmd-Shift-A then type a character you want to align by
nmap <D-A> :Tabularize /
vmap <D-A> :Tabularize /
```
```
:Tabularize /:
:Tabularize /=
:Tab /:
:Tab /:\zs
:Tab /|
```
## vundle
```
Using Vundle:

Just add this 2 lines to your ~/.vimrc:

Bundle 'rizzatti/funcoo.vim'
Bundle 'rizzatti/dash.vim'
And run :BundleInstall inside Vim.
```
## 删除选中行中符合正则的行
首先使用`v` 后者`V` 进入选择模式, 然后使用`j` `k` 选中行,然后按`:`, 然后输入命令:
`g/\.$/d` 即可删除选中行中最后一个字符为`.`的行
