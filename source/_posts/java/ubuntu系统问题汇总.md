---
title: ubuntu系统问题汇总
author: pzc
date: 2025-05-19
cover: /assets/images/jpg/156.jpg
categories: [java]
tags: [Backend,Server]
---

## compiler cc is not found

这个错误表明系统中缺少 C 编译器（`gcc` 或 `clang`）。在 Linux 系统中，编译 Nginx 和相关模块需要一个 C 编译器。以下是解决方法：

### 安装 C 编译器

在 Ubuntu 或 Debian 系统上，运行以下命令安装 `gcc`（GNU C Compiler）：

```bash
sudo apt update
sudo apt install build-essential
```

`build-essential` 包含了 `gcc`、`g++` 和其他编译工具。

在 CentOS 或 RHEL 系统上，运行以下命令：

```bash
sudo yum groupinstall "Development Tools"
```

### 安装完成后重新运行 `./configure`

安装完成后，返回到 Nginx 源码目录，重新运行 `./configure` 命令：

```bash
cd ~/nginx-1.28.0
./configure --add-module=../nginx-http-flv-module
```

如果还有其他依赖问题，`./configure` 会提示缺少的库，按照提示安装即可。例如，如果提示缺少 `pcre`、`zlib` 或 `openssl`，可以按照以下命令安装：

- 在 Ubuntu 或 Debian 上：

  ```bash
  sudo apt install libpcre3 libpcre3-dev zlib1g-dev openssl libssl-dev
  ```

- 在 CentOS 或 RHEL 上：

  ```bash
  sudo yum install pcre-devel zlib-devel openssl-devel
  ```

完成这些步骤后，重新运行 `./configure`，应该可以正常通过。



## Ubuntu 查看IP地址

在 Ubuntu 系统中，可以通过多种方式查看 IP 地址。以下是一些常用的方法：

### 1. **使用 `ifconfig` 命令**

虽然 `ifconfig` 在某些现代 Linux 发行版中可能不再默认安装，但可以通过安装 `net-tools` 包来使用它。

#### 安装 `net-tools`：

```bash
sudo apt update
sudo apt install net-tools
```

#### 查看 IP 地址：

```bash
ifconfig
```

输出示例：

```
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::a00:27ff:fe00:1  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:00:00:01  txqueuelen 1000  (Ethernet)
        RX packets 12345  bytes 12345678 (11.7 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 12345  bytes 12345678 (11.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 12345  bytes 12345678 (11.7 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 12345  bytes 12345678 (11.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

- **IPv4 地址**：在 `inet` 后面的地址（例如 `192.168.1.100`）。
- **IPv6 地址**：在 `inet6` 后面的地址（例如 `fe80::a00:27ff:fe00:1`）。

### 2. **使用 `ip` 命令**

`ip` 是一个更现代的工具，功能更强大，通常默认安装在大多数 Linux 发行版中。

#### 查看 IP 地址：

```bash
ip addr show
```

输出示例：

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:00:00:01 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.100/24 brd 192.168.1.255 scope global dynamic eth0
       valid_lft 86399sec preferred_lft 86399sec
    inet6 fe80::a00:27ff:fe00:1/64 scope link 
       valid_lft forever preferred_lft forever
```

- **IPv4 地址**：在 `inet` 后面的地址（例如 `192.168.1.100/24`）。
- **IPv6 地址**：在 `inet6` 后面的地址（例如 `fe80::a00:27ff:fe00:1/64`）。

### 3. **查看特定网络接口的 IP 地址**

如果你只想查看某个特定网络接口（例如 `eth0` 或 `wlan0`）的 IP 地址，可以使用以下命令：

#### 使用 `ip` 命令：

```bash
ip addr show eth0
```

#### 使用 `ifconfig` 命令：

```bash
ifconfig eth0
```

### 4. **查看公网 IP 地址**

如果你需要查看公网 IP 地址（即从外部网络看到的 IP 地址），可以使用以下命令：

```bash
curl ifconfig.me
```

或者：

```bash
curl checkip.amazonaws.com
```

这些命令会返回你的公网 IP 地址。

### 总结

- 使用 `ifconfig`（需要安装 `net-tools`）。
- 使用 `ip addr show`（推荐，现代工具）。
- 使用 `curl` 查看公网 IP 地址。

根据你的需求选择合适的方法即可！

## 查看ngnix模块情况

