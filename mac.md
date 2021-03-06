## Mac

### rtf to html
`textutil -convert html foo.rtf`

### zip
`zip -er xxx.zip xxx` 给压缩包加上密码

### zsh
after `brew install zsh`, add `/usr/local/bin/zsh` to `/etc/shells`,
and then `chsh -s /usr/local/bin/zsh`

### about mac

```
http://lyuehh.com/mac/2012/11/01/soft-of-mac.html
http://www.douban.com/note/290330877/
http://www.douban.com/note/290437635/
http://www.douban.com/note/291323218/
http://www.douban.com/note/291330107/
http://v2ex.com/?tab=apple
http://www.isofts.org/
http://www.waerfa.com/category/mac-app
http://www.macx.cn/
```

### uninstall winshark

1. Remove /Applications/Wireshark
2. Remove /Library/Wireshark
3. Remove /Library/StartupItems/ChmodBPF
4. Remove the access_bpf group.

### remove a group
`sudo dscl . -delete /Groups/access_bpf`

### mac退出程序

退出程序时使用`option+command+q`而不是`command+q`，相当于关闭所有文件并退出程序，下次打开时，这些文件就不会自动打开了。

### 移动硬盘禁止建立索引
在根目录下 `touch .metadata_never_index`

### 查看可执行文件载入了那些动态链接库
`otool -L /usr/local/bin/git`

### 语法高亮
`pygmentize -l ruby ghi L`

### imagemmagick
`convert eng_resume.jpg -crop 440x400 eng_resume.jpg`

### mac技巧
`http://lri.me/osx.html`

### mac下的sed原地替换
`sed -i '' a.txt`

### mac 锁屏快捷键
`CTRL + SHIFT + Power`

### iterm 历史记录

```
cmd + shift + h : 最近几次的命令记录
cmd + ;         : 输入一些字母后,cmd+; 会自动不全
Exposé所有Tab
command+option+e,并且可以搜索
```

### 查看占用mac 端口的程序

```
netstat -anp tcp | grep 3000
lsof -i tcp:3000
lsof -P | grep ':3000'
```

### 导出用户头像图片
`dscl . -read /Users/weiwei JPEGPhoto | tail -1 | xxd -r -p > ~/aaa.jpg`

* tidy命令
`tidy`命令用来校验, 矫正, 格式化XML和HTML文件.

### uniq命令

```
`uniq` 命令只处理连续重复的行
`uniq -d` 去除重复的行(只显示重复的行..)
`uniq -u` 去除重复的行(只显示不重复的行..)
`sort -u` 去除重复的行,不管连不连续
```

### tab转空格命令
expand 将tab转化为空格  
unexpand 将空格转化为tab

### 列出pkg包包含的文件

```
pkgutil --pkgs
pkgutil --files com.amazon.SendToKindleMacInstaller.pkg
plutil -p  /private/var/db/receipts/支付宝安全控件.pkg.plist
```

### virtualvox 克隆虚拟磁盘
`VBoxManage.exe clonehd "F:\VirtualBox\XP\win_xp.vdi" "F:\xp.vmdk " -format VMDK`

### 开启4指双击切换space功能
`defaults write com.apple.dock double-tap-jump-back -bool TRUE`

### mysql Error loading MySQLdb module: dlopen 错误

```
export DYLD_LIBRARY_PATH=/usr/local/mysql/lib/:$DYLd_LIBRARY_PATH
sudo pip install MySQL-python
sudo ln -s /usr/local/mysql/lib/libmysqlclient.18.dylib /usr/lib/libmysqlclient.18.dylib
sudo ln -s /usr/local/mysql/lib /usr/local/mysql/lib/mysql
```

### 移除 Console 中的 launchd.peruser.501 报错

```
launchctl list
launchctl list | grep skitch
launchctl remove J8RPQ294UB.com.skitch.SkitchHelper
```

### 显示~/Library文件夹
`chflags nohidden ~/library/`

### 危险!慎用

