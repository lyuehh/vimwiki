# shell tips

## 文件是否存在
`[[ -f ~/.ssh/id_rsa.pub ]] || ssh-keygen -t rsa`

## 复制文本
`[[ -f ~/.ssh/id_rsa.pub ]] && cat ~/.ssh/id_rsa.pub | pbcopy ;# only on mac`


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