在 Nginx 中，可以通过多种方式查看已加载的模块情况。以下是几种常用的方法：

### 1. **使用 `nginx -V` 命令**

运行以下命令可以查看 Nginx 的编译参数和已编译的模块：

```bash
nginx -V
```

#### 示例输出：

```
nginx version: nginx/1.28.0
built with OpenSSL 1.1.1f  31 Mar 2020
TLS SNI support enabled
configure arguments: --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_random_index_module --with-http_secure_link_module --with-http_stub_status_module --with-http_auth_request_module --with-http_xslt_module=dynamic --with-http_image_filter_module=dynamic --with-http_geoip_module=dynamic --with-http_perl_module=dynamic --add-module=../nginx-http-flv-module
```

- **`nginx version`**：显示 Nginx 的版本。
- **`configure arguments`**：显示编译 Nginx 时使用的参数，包括所有已编译的模块（如 `--with-http_ssl_module`、`--add-module=../nginx-http-flv-module` 等）。

### 2. **查看运行时加载的模块**

如果你使用的是动态模块（`.so` 文件），可以通过以下命令查看运行时加载的模块：

```bash
nginx -T
```

#### 示例输出：

```
# configuration file /usr/local/nginx/conf/nginx.conf:
events {
    worker_connections  1024;
}

rtmp {
    server {
        listen 1935;  # 接受推流的端口号
        chunk_size 8192; # 单一推流数据包的最大容量？

        application mlive { # mlive 模块，可以自行更换名字
            live on; # 打开直播
            meta off; # 为了兼容网页前端的 flv.js，设置为 off 可以避免报错
            gop_cache on; # 支持GOP缓存，以减少首屏时间
            allow play all; # 允许来自任何 ip 的人拉流
        }
    }
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       80;  # http 服务的端口
        server_name  localhost;

        location / {
            root   html;
            index  index.html index.htm;
            flv_live on; # 打开 http-flv 服务
            chunked_transfer_encoding on;
            add_header 'Access-Control-Allow-Origin' '*'; # 允许跨域
            add_header 'Access-Control-Allow-Credentials' 'true';
        }
    }
}

# modules
load_module modules/ngx_http_perl_module.so;
load_module modules/ngx_http_image_filter_module.so;
```

- **`load_module`**：显示运行时加载的动态模块。

### 3. **查看模块是否生效**

可以通过查看 Nginx 的配置文件来确认模块是否被正确加载和配置。例如，如果你加载了 `nginx-http-flv-module`，可以在配置文件中查找相关的指令：

```nginx
location /live {
    flv_live on;
}
```

如果配置文件中包含这些指令，说明模块已经生效。

### 4. **通过日志确认模块功能**

如果模块涉及特定功能（如日志记录、特定请求处理等），可以通过查看 Nginx 的日志文件来确认模块是否正常工作。例如，`nginx-http-flv-module` 会在推流或拉流时记录相关日志。

### 总结

- 使用 `nginx -V` 查看编译时的模块列表。
- 使用 `nginx -T` 查看运行时加载的动态模块。
- 查看配置文件确认模块是否被正确配置。
- 查看日志文件确认模块功能是否正常。

通过这些方法，你可以全面了解 Nginx 的模块加载情况。

## Command 'nginx' not found, but can be installed with:

当你在终端中运行 `nginx` 命令时，看到类似这样的提示：

```
Command 'nginx' not found, but can be installed with:
```

这表明你的系统中尚未安装 Nginx，或者 Nginx 的可执行文件路径没有被正确添加到系统的环境变量中。

以下是解决这个问题的几种方法：

### 方法 1：安装 Nginx

如果你尚未安装 Nginx，可以通过以下步骤安装它。

#### 在 Ubuntu/Debian 系统上安装 Nginx

1. 更新软件包列表：

   ```bash
   sudo apt update
   ```

2. 安装 Nginx：

   ```bash
   sudo apt install nginx
   ```

#### 在 CentOS/RHEL 系统上安装 Nginx

1. 安装 EPEL 仓库（如果尚未安装）：

   ```bash
   sudo yum install epel-release
   ```

2. 安装 Nginx：

   ```bash
   sudo yum install nginx
   ```

安装完成后，运行以下命令检查 Nginx 是否正常运行：

```bash
sudo systemctl start nginx
sudo systemctl status nginx
```

### 方法 2：检查 Nginx 的安装路径

如果你已经安装了 Nginx，但仍然看到这个错误，可能是因为 Nginx 的可执行文件路径没有被添加到系统的环境变量中。

