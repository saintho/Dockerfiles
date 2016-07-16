# Run Under Mac

## 环境要求

Mac系统，已经安装过以下组件：

- DockerToolbox
- git

```
内存充足的话，建议将虚拟机内存调整到4GB

```
VBoxManage modifyvm boot2docker-vm --memory 4096
```

运行Docker需要设置环境变量，建议在~/.bashrc中加入

```
if [ "`boot2docker status`" = "running" ]; then
    eval "$(boot2docker shellinit)"
fi
```


### 设置Docker镜像，加速下载

参考DaoCloud网站列子

## 启动EvaSkeleton

准备基础的目录，由于Mac下默认允许挂载/Users/的文件，因此本套方案将系统文件挂载位置强制设置为`~/opt/`

- ~/opt/data   存放MySQL数据库，Elastic数据
- ~/opt/htdocs 项目代码
- ~/opt/log    存放所有输出Log

创建这些目录:

```
mkdir ~/opt ~/opt/data ~/opt/data/mysql ~/opt/data/elasticsearch ~/opt/log ~/opt/log/nginx ~/opt/log/php ~/opt/htdocs
```

Clone本项目

```
cd ~/opt/htdocs
git clone https://github.com/saintho/Dockerfiles.git
Dockerfiles.git
cd Dockerfiles
```

下载镜像及构建

```
make dl
make build
```

构建及运行环境

```
docker-compose build
docker-compose up
```

绑定域名

```
sudo vi /etc/hosts
加入
192.168.99.100 docker local.evaengine.com static.evaengine.com
```

现在可以通过访问`http://docker/`来查看Web服务器根目录


构建EvaSkeleton项目文件

```
cd ~/opt/htdocs
git clone https://github.com/EvaEngine/EvaSkeleton.git
cd EvaSkeleton
cp config/config.local.dev.php config/config.local.php
make install
```
