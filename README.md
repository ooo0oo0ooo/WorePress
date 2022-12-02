# 使用Docker Compose在本地主机和生产中部署Wordpress

相关博客文章：

  - [使用Docker Compose进行WordPress本地开发](https://www.datanovia.com/en/lessons/wordpress-local-development-using-docker-compose/):使用docker在本地主机上部署Wordpress
  - [Docker WordPress生产部署](https://www.datanovia.com/en/lessons/docker-wordpress-production-deployment/):使用docker-compose在线部署WordPress的分步指南
  - [使用Docker WordPress Cli管理WordPress网站](https://www.datanovia.com/en/lessons/using-docker-wordpress-cli-to-manage-wordpress-websites/):用于管理WordPress网站的命令行界面
  - 
这里提供的安装工具包包括：

  - Nginx网络服务器
  - MariaDB/MySQL用于Wordpress数据库
  - phpMyAdmin界面连接到您的MySQL数据库
  - WP-Cli：Wordpress命令行界面
  - 用于自动化的Makefile指令。

您可以使用以下命令在5分钟内自动部署本地docker wordpress网站：

``` bash
# Download a wordpress docker-compose example
git clone https://github.com/kassambara/wordpress-docker-compose
cd wordpress-docker-compose
# Build and start installation
docker-compose up -d --build
```
在http://localhost访问您的网站，并通过phpMyAdmin访问您的数据库http://localhost:8080。

您的wordpress网站管理员的默认标识：

  - `Username: wordpress` and
  - `Password: wordpress`

phpMyAdmin接口的默认标识：

  - `Username: root` and
  - `Password: password`

**要知道的一组有用的命令：**:

``` bash
# Stop and remove containers
docker-compose down
# Build, and start the wordpress website
docker-compose up -d --build
# Reset everything
docker-compose down
rm -rf certs/* certs-data/* logs/nginx/* mysql/* wordpress/*
```

## 参考文献

  - [WordPress：使用Docker中的Nginx Web服务器](https://github.com/mjstealey/wordpress-nginx-docker)
  - [快速入门：编写和WordPress](https://docs.docker.com/compose/wordpress/)
