---
title: 初学者指南
link: https://docshome.gitbook.io
draft: true
---
# 初学者指南

本指南旨在介绍 Nginx 基本内容和一些在 Nginx 上可以完成的简单任务。这里假设您已经安装了 nginx，否则请参阅 [安装 nginx ](https://docshome.gitbook.io/nginx-docs/readme/an-zhuang-nginx) 页面。 本指南介绍如何启动、停止 nginx 和重新加载配置，解释配置文件的结构，并介绍如何设置 nginx 以提供静态内容服务，如何配置 nginx 作为代理服务器，以及如何将其连接到一个 FastCGI 应用程序。

nginx 有一个主进程（Master）和几个工作进程（Worker）。主进程的主要目的是读取和评估配置，并维护工作进程。工作进程对请求进行处理。nginx 采用了基于事件模型和依赖于操作系统的机制来有效地在工作进程之间分配请求。工作进程的数量可在配置文件中定义，并且可以针对给定的配置进行修改，或者自动调整到可用 CPU 内核的数量（请参阅 worker_processes）。

配置文件决定了 nginx 及其模块的工作方式。默认情况下，配置文件名为 `nginx.conf`，并放在目录 `/usr/local/nginx/conf`，`/etc/nginx` 或 `/usr/local/etc/nginx` 中。

## 启动、停止和重新加载配置

要启动 nginx，需要运行可执行文件。nginx 启动之后，可以通过调用可执行文件附带 `-s 参数` 来控制它。 使用以下语法：

复制

```
nginx -s 信号
```

信号可能是以下之一：

- 

    stop - 立即关闭

- 

    quit - 正常关闭

- 

    reload - 重新加载配置文件

- 

    reopen - 重新打开日志文件

例如，要等待工作进程处理完当前的请求才停止 nginx 进程，可以执行以下命令：

复制

```
nginx -s quit
```

> 这个命令的执行用户应该是与启动nginx用户是一致的

在将重新加载配置的命令发送到 nginx 或重新启动之前，配置文件所做的内容更改将不会生效。要重新加载配置，请执行：

复制

```
nginx -s reload
```

一旦主进程（Master）收到要重新加载配置（reload）的信号，它将检查新配置文件的语法有效性，并尝试应用其中提供的配置。如果成功，主进程将启动新的工作进程（Worker），并向旧工作进程发送消息，请求它们关闭。否则，主进程回滚更改，并继续使用旧配置。旧工作进程接收到关闭命令后，停止接受新的请求连接，并继续维护当前请求，直到这些请求都被处理完成之后，旧工作进程将退出。

可以借助 Unix 工具（如 kill 工具）将信号发送到 nginx 进程，信号直接发送到指定进程 ID 的进程。默认情况下，nginx 主进程的进程 ID 是写入在 `/usr/local/nginx/logs` 或 `/var/run` 中的 nginx.pid 文件中。例如，如果主进程 ID 为 1628，则发送 QUIT 信号让 nginx 正常平滑关闭，可执行：

复制

```
kill -s QUIT 1628
```

获取所有正在运行的 nginx 进程列表，可以使用 `ps` 命令，如下：

复制

```
ps -ax | grep nginx
```

有关向 nginx 发送信号的更多信息，请参阅 [控制 nginx](https://docshome.gitbook.io/nginx-docs/readme/kong-zhi-nginx)。

## 配置文件结构

nginx 是由配置文件中指定的指令控制模块组成。指令可分为简单指令和块指令。一个简单的指令是由空格分隔的名称和参数组成，并以分号 `;` 结尾。块指令具有与简单指令相同的结构，但不是以分号结尾，而是以大括号`{}`包围的一组附加指令结尾。如果块指令的大括号内部可以有其它指令，则称这个块指令为上下文（例如：[events](http://nginx.org/en/docs/ngx_core_module.html#events)，[http](http://nginx.org/en/docs/http/ngx_http_core_module.html#http)，[server](http://nginx.org/en/docs/http/ngx_http_core_module.html#server) 和 [location](http://nginx.org/en/docs/http/ngx_http_core_module.html#location)）。

配置文件中被放置在任何上下文之外的指令都被认为是主上下文 [main](http://nginx.org/en/docs/ngx_core_module.html)。`events` 和 `http` 指令在主 `main` 上下文中，`server` 在 `http` 中，`location` 又在 `server` 中。

井号 `#` 之后的行的内容被视为注释。

## 提供静态内容服务

Web 服务器的一个重要任务是提供文件（比如图片或者静态 HTML 页面）服务。您将实现一个示例，根据请求，将提供来自不同的本地目录的文件： `/data/www`（可能包含 HTML 文件）和 `/data/images`（包含图片）。这需要编辑配置文件，在 `http` 中配置一个包含两个 `location` 块的 `server` 块指令。

首先，创建 `/data/www` 目录将包含任何文本内容的 `index.html` 文件放入其中，创建 `/data/images` 目录然后放一些图片进去。

其次，打开这个配置文件， 默认配置文件已经包含几个服务器块示例，大部分是已经注释掉的。现在注释掉这些块并且启动一个新的 `server` 块。

复制

```
http {
    server {
    }
}
```

通常，配置文件可以包含几个由监听 [listen](http://nginx.org/en/docs/http/ngx_http_core_module.html#listen) 端口和服务器域名 [server names](http://nginx.org/en/docs/http/server_names.html) 区分的 `server` 块指令 [distinguished](http://nginx.org/en/docs/http/request_processing.html)。一旦 nginx 决定由哪个 `server` 来处理请求，它会根据 `server` 块中定义的 `location` 指令的参数来检验请求头中指定的URI。

添加如下 `location` 块指令到 `server` 块指令中：

复制

```
location / {
    root /data/www;
}
```

该 `location` 块指令指定 `/` 前缀与请求中的 URI 相比较。对于匹配的请求，URI 将被添加到根指令 [root](http://nginx.org/en/docs/http/ngx_http_core_module.html#root) 中指定的路径，即 `/data/ www`，以形成本地文件系统上所请求文件的路径。如果有几个匹配上的 `location` 块指令，nginx 将选择具有最长前缀的 `location` 块。上面的位置块提供最短的前缀，长度为 1，因此只有当所有其它 `location` 块不能匹配时，才会使用该块。

接下来，添加第二个 `location` 指令快：

复制

```
location /images/ {
    root /data;
}
```

以 `/images/` 为开头的请求将会被匹配上（虽然 `location /` 也能匹配上此请求，但是它的前缀更短）

最后，`server` 块指令应如下所示：

复制

```
server {
    location / {
        root /data/www;
    }

    location /images/ {
        root /data;
    }
}
```

这已经是一个监听标准 80 端口并且可以在本地机器上通过 `http://localhost/` 地址来访问的有效配置。响应以 `/images/` 开头的URI请求，服务器将从 `/data/images` 目录发送文件。例如，响应`http://localhost/images/example.png` 请求，nginx 将发送 `/data/images/example.png` 文件。如果此文件不存在，nginx 将发送一个404错误响应。不以 `/ images/` 开头的 URI 的请求将映射到 `/data/www` 目录。例如，响应 `http://localhost/some/example.html` 请求，nginx 将发送 `/data/www/some/example.html` 文件。

要让新配置立刻生效，如果 nginx 尚未启动可以启动它，否则通过执行以下命令将重新加载配置信号发送到 nginx 的主进程：

复制

```
nginx -s reload
```

> 如果运行的效果没有在预期之中，您可以尝试从 `/usr/local/nginx/logs` 或 `/var/log/ nginx` 中的 `access.log` 和 `error.log` 日志文件中查找原因。

## 设置一个简单的代理服务器

nginx 的一个常见用途是作为一个代理服务器，作用是接收请求并转发给被代理的服务器，从中取得响应，并将其发送回客户端。

我们将配置一个基本的代理服务器，它为图片请求提供的文件来自本地目录，并将所有其它请求发送给代理的服务器。在此示例中，两个服务器在单个 nginx 实例上定义。

首先，通过向 nginx 的配置文件添加一个 `server` 块来定义代理服务器，其中包含以下内容：

复制

```
server {
    listen 8080;
    root /data/up1;

    location / {
    }
}
```

这是一个监听 8080 端口的简单服务器（以前，由于使用了标准 80 端口，所以没有指定 listen 指令），并将所有请求映射到本地文件系统上的 `/data/up1` 目录。创建此目录并将 `index.html` 文件放入其中。请注意，`root` 指令位于 `server` 上下文中。当选择用于处理请求的 `location` 块自身不包含 `root` 指令时，将使用此 `root` 指令。

接下来，在上一节中的服务器配置基础上进行修改，使其成为代理服务器配置。在第一个 `location` 块中，使用参数指定的代理服务器的协议，域名和端口（在本例中为 `http://localhost:8080`）放置在 [proxy_pass](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass) 指令处：

复制

```
server {
    location / {
        proxy_pass http://localhost:8080;
    }

    location /images/ {
        root /data;
    }
}
```

我们将修改使用了 `/images/` 前缀将请求映射到 `/data/images` 目录下的文件的第二个 `location` 块，使其与附带常见的图片文件扩展名的请求相匹配。修改后的 `location` 块如下所示：

复制

```
location ~ \.(gif|jpg|png)$ {
    root /data/images;
}
```

该参数是一个正则表达式，匹配所有以`.gif`，`.jpg` 或 `.png` 结尾的 URI。正则表达式之前应该是 `~`。相应的请求将映射到 `/data/images` 目录。

当 nginx 选择一个 `location` 块来提供请求时，它首先检查指定前缀的 [location](http://nginx.org/en/docs/http/ngx_http_core_module.html#location) 指令，记住具有最长前缀的 `location`，然后检查正则表达式。如果与正则表达式匹配，nginx 会选择此 `location`，否则选择更早之前记住的那一个。

代理服务器的最终配置如下：

复制

```
server {
    location / {
        proxy_pass http://localhost:8080/;
    }

    location ~ \.(gif|jpg|png)$ {
        root /data/images;
    }
}
```

此 `server` 将过滤以 `.gif`，`.jpg` 或 `.png` 结尾的请求，并将它们映射到 `/data/images` 目录（通过向 root 指令的参数添加 URI），并将所有其它请求传递到上面配置的代理服务器。

要使新配置立即生效，请将重新加载配置文件信号（reload）发送到 nginx，如前几节所述。

还有更多的指令可用于进一步配置代理连接。

## 设置 FastCGI 代理

nginx 可被用于将请求路由到运行了使用各种框架和 PHP 等编程语言构建的应用程序的 FastCGI 服务器。

与 FastCGI 服务器协同工作的最基本的 nginx 配置是使用 [fastcgi_pass](http://nginx.org/en/docs/http/ngx_http_fastcgi_module.html#fastcgi_pass) 指令而不是 `proxy_pass` 指令，以及 `fastcgi_param` 指令来设置传递给 FastCGI 服务器的参数。假设 FastCGI 服务器可以在 localhost:9000 上访问。以上一节的代理配置为基础，用 `fastcgi_pass` 指令替换 `proxy_pass` 指令，并将参数更改为 `localhost:9000`。在 PHP 中，`SCRIPT_FILENAME` 参数用于确定脚本名称，`QUERY_STRING` 参数用于传递请求参数。最终的配置将是：

复制

```
server {
    location / {
        fastcgi_pass  localhost:9000;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param QUERY_STRING    $query_string;
    }

    location ~ \.(gif|jpg|png)$ {
        root /data/images;
    }
}
```

这里设置一个 `server`，将除了静态图片请求之外的所有请求路由到通过 FastCGI 协议在 `localhost:9000` 上运行的代理服务器。

## 原文档

- 

    http://nginx.org/en/docs/beginners_guide.html