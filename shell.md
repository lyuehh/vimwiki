# shell tips

## 文件是否存在
`[[ -f ~/.ssh/id_rsa.pub ]] || ssh-keygen -t rsa`

## 复制文本
`[[ -f ~/.ssh/id_rsa.pub ]] && cat ~/.ssh/id_rsa.pub | pbcopy ;# only on mac`

