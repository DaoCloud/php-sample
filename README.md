## 如何开发一个 PHP 的 Dcoker 化应用

目标：基于 PHP 的 Docker 基础镜像，开发一个 Docker 化的实例 PHP 应用 。本项目代码维护在 [DaoCloud/php-sample](https://github.com/DaoCloud/php-sample) 项目中。

> 本次基础镜像使用位于 [Docker Hub](https://github.com/docker-library/official-images/blob/master/library/php) 的 PHP 官方镜像，也可以根据自己的项目需求与环境依赖[定制一个 PHP 基础镜像]()。

### 基于官方镜像

官方镜像维护了自 5.4 版本起的所有 PHP 基础镜像，所有镜像均采用 debian:jessie 作为系统镜像。

首先，选择官方的 php:5.6-cli 镜像作为项目的基础镜像。

```
FROM daocloud.io/php:5.6-cli
```

* 由于示例代码较为简单，采用仅安装 PHP CLI 的 Docker 镜像来运行。

> 因所有镜像均位于境外服务器，为了确保所有示例能正常运行，DaoCloud 提供了一套境内镜像源，并与官方源保持同步。

接着，将代码复制到目标目录。

```
add . /app
WORKDIR /app
CMD [ "php", "./hello.php" ]
```

* `ADD` 与 `COPY` 的区别，总体来说 `ADD` 和 `COPY` 没有什么区别，只能说 `ADD` 比 `COPY` 能做的更多，`ADD` 允许后面的参数为 URL ，还有 `ADD` 添加的文件为压缩包的话，它将自动解压。
* `CMD` 为本次构建出来的镜像运行起来时候默认执行的，我们可以通过 docker 命令修改默认运行命令。
* Dockfile 具体语法请参考：[Dockerfile](https://docs.docker.com/reference/builder/)。

最后，让我们运行这个示例代码。

```
Welcome the world of Docker !
```

* 如果看到这段字符串，那么就说明你成功进入到了一个 docker 的世界。

欢迎来到 Docker 的世界，这个世界有你意想不到的精彩！






#[需要]
* php-apache-sample repo
* daocloud hub上的相关image
* 示例代码过于简单

`./hello.php`
```
<?php

echo 'Hello World';
```

`./Dockerfile`
```
FROM php:5.6-cli

COPY . /app
WORKDIR /app
CMD [ "php", "./hello.php" ]
```