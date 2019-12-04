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



## 二、用 Docker 打包镜像

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

3. 将 jar 包打包为镜像`docker build -t boot/docker .`

4. 测试运行镜像`docker run --name spring-boot-test -d -p 8080:8080 boot/docker`

	运行后,可以访问到 Spring Boot 项目(http://{运行镜像的主机IP}:8080)




## 三、与 mysql 容器互联

1. 下载 mysql  镜像 `docker pull mysql:5.7`

2. 运行 mysql 镜像

	```
	 docker run --name db1 -d -p 33061:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7
	```

3. 容器互联

	```
	docker run --name boot_docker --link db1:db1 -d -p 8080:8080 boot/docker
	
	-p 端口映射
	--name 本镜像名称
	--link db1 第一个参数为运行 mysql 镜像后容器的名称，db1 第二个参数为别名，此处和 application.properties 文件中连接mysql的地址保持一致 
	boot/docker 刚刚 build 的 java 项目镜像名称
	
	```

	![sb_application_jdbc](\images\posts\Dock部署SpringBoot项目\sb_application_jdbc.png)



## 四、完成 spring boot 部署

![ant-demo](\images\posts\Dock部署SpringBoot项目\ant-demo.png)