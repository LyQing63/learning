# MongoDB
> 适用于Linux服务端

## 服务器使用

1. 登录服务器

```PowerShell
ssh root@xxx.xxx.xxx.xxx
```

> “@”后为服务器公网地址

## Docker

1. 查看Docker版本号

```PowerShell
sudo docker version
```

* 若已安装
```
Client: Docker Engine - Community
 Version:           20.10.6
 API version:       1.41
 Go version:        go1.13.15
 Git commit:        370c289
 Built:             Fri Apr  9 22:46:45 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server:
 Engine:
  Version:          20.10.2
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.13.8
  Git commit:       20.10.2-0ubuntu1~20.04.2
  Built:            Mon Mar 29 19:10:09 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.5.2-0ubuntu1~20.04.2
  GitCommit:        
 runc:
  Version:          1.0.0~rc95-0ubuntu1~20.04.1
  GitCommit:        
 docker-init:
  Version:          0.19.0
  GitCommit:       
```

2. 安装Docker
```
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

3. 安装MongoDB
```
sudo docker pull mongo:latest //下载镜像源
sudo docker images//查看镜像源
sudo docker run -itd --name mongo -p 27017:27017 mongo --auth//启动
sudo docker ps//检查是否启动
```

4. 创建 admin 账户
	1. 登录数据库
	```
	sudo docker exec -it mongo mongosh admin
	```
	2. 创建管理员账户
	```
	db.createUser({ user:'admin', pwd:'123456', roles:[{ role:'root', db:'admin' }]});
	```
	3. 认证管理员账户
	```
	db.auth('admin', '123456')
	```
> ```db```开头的指令都必须登陆后才能执行

5. 创建数据库
	1. 切换数据库
	```
	use practice//数据库名
	```
	> 若数据库储存在则打开，若不存在则创建后打开
	2. 创建读写用户
	```
	db.createUser({ user:'xxxx',pwd:'xxxxxx',roles:[{ role:'root', db: 'admin'},{ role:'dbAdmin', db: 'practice'}]});
	```
	3. 认证数据库
	```
	db.auth('xx', 'xxx')
	```
	> 再次登录数据库后只需要执行 1 与 3 两步即可
6. 退出登录
```
exit
```

7. Spring 项目中的配置
```
## 购买的云服务器的公网 IP
spring.data.mongodb.host=
## MongoDB 服务的端口号
spring.data.mongodb.port=27017
## 创建的数据库及用户名和密码
spring.data.mongodb.database=
spring.data.mongodb.username=
spring.data.mongodb.password=
```
