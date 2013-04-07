# mac

## mac技巧
`http://lri.me/osx.html`

## mac 锁屏快捷键
`CTRL + SHIFT + Power`

## mac退出程序,下次不自动打开
退出程序时使用option+command+q而不是command+q，相当于关闭所有文件并退出程序，下次打开时，这些文件就不会自动打开了。

## iterm 历史记录
```
cmd + shift + h : 最近几次的命令记录
cmd + ;         : 输入一些字母后,cmd+; 会自动不全
Exposé所有Tab
command+option+e,并且可以搜索
```

## 查看占用mac 端口的程序
```
netstat -anp tcp | grep 3000
lsof -i tcp:3000
lsof -P | grep ':3000'
```

## 导出用户头像图片
`dscl . -read /Users/weiwei JPEGPhoto | tail -1 | xxd -r -p > ~/aaa.jpg`

## tidy命令
`tidy`命令用来校验, 矫正, 格式化XML和HTML文件.

## uniq命令
`uniq` 命令只处理连续重复的行
`uniq -d` 去除重复的行(只显示重复的行..)
`uniq -u` 去除重复的行(只显示不重复的行..)
`sort -u` 去除重复的行,不管连不连续


## tab转空格命令
expand 将tab转化为空格
unexpand 将空格转化为tab

## 列出pkg包包含的文件
```
pkgutil --pkgs
pkgutil --files com.amazon.SendToKindleMacInstaller.pkg
plutil -p  /private/var/db/receipts/支付宝安全控件.pkg.plist
```

## virtualvox 克隆虚拟磁盘
`VBoxManage.exe clonehd "F:\VirtualBox\XP\win_xp.vdi" "F:\xp.vmdk " -format VMDK`

## 开启4指双击切换space功能
`defaults write com.apple.dock double-tap-jump-back -bool TRUE`

## mysql Error loading MySQLdb module: dlopen 错误

```
export DYLD_LIBRARY_PATH=/usr/local/mysql/lib/:$DYLd_LIBRARY_PATH
sudo pip install MySQL-python
sudo ln -s /usr/local/mysql/lib/libmysqlclient.18.dylib /usr/lib/libmysqlclient.18.dylib
sudo ln -s /usr/local/mysql/lib /usr/local/mysql/lib/mysql
```

## 移除 Console 中的 launchd.peruser.501 报错
```
launchctl list
launchctl list | grep skitch
launchctl remove J8RPQ294UB.com.skitch.SkitchHelper
```
## 显示~/Library文件夹
`chflags nohidden ~/library/`

## 危险!慎用
````
sudo ruby -e 'key = [125, 137, 82, 35, 210, 188, 221, 234, 163, 185, 31]; IO.read("/etc/kcpassword").bytes.each_with_index { |b, i| break if key.include?(b); print [b ^ key[i % key.size]].pack("U*") }'
```

## 命令行播放MP3文件
`afplay aaa.mp3`




