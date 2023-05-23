---
title: ARMBIAN部署memos开源笔记软件
date: 2023-05-05
categories:
  - 编程电脑
  - 软件安装
tags: 
   - MEMOS
   - 开源笔迹
   - ARMBIAN
---
memos 是「一个具有知识管理和社交网络的开源、自我托管的备忘录中心」。
<!-- more -->
这是一个类似私人微博的产品，支持标签、过滤、搜索、多账户，可以自用也可以和朋友一起使用，用来碎片化的记录信息，就像 flomo 一样。

## 一、主要特征

![memos](https://preview.cloud.189.cn/image/imageAction?param=E2AAD4D8A23CC9D6536A1C08F848EA43799ECD4C1795AE472729BC8AC92D8D72651906D903D4F225E24A36F585A7424F86C0DCFCDE672DB1D0D128861C8BE28B3E0EA77E3250B80F6115A60A040D58300D0E529A89BAFC2A4DCA0FE6BD33CD3D42426385A33A0593FB92DE0B2874D6C0)

- 🦄 开源且永久免费
- 🚀 使用 Docker 几秒内安装托管
- 📜 纯文本，支持 Markdown 语法
- 👥 将备忘录设为私人或公开给
- 🧑‍💻 支持 RESTful API
- 📋 使用 iframe 在其他网站上嵌入备忘录
- 🏷️ 支持标签
- 📆 GitHub 式的交互式日历视图
- ☁️ 数据库可保存至 S3 API（AWS S3、Cloudflare R2、MinIO）
- 👮 支持 SSO 登录（OAuth 2.0）
- 💾 轻松迁移和备份数据

## 二、安装

附上 [Docker](https://sspai.com/link?target=https%3A%2F%2Fdocs.docker.com%2Fengine%2Finstall%2Fubuntu%2F) 官方部署文档（如果需要更详细的安装流程，请参考官方文档）

### （一）Docker 的安装

#### 1.卸载

如果已经存在旧版本的 Docker并且想要卸载请执行卸载命令（非必要）

```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

#### 2.设置存储库

更新 apt 包索引并安装包以允许apt通过 HTTPS 使用存储库

```
sudo apt-get update

sudo apt-get install ca-certificates curl gnupg lsb-release
```

添加 Docker 的官方 GPG 密钥

```
 sudo mkdir -p /etc/apt/keyrings

 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

使用以下命令设置存储库

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### 3.安装 Docker 引擎

更新 apt 包索引，安装最新版本的 Docker Engine、containerd 和 Docker Compose

```
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

#### 4.验证 Docker 运行情况

当 `Active: active (running)` 为 `running`时说明 Docker 运行正常

当进行到这一步骤的时候说明你的 Docker 服务已经成功安装了，离 Memos 的成功安装已经很近了。

### （二）Memos 服务的部署

仓库地址： <https://github.com/usememos/memos>

#### 1.创建存储卷

我们要先在服务器创建一个目录用来存储 Memos 数据。

```
mkdir memos
```

然后需要将创建的目录挂载到docker的容器里，我们先查看一下memos 的路径，下面启动 Memos 的时候需要指定此路径。

```
pwd
```

#### 2.运行容器

这条命令的参数的意思是： 将容器内的 5230 端口映射到宿主机的 5230 端口上，同时将容器内 `/var/opt/memos`路径下的内容挂载到宿主机的 `/root/memos`路径下，路径映射的好处是防止容器被误删导致数据丢失。此处地址要和安装的地址一致，即`pwd`输出结果。

只需要一条命令就能够启动 Memos 容器：

```
docker run -d --name memos -p 5230:5230 -v /root/memos/:/var/opt/memos neosmemo/memos:latest
```

这条命令的参数的意思是： 将容器内的 5230 端口映射到宿主机的 5230 端口上，同时将容器内 /var/opt/memos路径下的内容挂载到宿主机的 /root/memos 路径下，路径映射的好处是防止容器被误删导致数据丢失。

查看容器运行状态

```
docker ps -a
```

当我们看到容器状态是 Up 的时候说明我们已经成功部署好了 Memos 服务，只需要在浏览器访问 127.0.0.1:5230 就可以开的 Memos 的初始页面了

```bash
运行容器：docker run -it 镜像名 /bin/bash

退出容器：exit 或者 Ctrl+P+Q

查看所有容器：docker ps -a

查看运行的容器：docker ps

重启容器：docker restart 容器ID

重启容器后进入交互式：docker start -i 5c6ce895b979

进入容器：docker attach 容器ID

docker exec -it 容器ID /bin/bash
```

<<<<<<< HEAD
### （三）Memos 服务升级
#### 1.删除现有容器
首先进入memo文件夹，然后进行操作，一般情况下操作会出错，没有yml类型文件，可忽略。

```
cd memos
docker-compose down  
docker-compose pull
docker-compose up -d
```

#### 2.备份文件
首先将数据文件、配置文件备份。也就是memo文件夹下的三个文件。 `memos_prod.db ` 和 `memos_prod.db-shm`   还有 `memos_prod.db-wal` 三个文件备份，以待恢复。

#### 3.删除容器

```
docker stop memos

docker rm -f memos
```
#### 4.拉取最新镜像并创建容器

```
docker pull neosmemo/memos:latest  # 拉取最新镜像

sudo docker run -d --name memos -p 5230:5230 -v /home/linux/memo/:/var/opt/memos neosmemo/memos:latest  # 创建容器

```

#### 5.恢复文件、更改文件权属并重新设置内网穿透


=======
>>>>>>> 1c1eca960bc274aa0889e5d7f74fc3f120868fd7
## 三、第三方客户端

- 第三方客户端：[Moe Memos](https://memos.moe/)
- Chrome 扩展：[lmm214/memos-bber](https://github.com/lmm214/memos-bber)
- 微信小程序：[Rabithua/memos_wmp](https://github.com/Rabithua/memos_wmp)
- Telegram Bot：[qazxcdswe123/telegramMemoBot]
(<https://github.com/qazxcdswe123/telegramMemoBot>)
- Obsidian插件： [Obsidian Memos](https://github.com/quorafind/obsidian-memos)
<<<<<<< HEAD

=======
>>>>>>> 1c1eca960bc274aa0889e5d7f74fc3f120868fd7
