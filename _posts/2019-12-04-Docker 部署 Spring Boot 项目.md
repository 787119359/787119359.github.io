---
layout: post
title: "Docker 部署 Spring Boot 项目"
date: 2019-12-04
tag: Docker
---

## 一、前提条件

1. 要有一个Spring Boot 项目

	![项目目录结构](\images\posts\Dock部署SpringBoot项目\项目目录结构.png)

2. 编译打包 (mvn clean package) 在 target 目录下生成 jar 包

3. 安装 Docker 



## 二、用 Docker 打包镜像并发布

1. 编写 Dockerfile 文件，创建文件名为 Dockerfile 的文本文件

	```
	FROM java:8-alpine
	
	COPY JavaTest.jar /
	
	WORKDIR /
	
	ENTRYPOINT ["java", "-jar", "JavaTest.jar"]
	
	EXPOSE 8080
	```

	* java:8-alpine  指Docker hub 上官方提供的 java 镜像
	* ENTRYPOINT 应用启动命令 参数设定
	* EXPOSE 容器暴露端口

2. 将 Dockerfile 和 springBootDocker.jar 放在同一目录下

3. 将 jar 包打包为镜像`docker build -t boot-docker .`

4. 运行镜像`docker run --name spring-boot-docker -d -p 8080:8080 java_test`

	运行后,可以访问到 Spring Boot 项目(http://{运行镜像的主机IP}:8080)

	