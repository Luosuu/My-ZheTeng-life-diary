# 管理npm和node

前端开发经常必然需要很好的管理自己的npm和node。奈何mac上的homebrew不给力，经常有很多问题。

通过查询知道还有nvm这样一种方便的工具可以使用。便立即学习了一下。

首先需要安装nvm。

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
```

然后你可以直接运行

```bash
nvm install node
```

来直接安装最新的node。

也可以使用

```bash
nvm ls-remote
```

看看所有可用的版本。

如果你有多个node版本。可以仿照下面的代码交换使用。

```bash
nvm use v12.7.0
```

如果使用

```bash
nvm use node
```

就切换到最新版了。

其他用法可以看官方文档。
