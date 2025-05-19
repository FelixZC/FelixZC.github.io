---
title: 使用nginx-http-flv-module模块
author: pzc
date: 2025-05-18
cover: /assets/images/jpg/155.jpg
categories: [java]
tags: [Backend,Server]
---

## 宿主环境

Edition	Windows 11 Home
Version	23H2
Installed on	‎10/‎26/‎2022
OS build	22631.5335
Serial number	PF2WST25
Experience	Windows Feature Experience Pack 1000.22700.1081.0

## 虚拟机环境

vmware 16.2.2 build-19200509
## 镜像文件

ubuntu-18.04.6-desktop-amd64

## 安装步骤

要安装带有 `nginx-http-flv-module` 的 Nginx，可以通过以下步骤完成：

### 1. 准备环境
- **安装依赖库**：Nginx 和 `nginx-http-flv-module` 需要一些依赖库，如 PCRE、zlib 和 OpenSSL。在 Linux 上可以使用以下命令安装：
  
  ```bash
  sudo apt install libpcre3 libpcre3-dev zlib1g-dev openssl libssl-dev
  ```
  或者在 CentOS 上使用：
  ```bash
  yum install -y gcc gcc-c++ pcre pcre-devel zlib zlib-devel openssl openssl-devel
  ```

### 2. 下载源码
- **下载 Nginx 源码**：
  ```bash
  wget https://nginx.org/download/nginx-1.28.0.tar.gz
  tar -xzvf nginx-1.28.0.tar.gz
  ```
- **下载 `nginx-http-flv-module` 源码**：
  ```bash
  git clone https://github.com/winshining/nginx-http-flv-module.git
  ```

### 3. 编译安装
- **进入 Nginx 源码目录并配置**：
  ```bash
  cd nginx-1.28.0
  ./configure --add-module=../nginx-http-flv-module
  ```
- **编译并安装**：
  
  ```bash
  make
  sudo make install
  ```

### 4. 配置 Nginx
编辑 Nginx 配置文件 `/usr/local/nginx/conf/nginx.conf`，添加以下配置：
```nginx
http {
    include       mime.types;
    default_type  application/octet-stream;

    server {
        listen       8080;
        server_name  localhost;

        location /live {
            flv_live on;  # 开启 HTTP-FLV 直播功能
            chunked_transfer_encoding on;  # 启用分块传输
            add_header 'Access-Control-Allow-Origin' '*';  # 允许跨域
            add_header 'Access-Control-Allow-Credentials' 'true';
        }
    }
}
```

### 5. 启动 Nginx
- **启动 Nginx**：
  
  ```bash
  sudo /usr/local/nginx/sbin/nginx
  ```
- **检查配置文件是否正确**：
  
  ```bash
  sudo /usr/local/nginx/sbin/nginx -t
  ```

### 6. 测试
- **推流**：使用工具如 OBS 或 FFmpeg 将视频流推送到 Nginx 的 RTMP 服务器。
  
  ```bash
  ffmpeg -re -i input.mp4 -c:v libx264 -preset veryfast -maxrate 3000k -bufsize 6000k -f flv rtmp://127.0.0.1:1935/myapp/stream
  ```
- **拉流**：使用浏览器或播放器访问 `http://127.0.0.1:8080/live?port=1935&app=myapp&stream=stream`。

通过以上步骤，你可以成功搭建一个带有 `nginx-http-flv-module` 的 Nginx 服务器，用于 

## 示例推拉流地址

采用OBS示例

![image-20250518234117264](/assets/images/png/image-20250518234117264.png)

![image-20250518234133274](/assets/images/png/image-20250518234133274.png)

推流地址：rtmp://192.168.199.130:1935/mlive

拉流一：rtmp://192.168.199.130:1935/mlive/ssss
拉流二：http://192.168.199.130:80/mlive?port=1935&app=mlive&stream=ssss

## 参考博客

[通过 nginx 搭建一个基于 http-flv 的直播流媒体服务器 - 黄浩# - 博客园 (cnblogs.com)](https://www.cnblogs.com/hhmm99/p/16050844.html)

## 延迟问题

![image-20250518234237422](/assets/images/png/image-20250518234237422.png)
```
sudo nano /usr/local/nginx/conf/nginx.conf
```
注释下面这行
```
# gop_cache on; # 支持GOP缓存，以减少首屏时间
```
可缩延迟短为2s

## VLC软件测试

![image-20250518234426703](/assets/images/png/image-20250518234426703.png)