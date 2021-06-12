###### 安装php依赖模块

- fileinfo
- redis


###### php 禁用函数删除

- putenv
- pcntl_alarm
- pcntl_signal
- symlink
- proc_开头函数


#### 数据库 mysql

`新建数据库-MySQL-utf8mb4`

`记录以下信息`
- 数据库名
- 账号
- 密码


#### nginx 设置

##### 设置运行目录

- 运行目录至pubilc 
- 取消防跨站攻击(openbase_dir)

##### 设置伪静态(laravel5伪静态)

```

location / {  
	try_files $uri $uri/ /index.php$is_args$query_string;  
}  

```

##### 设置SSL

```
let's Encrypt

```

#### 网站配置

##### 复制配置文件模板

```

cp .env.example .env

```

##### 编辑.env


```

DB_HOST=127.0.0.1 数据库服务器IP/域名
DB_PORT=3306 数据库端口 默认为3306
DB_DATABASE=ProxyPanel 数据库名
DB_USERNAME=root 用户名
DB_PASSWORD=root 密码

```


#### 安装 `composer`

```

## centos
yum install composer

## ubutu
apt-get install composer

## 备用
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/bin --filename=composer

```

#### 安装依赖

```
composer install --prefer-dist --optimize-autoloader --no-dev
```

#### 导入数据库

```
#5.7+
php artisan migrate --seed

#5.5-5.6
cp database/migrations/5.6/* database/migrations
php artisan migrate --seed

```

#### 环境设置

```

php artisan key:generate
php artisan storage:link
chown -R www:www storage/ 
chmod -R 777 storage/

```

#### 设置定时任务

```
crontab -e -u www

添加
* * * * * php /www/wwwroot/你的域名/artisan schedule:run >> /dev/null 2>&1
```

#### 设置邮件

```

MAIL_DRIVER=smtp #或使用 mailgun
# SMTP设置
MAIL_HOST=smtp.exmail.qq.com
MAIL_PORT=465 #SMTP端口
MAIL_USERNAME=admin@proxypanel.ml #使用的邮箱地址
MAIL_PASSWORD=password #SMTP授权码
MAIL_ENCRYPTION=ssl
MAIL_FROM_ADDRESS=admin@proxypanel.ml #用户看到的发件人邮箱地址
MAIL_FROM_NAME=ProxyPanel #发件人名称

# Mailgun设置
MAILGUN_DOMAIN=
MAILGUN_SECRET=

```


#### 更新数据库

```
php artisan migrate

```