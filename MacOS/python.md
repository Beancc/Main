#### 首先，Mac系统是自带python的，比如说我的mac，在终端输入`python --version`，会跳出`Python 2.7.16`的提示。但是我们现在一般使用的都是python3以上的版本，这就需要我们去官网自己下载。
#### 下载安装略，这里注意从官网下载的话比在终端里直接用命令安装要快，原因吗也很简单，源是国外的嘛。
#### 安装完以后此时重新执行版本查询命令发现还是原来python2那个版本，这时候不要慌，其实已经安装好了，但是你希望制定版本就是你最新安装的版本的话，需要配置一下环境变量。
#### 配置的指令如下，根据自己实际安装版本和位置进行修改，大体命令如下：
```shell
export PATH=${PATH}:/usr/local/Cellar/python@3.8/3.8.5/bin
alias python="/usr/local/Cellar/python@3.8/3.8.5/bin/python3"
alias pip="/usr/local/Cellar/python@3.8/3.8.5/bin/pip3"
```
至此，python3的版本就已经安装好和配置好了。

