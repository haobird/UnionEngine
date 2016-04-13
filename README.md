# UnionEngine
Development environment of UnionEngine, based on Docker

## 环境要求

Mac系统，已经安装过以下组件：

- VirtualBox
- git
- Homebrew
- pip

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install wget
sudo easy_install pip
```

## 安装Docker/Boot2Docker/Docker-Compose（最好参考官方安装教程）

```
brew update
brew tap homebrew/binary
brew install docker boot2docker
sudo pip install -U docker-compose
```

Ubuntu系统，已经安装过以下组件：

```
apt-get update && apt-get install python gcc make g++ git vim  wget curl pip
```

## 安装Docker/Boot2Docker/Docker-Compose（最好参考官方安装教程）

```
curl -sSL https://get.docker.io/ubuntu/ | sudo sh
sudo pip install -U docker-compose
```

### 设置Docker镜像，加速下载（请针对你能访问的源添加）

Mac下：

```
boot2docker ssh
sudo vi /var/lib/boot2docker/profile
EXTRA_ARGS="--registry-mirror=http://192.168.11.180:5000"
boot2docker restart
```

Ubuntu下:

```
vi /etc/default/docker
DOCKER_OPTS=" --registry-mirror http://192.168.11.180:5000 --insecure-registry 192.168.11.180:5000"
service docker restart
```

##目录说明

建立目录

```
mkdir /www /www/htdocs/ /www/log/ /www/settings/
```

- /www 工作目录
- /www/htdocs/ 多项目目录
- /www/log/ log日志记录
- /www/settings/nginx/ nginx域名配置文件，.conf 后缀结尾

主机域名配置如下例：

```
server {
    listen   80 ;
    index index.html index.htm;
    server_name app.dev;

    root /opt/htdocs/app/public;
    index index.php index.html index.htm;
    location / {
        expires off;
        try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php {
        expires off;
        include fastcgi_params;
        fastcgi_pass   php:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    }
}
```


## 构建步骤

下载镜像及构建镜像

```
make dl
make build
```

构建及运行环境

```
docker-compose build
docker-compose up -d
```

