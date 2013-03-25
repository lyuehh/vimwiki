# shell tips

# bash, ksh, zsh语法比较
<http://hyperpolyglot.org/unix-shells#group-cmd>

## 文件是否存在
`[[ -f ~/.ssh/id_rsa.pub ]] || ssh-keygen -t rsa`

## 复制文本
`[[ -f ~/.ssh/id_rsa.pub ]] && cat ~/.ssh/id_rsa.pub | pbcopy ;# only on mac`

## 参数相关
```
$1 第1个参数
$2 第2个参数
...
$? 最后一条命令的结果
$# 参数的个数
$@ 所有的参数列表
```
## install ruby on ubuntu
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

## 创建目录树
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

## 使用-C命令解压文件
`tar xvf -C tmp/a/b/c newarc.tar.gz`

## 仅当另一个命令返回零退出状态时才运行某个命令
`cd tmp/a/b/c && tar xvf ~/archive.tar`

## 仅当另一个命令返回非零退出状态时才运行某个命令
`cd tmp/a/b/c || mkdir -p tmp/a/b/c`

## 将命令与控制操作符组合使用
`cd tmp/a/b/c || mkdir -p tmp/a/b/c && tar xvf -C tmp/a/b/c ~/archive.tar`

##  在子shell执行命令, 在当前shell执行命令
```
# 在子shell执行命令
(cd ~/bin; ll)
# 在当前shell执行命令
{ cd ~/bin; ll }
```

##  使用git clone googlecode项目
`git svn clone http://ccons.googlecode.com/svn -T trunk -b branches -t tags`
将`ccons`替换为其他项目名称即可

## awk if判断
```
ret=`echo $1 | awk '{if(index($1,".")==0) {print 0;} else {print 1;}}'`
```

## shell 算数运算
```
expr 3 + 2   # 中间必须要有空格
expr 3 \* 20 # *号必须转义
expr 1.2 + 2.2 # error expr只能计算整数

echo (( 3 + 2 ))
echo (( 3+2 ))
echo ((3+2))
# 以上3种方式均可
```

## awk 语法
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
## awk 特殊变量
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

## curl使用代理
curl -x 127.0.0.1:8087 http://ip.taobao.com/service/getIpInfo.php\?ip\=218.195.250.123

## wget使用代理
wget -e "http_proxy=127.0.0.1:8087" http://www.taobao.com

## imagemagick 批量压缩图片
`ls -1 | xargs -I {} convert -quality 20% {} ../2/{}`
