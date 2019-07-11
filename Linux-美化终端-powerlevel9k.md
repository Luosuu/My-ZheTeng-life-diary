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

## 安装omz

```shell
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

如果你没安装curl会提醒你安装

```shell
sudo apt install curl
```

## 更改主题

```shell
vim ~./zshrc
```

然后修改里面的`ZSH_THEME= ···`为
`ZSH_THEME="powerlevel9k/powerlevel9k"`
然后重新打开终端，康康你的终端有没有发生令人惊喜的变化。

### 涉及的vim操作

进去后按i进入编辑模式，编辑完了之后输入`:wq`退出，这样退出才会保存你做到更改。

## 如果出现了问题

那可能是你的默认终端出现了问题。你可以进入终端后尝试`zsh`，康康你的终端变化没有，如果成功变化了，说明你安装成功了，但是默认的终端没有换成zsh。你可以尝试

```shell
chsh -s /bin/zsh
 ```

然后重启终端。关于chsh可以自己谷歌具体作用（change shell的缩写）。

## 如果不是上面这个问题

你进去了之后发现是乱码，那么就是你的字体虽然安装了但是没有启用。你可以在外面的设置里将终端的默认字体改成`powerline`系的字体。理论上来说只要包含powerline字体即可，现在很流行的`nerd-fonts`也包含powerline字体。
