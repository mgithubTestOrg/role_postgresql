# PostgreSQL Notes

组件名称：PostgreSQL  
安装文档：https://www.postgresql.org/docs
配置文档：https://www.postgresql.org/docs  
支持平台： Debian家族 | RHEL家族 | Windows | Kubernetes |Docker  

责任人：cdl

## 概要

RabbitMQ是传统的关系型数据库，应用广泛

## 环境要求

* 程序语言：无
* 应用服务器：无
* 数据库：无
* 依赖组件：无
* 其他：

## 安装说明

主要通过yum/apt安装，PostgreSQL安装与配置要素包括：

* 安装的组件有哪些？
* 默认是否创建操作系统普通用户和数据库用户（密码）？
* 如何开启远程连接？
* 是否创建了数据目录（initdb -D）？

下面基于不同的安装平台，分别进行安装说明。

### CentOS

```shell

```

### Ubuntu

```shell

```

## 路径

* 程序路径：/usr/lib/rabbitmq/lib/rabbitmq_server-*
* 日志路径：/var/log/rabbitmq  
* 配置文件路径：  
* 其他...

## 配置

安装完成后，需要依次完成如下配置

```shell
# Set RabbitMQ
- name: Restart RabbitMQ
  shell: systemctl start rabbitmq-server

- name: Enable the management console of RabbitMQ
  shell: rabbitmq-plugins enable rabbitmq_management

- name: Create administrator for RabbitMQ console
  shell: |
    rabbitmqctl add_user admin admin
    rabbitmqctl set_user_tags admin administrator
```

## 账号密码

### 数据库密码

如果有数据库

* 数据库安装方式：包管理工具自带 or 自行安装
* 账号密码：

### 后台账号

如果有后台账号

* 登录地址
* 账号密码
* 密码修改方案：最好是有命令行修改密码的方案


## 服务

本项目安装后自动生成：rabbitmq-server 服务

备注：如果开机没有服务，程序无法运行的情况下，需要自行编写服务后存放到项目中

服务的模板如下：

```
[Unit]
Description=Redmine
After=nginx.service
[Service]
Environment=RAILS_ENV=production
Type=simple
WorkingDirectory=/data/wwwroot/redmine
ExecStart=/usr/local/bin/puma -b tcp://127.0.0.1:9292 -e production 
User=redmine
[Install]
WantedBy=multi-user.target
```

## 环境变量

列出需要增加的环境变量以及增加环境变量的命令：

* 名称 | 路径

## 版本号

通过如下的命令获取主要组件的版本号: 

```
# Check RabbitMQ version
sudo rabbitmqctl status | grep RabbitMQ*

# Check Erlang version
ls /usr/lib64/erlang
```

## 常见问题

#### 有没有管理控制台？

*http:// 公网 IP:15672* 即可访问控制台，系统默认存在一个无法通过外网访问的guest/guest账号

#### 本项目需要开启哪些端口？

| item      | port  |
| --------- | ----- |
| lustering | 25672 |
| AMQP      | 5672  |
| http      | 15672 |

#### 有没有CLI工具？

有，通过 `rabbitmqctl` 查看工具的说明

#### 是否创建了普通用户？

yum/apt 安装的时候系统自动创建名称为postgres的操作系统用户和数据库管理员用户

## 日志

* 2020-04-14 完成CentOS安装研究
