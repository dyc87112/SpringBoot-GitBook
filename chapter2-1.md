# 系统构建

## 基本要求：
- Java 7及以上 
- Spring Framework 4.1.5及以上

## 如何支持Java 6

官方建议使用`Java 8`，若一定要使用`Java 6`，我们需要做一些额外的配置。

#### 使用Tomcat
由于Spring Boot默认使用的是`Tomcat 8`，该容器要求`Java 7`版本以上，为了支持`Java 6`我们需要修改tomcat版本为7，通过修改Maven配置文件`pom.xml`，修改内容如下：

```xml
<properties>
    <tomcat.version>7.0.59</tomcat.version>
</properties>
```

#### 使用Jetty
若您使用的是`jetty`,除了加入jetty的版本属性外，还要`spring-boot-starter-web`去除`spring-boot-starter-tomcat`的依赖，再引入`spring-boot-starter-jetty`的依赖，具体下面：

```xml
<properties>
    <jetty.version>8.1.15.v20140411</jetty.version>
    <jetty-jsp.version>2.2.0.v201112011158</jetty-jsp.version>
</properties>

<dependencies>
    <dependency> 
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId> 
        <exclusions>
            <exclusion> 
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-tomcat</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-jetty</artifactId> 
        <exclusions>
            <exclusion>
                <groupId>org.eclipse.jetty.websocket</groupId>
                <artifactId>*</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>
```


## Servlet容器要求

推荐使用以下版本的Servlet容器

| 名称 | Servlet版本 | Java版本 |
| -- | -- | -- |
| Tomcat 8 | 3.1 | Java 7+ |
| Tomcat 7 | 3.0 | Java 6+ |
| Jetty 9 | 3.1 | Java 7+ |
| Jetty 8 | 3.0 | Java 6+ |
| Undertow 1.1 | 3.1 | Java 7+ |

当然，你也可以将Spring Boot应用部署在其他支持Servlet 3.0以上的容器中。






