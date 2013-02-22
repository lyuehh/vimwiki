# mac

## mac 锁屏快捷键
`CTRL + SHIFT + Power`

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
`uniq -d` 去除重复的行(只剩1行)
`uniq -u` 去除重复的行(1行不剩)




