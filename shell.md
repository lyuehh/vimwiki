## Shell

### ab测试
`ab -q -c 50 -n 1000 http://www.qq.com`

### awk split
`awk '{split($0,a,"/")`

### zmv
`zmv -W '*.cgi' '*.jpg'`
`zmv *.txt.xml *.xml`

### sed 替换chrome书签
`sed 's/ICON=.*"/ICON=""/g' bookmarks_13-9-13.html > bookmark.html`

### convert 水平方向拼接图片
`convert +append 1.jpg 2.jpg 3.jpg .... 0.jpg`

### convert 垂直方向拼接图片
`convert -append 1.jpg 2.jpg 3.jpg .... 0.jpg`

### zsh tips

```
ll -l **/README
chmod 700 **/(.) # Only files
chmod 700 **/(/) # Only directories
ls -l **/*.(js|css)
```

### shell 技巧
<http://lri.me/shell.txt>

### bash, ksh, zsh语法比较
<http://hyperpolyglot.org/unix-shells#group-cmd>

### 文件是否存在
`[[ -f ~/.ssh/id_rsa.pub ]] || ssh-keygen -t rsa`

### 复制文本
`[[ -f ~/.ssh/id_rsa.pub ]] && cat ~/.ssh/id_rsa.pub | pbcopy ;# only on mac`

### 参数相关

```
$1 第1个参数
$2 第2个参数
...
$? 最后一条命令的结果
$# 参数的个数
$@ 所有的参数列表
```


### install ruby on ubuntu

```
sudo vi /etc/apt/source.list
:%s/us/cn/g

sudo apt-get update
sudo apt-get install git-core
sudo apt-get install curl
sudo apt-get install build-essential zlib1g zlib1g-dev libreadline5 libreadline5-dev libssl-dev
curl -L https://get.rvm.io | bash -s stable
source /home/vagrant/.rvm/scripts/rvm
rvm install 1.9.3
sudo apt-get install zsh

git clone https://github.com/skwp/dotfiles ~/.yadr
cd ~/.yadr && rake install

chsh -s /bin/zsh
password: vagrant
```

### 创建目录树
`mkdir -p project/{lib/ext,bin,src,doc/{html,info,pdf},demo/stat/a}`
会在project下创建如下的目录树

```
├── bin
├── demo
│   └── stat
│       └── a
├── doc
│   ├── html
│   ├── info
│   └── pdf
├── lib
│   └── ext
└── src
```

### 使用-C命令解压文件
`tar xvf -C tmp/a/b/c newarc.tar.gz`

### 仅当另一个命令返回零退出状态时才运行某个命令
`cd tmp/a/b/c && tar xvf ~/archive.tar`

### 仅当另一个命令返回非零退出状态时才运行某个命令
`cd tmp/a/b/c || mkdir -p tmp/a/b/c`

### 将命令与控制操作符组合使用
`cd tmp/a/b/c || mkdir -p tmp/a/b/c && tar xvf -C tmp/a/b/c ~/archive.tar`

###  在子shell执行命令, 在当前shell执行命令

```
# 在子shell执行命令
(cd ~/bin; ll)
# 在当前shell执行命令
{ cd ~/bin; ll }
```

###  使用git clone googlecode项目
`git svn clone http://ccons.googlecode.com/svn -T trunk -b branches -t tags`
将`ccons`替换为其他项目名称即可

### awk if判断

```
ret=`echo $1 | awk '{if(index($1,".")==0) {print 0;} else {print 1;}}'`
```

### shell 算数运算

```
expr 3 + 2   # 中间必须要有空格
expr 3 \* 20 # *号必须转义
expr 1.2 + 2.2 # error expr只能计算整数

echo (( 3 + 2 ))
echo (( 3+2 ))
echo ((3+2))
以上3种方式均可
```

### awk 语法

```
if (expression) statement [ else statement ]
while (expression) statement
for (expression; expression; expression) statement
for (var in array) statement
do statement while (expression)
break
continue
{ [ statement ... ] }
expression
print [ expression-list ] [ > expression ]
printf format [ , expression-list ] [ > expression ]
return [ expression ]
next
nextfile
delete array[expression]
delete array
exit [ expression ]
```

### awk 特殊变量

