---
title: 使用heroku搭建shadowsocks
date: 2017-04-20 19:51:22
tags: [heroku,shadowsocks]
categories: "shadowsocks"
---


## 使用heroku搭建shadowsocks


### 注册heroku.com

heroku官网注册: [www.heroku.com](https://www.heroku.com)


### 下载安装Heroku CLI

![下载安装](/images/posts/heroku-cli.png)


### 登录heroku

``` bash
$ heroku login
Enter your Heroku credentials.
Email: example@example.com
Password:
...
```

更多: [开始heroku](https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up)

### 创建heroku应用

``` bash
$ heroku create app-name
```


### 下载Shadowsocks的Heroku专版，准备应用程序

``` bash
$ git clone https://github.com/mrluanma/shadowsocks-heroku.git
$ cd shadowsocks-heroku
$ git init
$ git commit -m "init"
```

### 添加remote

``` bash
$ heroku git:remote -a app-name
```


### 推送到heroku

``` bash
$ heroku push heroku master
```


### 设置加密方法和密码，如：heroku config:set METHOD=rc4 KEY=PASSWORD
    
#### 加密方法推荐rc4和aes-256-cfb

``` bash
$ heroku config:set METHOD=加密方法 KEY=密码
```

#### 运行，如：node local.js -s appname.herokuapp.com -l 1080 -m rc4 -k PASSWORD

``` bash
$ node local.js -s 应用名称.herokuapp.com -l 本地端口 -m 加密方法 -k
```
    
    修改代理设置 SOCKS5 127.0.0.1:1080
    
[详细介绍](https://github.com/mrluanma/shadowsocks-heroku)


