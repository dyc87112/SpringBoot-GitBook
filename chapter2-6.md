# 开发工具

这里的开发工具不是IDE，而是Spring Boot提供的一个模块`spring-boot-devtools`，它包含了一套能够帮助我们快速开发调试的效率工具。

我们只需要在Maven配置文件中加入下面依赖就可以使用它。

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

** 
该模块在完整的打包环境下运行的时候会被禁用。如果你使用java -jar启动应用或者用一个特定的classloader启动，它会认为这是一个“生产环境”。
**


## 默认属性



## 自动重启

该工程在spring boot开发过程中非常有用，当工程文件发生变化的时候工程能够自动重启生效变化的内容。

除了引入`spring-boot-devtools`模块之外，还需修改pom.xml如下内容：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <fork>true</fork>
            </configuration>
        </plugin>
    </plugins>
</build>
```

**重启触发机制**

在Eclipse和IntelliJ IDEA中重启的触发机制有所区别：

- Eclipse在保存修改过的文件时触发
- IntelliJ IDEA在build项目的时候触发

**注意不要以java -jar的方式执行，不然不会启用“自动重启”功能，可以用mvn spring-boot:run来运行 **

## 全局设置


## 远程应用