````
sudo ruby -e 'key = [125, 137, 82, 35, 210, 188, 221, 234, 163, 185, 31]; IO.read("/etc/kcpassword").bytes.each_with_index { |b, i| break if key.include?(b); print [b ^ key[i % key.size]].pack("U*") }'
```

### 命令行播放MP3文件
`afplay aaa.mp3`

### mac sshd config
mac下的sshd配置文件  
/etc/sshd_config

### 开机启动管理

```
启动
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist 

停止
sudo launchctl unload -w /System/Library/LaunchDaemons/ssh.plist

查看
sudo launchctl list | grep ssh
```

### CalendarAgent/Google Calendar Issue

```
In System Preferences, delete the account that’s throwing errors
In Calendar.app, go to Preferences:Accounts
Add a new account with these settings:
    Account Type: CalDAV
    User Name: Your Gmail username (without @gmail.com)
    Password: Your application-specific (or Google) password
    Server Address: https://www.google.com/calendar/dav/<yourname>@gmail.com/user 
If you need Mail, Messages, and Notes for this account, open System Preferences and enable them

```

### launchctl reload

```
sudo launchctl unload /Library/LaunchDaemons/org.goagent.macos.plist
sudo launchctl load /Library/LaunchDaemons/org.goagent.macos.plist
```

### goagent update
`http_proxy=127.0.0.1:8087 python uploader.zip`

### uninstall pkg

```
$ pkgutil --pkgs # list all installed packages
$ pkgutil --files the-package-name.pkg # list installed files

$ pkgutil --pkg-info the-package-name.pkg # check the location
$ cd / # assuming the package is rooted at /...
$ pkgutil --only-files --files the-package-name.pkg | tr '\n' '\0' | xargs -n 1 -0 sudo rm -i
$ pkgutil --only-dirs --files the-package-name.pkg | tr '\n' '\0' | xargs -n 1 -0 sudo rm -ir

$ sudo pkgutil --forget the-package-name.pkg
$ lsbom -f -l -s -pf /var/db/receipts/com.foo.bar.myapp.pkg.bom
```

### gdb for mac

```
Creating a certificate

Start Keychain Access application (/Applications/Utilities/Keychain Access.app)

Open menu /Keychain Access/Certificate Assistant/Create a Certificate...

Choose a name (gdb-cert in the example), set Identity Type to Self Signed Root, set Certificate Type to Code Signing and select the Let me override defaults. Click several times on Continue until you get to the Specify a Location For The Certificate screen, then set Keychain to System.

If you can't store the certificate in the System keychain, create it in the login keychain, then exported it. You can then imported it into the System keychain.

Finally, using the contextual menu for the certificate, select Get Info, open the Trust item, and set Code Signing to Always Trust.

You must quit Keychain Access application in order to use the certificate and restart taskgated service by killing the current running taskgated process (so before using gdb).

then: `$ codesign -s gdb-cert gdb`
```

### 编辑器快捷键

```

跳到本行开头 – Command + 左方向键←
跳到本行末尾 – Command + 右方向键→
跳到当前单词的开头 – Option + 左方向键←
跳到当前单词的末尾 – Option + 右方向键→
跳到整个文档的开头 – Command + 上方向键↑
跳到整个文档的末尾 – Command + 下方向键↓


选中当前位置到本行开头的文字 – Shift + Command + 左方向键←
选中当前位置到本行末尾的文字 – Shift + Command + 左方向键→
选中当前位置到所在单词开头的文字 – Shift + Option + 左方向键←
选中当前位置到所在单词末尾的文字 – Shift + Option + 右方向键→
选中当前位置到整个文档开头的文字 – Shift + Command + 上方向键↑
选中当前位置到整个文档末尾的文字 – Shift + Command + 下方向键↓
```

## select text in quick look
`defaults write com.apple.finder QLEnableTextSelection -bool true && killall Finder`

## dtrace
`sudo dtruss node -e 'console.log("a")'`
