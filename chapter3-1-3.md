# 静态资源访问

在我们开发Web应用的时候，需要引用大量的js、css、图片等静态资源。

## 默认配置

Spring Boot默认提供静态资源目录位置需置于classpath下，目录名需符合如下规则：

- /static
- /public
- /resources
- /META-INF/resources

举例：我们可以在`src/main/resources/`目录下创建`static`，在该位置放置一个图片文件。启动程序后，尝试访问`http://localhost:8080/D.jpg`。如能显示图片，配置成功。

![静态资源结构](img/chapter3-1-3.png)


## 自定义配置

。。。