```
$0          当前行
$na         第n个域
FILENAME    当前文件名
NR          当前行的行号,从1开始
NF          当前行有多少个域
RS          输入记录的分隔符,默认为换行
ORS         输出记录的分隔符,默认也是换行
FS          域分隔符,默认是空格或TAB
OFS         输出域分隔符,默认是空格
```

### curl使用代理
`curl -x 127.0.0.1:8087 http://ip.taobao.com/service/getIpInfo.php\?ip\=218.195.250.123`

### wget使用代理
`wget -e "http_proxy=127.0.0.1:8087" http://www.taobao.com`

### imagemagick 批量压缩图片
`ls -1 | xargs -I {} convert -quality 20% {} ../2/{}`  
`convert favicon.png favicon.ico`

### shell算数运算
`$(( 1 + 1 ))` bash, ksh, zsh均支持  
`$(( 1.1 + 1.1 ))` 只有ksh, zsh支持

### shell 数组
bash:

```
a=(a b c)
a[0]="a"
a[1]="b"
a[2]="c"
```

zsh:

```
a=(a b c)
a[1]="a"
a[2]="b"
a[3]="c"
```

### 查看Makefile 的所有target
类似`rake -T`  
`env -i make -nRrp | grep -v '^#'`

### rot13 使用tr
`echo 'abc' | tr A-Za-z N-ZA-Mn-za-m`

### 错误重定向
`$ kill -1 1234 >killouterr.txt 2>&1`  
将标准输出重定向到文件, 将标准错误输出重定向到和标准输出相同的地方  
如果顺序有误, 不会按照预期那样工作  
`$ kill -1 1234 > /de/null 2>&1`  
抛弃所有输出

### 查看进程名字
`$ ps –xo comm | sort | uniq | more`

### here doc

```
cat <<-EOF
this is
a
test
EOF
```

### bash 快捷键
```
编辑命令

    Ctrl + a ：移到命令行首
    Ctrl + e ：移到命令行尾
    Ctrl + f ：按字符前移（右向）
    Ctrl + b ：按字符后移（左向）
    Alt + f ：按单词前移（右向）
    Alt + b ：按单词后移（左向）
    Ctrl + xx：在命令行首和光标之间移动
    Ctrl + u ：从光标处删除至命令行首
    Ctrl + k ：从光标处删除至命令行尾
    Ctrl + w ：从光标处删除至字首
    Alt + d ：从光标处删除至字尾
    Ctrl + d ：删除光标处的字符
    Ctrl + h ：删除光标前的字符
    Ctrl + y ：粘贴至光标后
    Alt + c ：从光标处更改为首字母大写的单词
    Alt + u ：从光标处更改为全部大写的单词
    Alt + l ：从光标处更改为全部小写的单词
    Ctrl + t ：交换光标处和之前的字符
    Alt + t ：交换光标处和之前的单词
    Alt + Backspace：与 Ctrl + w 类似

重新执行命令

    Ctrl + r：逆向搜索命令历史
    Ctrl + g：从历史搜索模式退出
    Ctrl + p：历史中的上一条命令
    Ctrl + n：历史中的下一条命令
    Alt + .：使用上一条命令的最后一个参数

控制命令

    Ctrl + l：清屏
    Ctrl + o：执行当前命令，并选择上一条命令
    Ctrl + s：阻止屏幕输出
    Ctrl + q：允许屏幕输出
    Ctrl + c：终止命令
    Ctrl + z：挂起命令

Bang (!) 命令

    !!：执行上一条命令
    !blah：执行最近的以 blah 开头的命令，如 !ls
    !blah:p：仅打印输出，而不执行
    !$：上一条命令的最后一个参数，与 Alt + . 相同
    !$:p：打印输出 !$ 的内容
    !*：上一条命令的所有参数
    !*:p：打印输出 !* 的内容
    ^blah：删除上一条命令中的 blah
    ^blah^foo：将上一条命令中的 blah 替换为 foo
    ^blah^foo^：将上一条命令中所有的 blah 都替换为 foo
```
### find

如何查找在/home/work/log/路径下，修改时间在3天以前的文件，并将这些文件mv到/home/work/log/backup下？

```
find  /home/work/log/  -type f -mtime -3 -exec mv {}  /home/work/log/backup   \;
```

### 随机数

`seq -f %.0f 1 100 | gshuf > data2`

## mysql
`cd /usr/local/var`
`chown -R weiwei mysql55`