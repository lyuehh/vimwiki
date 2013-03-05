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

