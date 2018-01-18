## vsCode  编辑器

[相关文档](https://jeasonstudio.gitbooks.io/vscode-cn-doc/content/md/%E5%AE%9A%E5%88%B6%E5%8C%96/%E7%94%A8%E6%88%B7%E5%AE%9A%E4%B9%89%E4%BB%A3%E7%A0%81%E6%AE%B5.html)


【链接】VisualStudioCode入门(译)
http://www.jianshu.com/p/3dda4756eca5

**vscode快捷键**

```
1.~/.bash_profile(用户的快捷键设置，关闭需要重新弄)

code () { VSCODE_CWD="$PWD" open -n -b "com.microsoft.VSCode" --args $* ;}
export ANDROID_HOME=/Users/songkk/Library/Android/sdk

2.source ~/.bash_profile

3.code .就打开了

```

**快速进入项目：**

```
cd ~

atom .zshrc(全局的，无论在哪输入goAdmin就可以进入admin项目)

最后加alias goAdim="cd /Users/liuyihao/kr-dev/Code/kr-admin-new"
export EDITOR="goAdim"

```
