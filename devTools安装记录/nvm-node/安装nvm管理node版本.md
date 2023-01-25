安装nvm
nvm是node版本管理工具，为了解决node各种版本存在不兼容现象，nvm是让你在同一台机器上安装和切换不同版本的node的工具。

安装nvm
$ brew install nvm

安装完成后，修改环境变量

进入当前用户的Home目录

$ cd ~

> 这里以zsh为例，在 `~/.zshrc` 这个配置文件中配置，如果你的 shell 用的是 bash 或其它的，就找找看 `~/.bash_profile` 或者 `~/.profile`，`~/.bashrc`。

这一步的作用是每次新打开一个bash，nvm都会被自动添加到环境变量中了。





编辑.bash_profile文件
$ vim .bash_profile
在文件里添加以下内容（安装nvm成功后终端的最后3行代码）

###### export NVM_DIR="$HOME/.nvm"

###### #This loads nvm
###### [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  

###### #This loads nvm bash_completion
###### [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  

然后按 esc 退出编辑模式
按 :wq 保存并退出

输入以下命令，更新配置过的环境变量
$ source .bash_profile

查看nvm版本
$ nvm --version

如果出现版本号，则说明安装成功

nvm 常用语法
安装node指定版本
$ nvm install 版本号


查看本地node的所有版本
$ nvm list

切换到指定的node版本
$ nvm use 10.19

卸载指定的node版本
$ nvm uninstall 版本号

安装最新的node稳定版本
$ nvm install --lts

查看node的所有的版本
$ nvm ls-remote

使用node指定版本执行指定文件
$ nvm exec 版本号 node 要执行的文件路径

例如：nvm exec 4.8.3 node app.js
表示使用4.8.3 版本的node，执行app.js文件

设置默认版本的Node，每次启动终端都使用该版本的node
$nvm alias default 版本号