#### 查找 Nginx 的安装路径

运行以下命令查找 Nginx 的可执行文件路径：

```bash
which nginx
```

或者：

```bash
find / -name nginx 2>/dev/null
```

如果找到了路径（例如 `/usr/local/nginx/sbin/nginx`），可以将其添加到系统的环境变量中。

#### 添加到环境变量

1. 编辑你的 shell 配置文件（如 `.bashrc` 或 `.zshrc`）：

   ```bash
   nano ~/.bashrc
   
   ```

2. 在文件末尾添加以下行（假设 Nginx 的可执行文件路径是 `/usr/local/nginx/sbin/nginx`）：

   ```bash
   export PATH=$PATH:/usr/local/nginx/sbin
   ```

3. 保存文件并重新加载配置：

   ```bash
   source ~/.bashrc
   ```

### 方法 3：检查是否正确编译安装了 Nginx

如果你是从源码编译安装的 Nginx，可能在安装过程中没有正确设置路径。

#### 检查编译时的安装路径

在编译 Nginx 时，`./configure` 命令会指定安装路径。默认情况下，Nginx 会被安装到 `/usr/local/nginx` 目录。你可以通过以下命令检查：

```bash
./configure --help
```

查看是否有 `--prefix` 参数。

#### 确保 Nginx 可执行文件路径正确

如果你使用了自定义路径（如 `--prefix=/path/to/nginx`），请确保该路径下的 `sbin/nginx` 文件存在。然后按照 **方法 2** 中的步骤将其路径添加到环境变量中。

### 方法 4：重新安装 Nginx

如果上述方法都无法解决问题，建议重新安装 Nginx。你可以选择从源码重新编译安装，或者直接使用系统包管理器安装（推荐）。

#### 从源码重新编译安装

1. 下载 Nginx 源码并解压。

2. 运行 `./configure`，确保指定正确的路径（如 `--prefix=/usr/local/nginx`）。

3. 编译并安装：

   ```bash
   make
   sudo make install
   ```

4. 将 Nginx 的可执行文件路径添加到环境变量中（如 `/usr/local/nginx/sbin`）。

#### 使用系统包管理器安装

直接使用系统包管理器安装 Nginx（如 `apt` 或 `yum`），避免手动编译带来的问题。

### 总结

- 如果尚未安装 Nginx，请使用系统包管理器安装。
- 如果已经安装，但无法找到 `nginx` 命令，请检查 Nginx 的安装路径，并将其添加到环境变量中。
- 如果仍然有问题，建议重新安装 Nginx，确保路径正确。



## 启动nginx

启动 Nginx 的方法取决于你是通过系统包管理器安装的 Nginx，还是从源码编译安装的 Nginx。以下是两种情况下的启动方法：

### 1. **通过系统包管理器安装的 Nginx**

如果你是通过 `apt`（Ubuntu/Debian）或 `yum`（CentOS/RHEL）安装的 Nginx，可以使用 `systemctl` 命令来管理 Nginx 服务。

#### 启动 Nginx

```bash
sudo systemctl start nginx
```

#### 检查 Nginx 是否成功启动

```bash
sudo systemctl status nginx
```

如果 Nginx 正常运行，你会看到类似以下的输出：

```
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2025-05-18 12:00:00 UTC; 1min ago
   Main PID: 1234 (nginx)
      Tasks: 2 (limit: 4915)
     Memory: 1.5M
     CGroup: /system.slice/nginx.service
             ├─1234 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             └─1235 nginx: worker process
```

#### 设置 Nginx 开机自启

如果你希望 Nginx 在系统启动时自动运行，可以运行以下命令：

```bash
sudo systemctl enable nginx
```

### 2. **从源码编译安装的 Nginx**

如果你是从源码编译安装的 Nginx，通常需要手动启动 Nginx。

#### 启动 Nginx

假设 Nginx 被安装到了默认路径 `/usr/local/nginx`，可以使用以下命令启动：

```bash
sudo /usr/local/nginx/sbin/nginx
```

#### 检查 Nginx 是否成功启动

可以通过访问 Nginx 的默认页面来检查是否成功启动。在浏览器中输入：

```
http://<你的服务器IP地址>
```

如果看到 Nginx 的欢迎页面，说明 Nginx 已成功启动。

#### 停止 Nginx

如果需要停止 Nginx，可以使用以下命令：

