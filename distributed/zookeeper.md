# Zookeeper

## 下载安装包

下载速度慢可以手动下载到本机然后传过去

```bash
cd /usr/local/
sudo wget https://archive.apache.org/dist/zookeeper/zookeeper-3.5.9/apache-zookeeper-3.5.9-bin.tar.gz

sudo tar -zxvf apache-zookeeper-3.5.9-bin.tar.gz 
```

## 配置目录

```bash
cd apache-zookeeper-3.5.9-bin/
	
mkdir data
mkdir logs

cp conf/zoo_sample.cfg conf/zoo.cfg
```

![image-20231010192538401](https://ericcoder-oss.oss-cn-hangzhou.aliyuncs.com/markdown_images/image-20231010192538401.png)

可以添加admin.serverPort=8079避免8080端口冲突

后续配置根据需求再更加细化