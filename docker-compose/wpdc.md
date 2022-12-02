# WPDC - WordPress Docker Compose

使用Docker和Docker Compose轻松开发WordPress。

通过这个项目，您可以快速运行以下内容：

- [WordPress和WP CLI](https://hub.docker.com/_/wordpress/)
- [phpMyAdmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/)
- [MySQL](https://hub.docker.com/_/mysql/)

内容：

- [要求](#requirements)
- [配置](#configuration)
- [安装](#installation)
- [用法](#usage)

## 要求

确保您的计算机上安装了最新版本的Docker和Docker Compose。

克隆此存储库或将此存储库中的文件复制到新文件夹中。在thedocker-compose.yml文件中，您可以将IP地址（如果您运行多个容器）或数据库从MySQL更改为MariaDB。
使用Linux时 [请务必将您的用户添加到docker组中。](https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user) when using Linux.

## 配置

将示例环境复制到 `.env`

```
cp env.example .env
```

编辑 `.env` 文件以更改默认IP地址、MySQL根密码和WordPress数据库名称。

## 安装

将docker-compose.yml文件复制到新目录中。在目录中，您可以创建两个文件夹：

```
docker-compose up
```

这在您的`docker-compose.yml` 文件旁边创建了两个新文件夹.
* `wp-data`  –用于存储和恢复数据库转储
* `wp-app` –您的WordPress应用程序的位置
容器现已建成并运行。您应该能够在浏览器地址中使用配置的IP访问WordPress安装。默认情况下，它是http://127.0.0.1。
为了方便起见，您可以在主机文件中添加新条目。


## 用法
### 起始容器
您可以`up` 在守护进程模式下（通过添加-d作为参数）或使用start命令启动容器：
You can start the containers with the command in daemon mode (by adding `-d` as an argument) or by using the `start` command:

```
docker-compose start
```

### 停止容器

```
docker-compose stop
```

### 移除容器

要停止并删除所有容器，请使用`down`命令：

```
docker-compose down
```

如果您需要删除用于持久化数据库的数据库卷，请使用-v：

```
docker-compose down -v
```

### 来自现有来源的项目
Copy the `docker-compose.yml` file into a new directory. In the directory you create two folders:

* `wp-data` – –在这里，您可以添加数据库转储
* `wp-app` –在这里，您可以复制现有的WordPress代码

您现在可以使用up命令：

```
docker-compose up
```

这将创建容器，并使用给定的转储填充数据库。您可以设置主机条目并在数据库中更改它，或者您只需通过添加以下内容来覆盖inwpwp-config.php：
```
define('WP_HOME','http://wp-app.local');
define('WP_SITEURL','http://wp-app.local');
```
### 创建数据库转储

```
./export.sh
```

### 开发一个主题

配置卷以在docker-compose.yml的容器中加载主题：

```
volumes:
  - ./theme-name/trunk/:/var/www/html/wp-content/themes/theme-name
```

### 开发插件

配置卷以在docker-compose.yml的容器中加载插件：

```
volumes:
  - ./plugin-name/trunk/:/var/www/html/wp-content/plugins/plugin-name
```

### WP CLI

docker编写配置还提供了使用WordPress CLI的服务。

安装WordPress的示例命令：

```
docker-compose run --rm wpcli core install --url=http://localhost --title=test --admin_user=admin --admin_email=test@example.com
```

或者列出已安装的插件：

```
docker-compose run --rm wpcli plugin list
```

为了便于使用，您可以考虑为CLI添加别名：

```
alias wp="docker-compose run --rm wpcli"
```

这样，您可以使用上面的CLI命令如下：

```
wp plugin list
```

### phpMyAdmin

启动容器后，您还可以访问http://127.0.0.1:8080访问phpMyAdmin。

默认用户名是root，密码与.env文件中提供的密码相同。