```bash
sudo /usr/local/nginx/sbin/nginx -s stop
```

#### 重启 Nginx

如果需要重启 Nginx，可以使用以下命令：

```bash
sudo /usr/local/nginx/sbin/nginx -s reload
```

### 3. **检查 Nginx 配置文件**

在启动 Nginx 之前，建议检查配置文件是否有语法错误。可以使用以下命令进行检查：

```bash
sudo nginx -t
```

如果配置文件没有问题，你会看到类似以下的输出：

```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

### 4. **防火墙设置**

如果你的服务器启用了防火墙，确保防火墙允许 HTTP（端口 80）和 HTTPS（端口 443）流量。

#### 在 Ubuntu/Debian 上设置防火墙

```bash
sudo ufw allow 'Apache Full'
```

#### 在 CentOS/RHEL 上设置防火墙

```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
```

### 总结

- 如果通过系统包管理器安装，使用 `systemctl` 命令管理 Nginx 服务。
- 如果从源码编译安装，手动启动 Nginx。
- 检查配置文件是否有语法错误。
- 确保防火墙允许 HTTP 和 HTTPS 流量。

按照这些步骤操作后，你应该能够成功启动 Nginx 并访问其服务。



## Could not save the file “/usr/local/nginx/conf/nginx.conf”.

出现“Could not save the file `/usr/local/nginx/conf/nginx.conf`”的错误，通常是因为当前用户没有足够的权限来编辑或保存该文件。在 Linux 系统中，`/usr/local/nginx/conf/nginx.conf` 文件通常属于 `root` 用户，普通用户无法直接对其进行修改。以下是解决此问题的几种方法：

### 方法 1：使用 `sudo` 命令

如果你需要编辑 Nginx 的配置文件，可以使用 `sudo` 命令以管理员权限打开文件。例如，使用 `nano` 或 `vi` 编辑器：

```bash
sudo nano /usr/local/nginx/conf/nginx.conf
```

或者：

```bash
sudo vi /usr/local/nginx/conf/nginx.conf
```

通过 `sudo`，你可以以 `root` 用户的权限编辑文件并保存更改。

### 方法 2：更改文件权限（不推荐）

虽然可以通过更改文件权限来允许普通用户编辑该文件，但这种方法并不推荐，因为它可能会带来安全风险。如果你仍然需要尝试，可以运行以下命令：

```bash
sudo chmod 666 /usr/local/nginx/conf/nginx.conf
```

这会将文件权限设置为允许所有用户读写。编辑完成后，建议将权限恢复为默认值：

```bash
sudo chmod 644 /usr/local/nginx/conf/nginx.conf
```

### 方法 3：使用图形界面编辑器（如果适用）

如果你正在使用图形界面（如 GNOME、KDE 等），可以通过图形界面的文本编辑器以管理员权限打开文件。例如，在 GNOME 中，可以使用以下命令：

```bash
gksudo gedit /usr/local/nginx/conf/nginx.conf
```

或者在 KDE 中：

```bash
kdesudo kate /usr/local/nginx/conf/nginx.conf
```

这些命令会提示你输入管理员密码，然后以管理员权限打开文件。

### 方法 4：检查文件锁

在某些情况下，文件可能被其他进程锁定，导致无法保存。你可以通过以下命令检查是否有进程正在使用该文件：

```bash
sudo lsof /usr/local/nginx/conf/nginx.conf
```

如果有进程正在使用该文件，可以尝试停止相关进程后再进行编辑。

### 方法 5：检查磁盘空间

确保你的系统有足够的磁盘空间。如果磁盘空间不足，也可能导致无法保存文件。运行以下命令检查磁盘空间：

```bash
df -h
```

如果磁盘空间不足，需要清理一些不必要的文件或扩展磁盘空间。

### 方法 6：检查文件系统错误

在某些情况下，文件系统错误可能导致无法保存文件。运行以下命令检查文件系统：

```bash
sudo fsck -n
```

这将检查文件系统并报告任何错误。如果发现错误，可能需要进一步修复。

### 总结

最推荐的方法是使用 `sudo` 命令以管理员权限编辑文件。例如：

```bash
sudo nano /usr/local/nginx/conf/nginx.conf
```

或者：

```bash
sudo vi /usr/local/nginx/conf/nginx.conf
```

编辑完成后，保存文件并退出编辑器。如果你仍然遇到问题，请提供更多详细信息以便进一步排查。