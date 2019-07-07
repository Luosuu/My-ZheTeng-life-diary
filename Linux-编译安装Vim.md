# Linux下编译安装Vim
### 为什么要编译安装配置Vim
Vim是一种很强大的编辑器，很多时候我们在Linux下的需求都是在Vim上解决的。而很多Linux的发行版或许版本过老，或者很多配置不符合我们的期待。所以我们需要自己编译配置Vim。
所谓的编译配置就是通过git clone下来源代码，自己按照需求调整设置安装（即安装的时候添加config参数）。
### 你需要准备的东西
你的Linux发行版需要先具备git。
```shell
sudo apt install git
 ```
如果你需要编译安装的目的是使Vim支持python的一些命令，那么你需要安装一些依赖。
 ```shell
sudo apt-get install python-dev
sudo apt-get install python3-dev
sudo apt-get install libncurses5-dev
 ```
至于你需要什么样的依赖，以及想要知道自己的Vim已经支持了什么功能，你只需要在终端里
```shell
vim --version
 ```
显示内容就会告诉你，你的Vim的版本（一般推荐Vim8），以及你的Vim已经支持的功能。前面是`+`的，就是支持的，前面是`-`的，就是不支持的。Deepin15.10.1自带的Vim8就不支持python与python3。
对于开发要求多一些的，python，go，markdown都有需求的可以按照如下安装依赖
```shell
sudo apt install libncurses5-dev libgnome2-dev libgnomeui-dev libgtk2.0-dev libatk1.0-dev libbonoboui2-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev python3-dev ruby-dev lua5.1 liblua5.1-dev libperl-dev 
 ```
### 开始折腾
#### (1)彻底删除你的Vim
没错，你要**彻底的**删除你的Vim。不要以为单纯的`sudo apt remove vim`就能做到这一点。你常常需要添加`--purge`来达到根本去除它的目的。不过你也可以尝试不完全删除掉，直接进行后面的步骤，尝试直接覆盖安装掉，在一些情况下并不会产生冲突的错误。这很玄学。
对于Ubuntu/Debian用户：
```shell
sudo apt-get remove --purge vi vim-tiny vim vim-runtime gvim vim-common vim-gui-common vim-nox
 ```
对于ArchLinux用户
```shell
sudo pacman -Rsn vi vim-tiny vim vim-runtime gvim vim-common vim-gui-common vim-nox
 ```
 其他发行版，例如Deepin这样的系统，它基于Debian不稳定版开发，所以一般命令都和Debian一样，你也可以查查自己的发行版基于什么开发，它的命令是什么样的。
一般来说这样就够了，但是可以的话建议全局搜索vim以避免漏网之鱼，要注意一些系统文件不能删去，否则你就要重装你的系统了。具体可以参考[Linux 下源码编译安装 vim 8.1]('https://www.v2ex.com/t/483931')。
当然你也可以有更好的办法
```shell
dpkg -l | grep vim
 ```
 这样你就可以知道你所有的vim相关的东西了。然后用`sudo apt remove --purge ···`将它们都删掉。`sudo dpkg -P vim vim-common vim-run`也可以做到这一点。
#### (2)克隆代码
```shell
git clone https://github.com/vim/vim.git
 ```
#### (3)进入文件夹更改配置开关
```shell
# 进入Vim的文件夹
cd ./vim
# 更改配置文件
./configure --with-features=huge \
    --enable-multibyte \
    --enable-rubyinterp=yes \
    --enable-python3interp=yes \
    --with-python-config-dir=/usr/lib/python3.7/config-3.7m-x86_64-linux-gnu \
    --enable-perlinterp=yes \
    --enable-luainterp=yes \
    --enable-gui=gtk2 \
    --enable-cscope \
    --prefix=/usr/local
 ```
 注意到里面的`with-python-config-dir=···`那一行了吗？那一行的配置因发行版的不同而不同。
 你可以在终端中输入
 ```shell
whereis python3
  ```
`whereis`用于查找应用程序的位置。这样你就能看见python3的位置了。你会看到很多位置，这是因为一个应用程序会有很多部分，这些部分就分布在不同的文件夹里。那么如何找到咱们需要的那个路径呢?答案是和别人配置好的路径里的内容找相似（我知道你很无语）。但可能这就是Linux吧，或许是我太菜，没找到更好的办法。
在Deepin15.10.1中，其运行结果应该是
```shell
python3: /usr/bin/python3.5m-config
 /usr/bin/python3.5-config \
 /usr/bin/python3.5m  \
 /usr/bin/python3.5 \
 /usr/bin/python3 \
 /usr/lib/python3.5 \
 /usr/lib/python3 \
 /etc/python3.5 \
 /etc/python3 \
 /usr/local/lib/python3.5 \
 /usr/include/python3.5m \
 /usr/include/python3.5 \
 /usr/share/python3 \
 /usr/share/man/man1/python3.1.gz
 ```
 然后你看到了很多路径，你可能很无奈。但是你要看到希望啊！
 我们浏览这些文件夹，看到了和别人配置好的路径相似的文件夹`/usr/lib/python3.5`。于是我们进去看看这里面有啥，有没有我们需要的`config-3.5m-x86_64-linux-gnu`（按照名字推测来的）。
```shell
cd /usr/lib/python3.5
# ls是代表将文件夹的所有内容陈列出来
ls
  ```
其内容过于多，就不在这里陈列了，但是我们确实在这个文件夹里找到了`config-3.5m-x86_64-linux-gnu`。这是我们胜利的曙光！
我们把这个更改到配置里去，更改后如下
```shell
./configure --with-features=huge \
    --enable-multibyte \
    --enable-rubyinterp=yes \
    --enable-python3interp=yes \
    --with-python-config-dir=/usr/lib/python3.5/config-3.5m-x86_64-linux-gnu \
    --enable-perlinterp=yes \
    --enable-luainterp=yes \
    --enable-gui=gtk2 \
    --enable-cscope \
    --prefix=/usr/local
 ```
 这样就基本大功告成了。不要忘记要make和make install，很多教程都忘了make然后直接make install了，这样会出问题。
 #### (4)make与make install
 ```shell
make VIMRUNTIMEDIR=/usr/local/share/vim/vim81
make install
 ```
最后，再利用`vim --version`功能是不是已经启用！
### 关于本文
会有很多错误和不妥的地方，大部分参考于[Linux 下源码编译安装 vim 8.1]('https://www.v2ex.com/t/483931')。