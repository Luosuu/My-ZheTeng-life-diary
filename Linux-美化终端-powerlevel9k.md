# Linux-不美还用个啥劲儿系列
Linux提供了非常高的自定义美化终端的空间。不搞的漂亮点，天天面对丑丑的终端，谁受得了啊！
本文主要参考（~~搬运~~）于[Powerlevel9k --- 一个美观而又实用的 ZSH 主题](https://www.jianshu.com/p/f84cf6132d1e)。
## 安装zsh
我们目标的主题是oh my zsh里面的一个主题，而安装oh my zsh需要安装zsh。
```shell
sudo apt install zsh
```
## 安装字体
然后你可能需要安装一下字体
```shell
# clone
git clone https://github.com/powerline/fonts.git
# install
cd fonts
./install.sh
```
## 更改主题
```shell
~./zshrc
```
然后修改里面的`ZSH_THEME= ···`为
`ZSH_THEME="powerlevel9k/powerlevel9k"`
然后重新打开终端，康康你的终端有没有发生令人惊喜的变化。
## 如果出现了问题
那可能是你的默认终端出现了问题。你可以进入终端后尝试`zsh`，康康你的终端变化没有，如果成功变化了，说明你安装成功了，但是默认的终端没有换成zsh。你可以尝试
```shell
chsh -s /bin/zsh
 ```
然后重启终端。关于chsh可以自己谷歌具体作用（change shell的缩写）。
