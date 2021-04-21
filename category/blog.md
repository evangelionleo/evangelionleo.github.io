---
layout: category
title: Blog
slug: blog
description: A category for general blog posts.
---

## 新建子模块

`Maven`多模块下新建子模块流程案例。

1、新建业务模块目录，例如：`ruoyi-war`。

2、在`ruoyi-war`业务模块下新建`pom.xml`文件以及`src\main\java`，`src\main\resources`目录。

![image-20210408141840402](../assets/image-20210408141840402.png)cc

`pom.xml`文件(sample)

![image-20210408141931182](../assets/image-20210408141931182.png)

3、根目录`pom.xml`依赖声明节点`dependencies`中添加依赖

![image-20210408142152930](../assets/image-20210408142152930.png)

4、根目录`pom.xml`模块节点`modules`添加业务模块

![image-20210408142245996](../assets/image-20210408142245996.png)

5、`ruoyi-admin`目录`pom.xml`添加模块依赖

![image-20210408142350241](../assets/image-20210408142350241.png)

6、测试模块

在`ruoyi-test`业务模块添加`com.ruoyi.test`包，新建`TestService.java`

在`ruoyi-admin`新建测试类，调用`helloTest`成功返回`hello`代表成功。s32g2y

