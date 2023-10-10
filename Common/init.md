# 初始化

更新系统软件包列表：

```shell
sudo apt update
```

安装 build-essential 包，这个包包含了一些必要的编译工具：

```shell
sudo apt install build-essential
```

安装 Git，是一个版本控制工具：

```shell
复制代码sudo apt install git
```

安装一个文本编辑器，例如 vim 或者你喜欢的其他文本编辑器：

```shell
复制代码sudo apt install vim
```

其他部分

```shell
# 
sudo apt install npm 
sudo apt install nodejs
```

安装 Java

```bash
sudo apt install openjdk-17
# 打开/etc/environment文件
vim /etc/environment
#将JAVA_HOME指定到OpenJDK17，在文件末尾添加
JAVA_HOME="/usr/lib/jvm/java-17-openjdk-amd64"

source /etc/environment

echo $JAVA_HOME
```

Ubuntu 系统如何使用 root 用户登录实例？

[Ubuntu 系统如何使用 root 用户登录实例？](https://cloud.tencent.com/document/product/1207/44569#ubuntu-.E7.B3.BB.E7.BB.9F.E5.A6.82.E4.BD.95.E4.BD.BF.E7.94.A8-root-.E7.94.A8.E6.88.B7.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B.EF.BC.9F)

