---
title: 2019-07-12-Notes-iterm2的安装及相关设置
date: 2019-07-12 18:50:11
tags: Notes
---

## 1.安装iterm2

> 官网下载[iterm2](https://www.iterm2.com/)，直接安装即可

<!--more-->

## 2.配置

> 查看当前系统可以使用哪些shell
```shell
cat /etc/shells
```

> 查看当前正在使用的shell
```shell
echo $SHELL
```

> 将Mac系统终端由默认使用的sash切换至zsh
```shell
chsh -s /bin/zsh
```

## 3.安装Oh My ZSH
> 官方推荐的安装方法
```shell
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## 4.安装PowerLine
> 安装powerline之前如果没有安装pip，需先安装pip命令
```shell
# 已安装的无需再次安装
sudo easy_install pip
```

```shell
pip install powerline-status --user
```


## 5.安装PowerFonts
> 在常用的位置新建一个文件夹，如：~/OpenSource

在OpenSource文件夹下下载PorweFonts
```shell
git clone https://github.com/powerline/fonts.git --depth=1
cd fonts
./install.sh
```

安装好字体库之后，再设置iTerm2的字体
```shell
iTerm2 -> Preferences -> Profiles -> Text
```
具体参考下图：
![](image_01.png)

## 6.安装配色方案

在OpenSource文件夹下下载配色方案
```shell
git clone https://github.com/altercation/solarized
cd solarized/iterm2-colors-solarized/
open .
```
在打开的finder窗口中，双击Solarized Dark.itermcolors和Solarized Light.itermcolors即可安装明暗两种配色

根据个人喜好选择配色
```shell
iTerm2 -> Preferences -> Profiles -> Colors -> Color Presets
```

## 7.安装主题

在OpenSource文件夹下下载主题
```shell
git clone https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor.git
cd oh-my-zsh-agnoster-fcamblor/
./install
```
执行上面的命令会将主题拷贝到oh my zsh的themes.

执行命令打开zshrc配置文件
```shell
vim ~/.zshrc
```
将ZSH_THEME后面的字段改为agnoster，如下图：
![](image_02.png)

## 8.安装高亮插件
> 这是oh my zsh的一个插件，安装方式与theme大同小异

```shell
cd ~/.oh-my-zsh/custom/plugins/
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
```
再次打开zshrc文件进行编辑
```shell
vim ~/.zshrc
```
找到plugins，此时plugins中应该已经有了git，我们需要把高亮插件也加上：
![](image_03.png)
请务必保证插件顺序，zsh-syntax-highlighting必须在最后一个

然后在文件的最后一行添加后，保存并退出
```shell
source ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```
执行命令使刚才的修改生效
```shell
source ~/.zshrc
```

## 9.可选择、命令补全
> 跟代码高亮的安装方式一样，这也是一个zsh的插件，叫做zsh-autosuggestion，用于命令建议和补全。

```shell
cd ~/.oh-my-zsh/custom/plugins/
git clone https://github.com/zsh-users/zsh-autosuggestions
```
再次打开zshrc文件进行编辑
```shell
vim ~/.zshrc
```
找到plugins，加上这个插件即可
![](image_04.png)