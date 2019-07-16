# 为你的zsh增加语法高亮

首先进入到zsh的插件文件夹，我用的是omz，所以要进入omz的插件文件夹

```shell
cd ~/.oh-my-zsh/custom/plugins
```

然后下载插件

```shell
git clone git://github.com/zsh-users/zsh-syntax-highlighting.git
```

然后更改`.zshrc`里的配置

```shell
plugins=(zsh-syntax-highlighting)
```

然后读取配置即时生效

```shell
source ~/.zshrc
```
