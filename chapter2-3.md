# 框架配置

我们在使用Spring的时候，需要做一系列的配置，通常使用XML或者Java来配置。

Spring Boot更偏向于使用Java来进行配置，从本文开始的入门项目中可以看到，就没有出现XML格式的Spring配置文件。

## 加载配置

从入门例子中的主类看，`SpringApplication.run`函数传入的`Chapter1Application.class`类就是要读取的配置类，该函数通过传入配置类来进行Spring的基础配置加载。

```java
@SpringBootApplication
public class Chapter1Application {

	public static void main(String[] args) {
		SpringApplication.run(Chapter1Application.class, args);
	}

}
```

Spring中的配置类需要以`@Configuration`注解修饰，这里的`@SpringBootApplication`能被正常加载，是由于其整合了`@Configuration`，`@Configuration`，`@Configuration`三个注解。

## 多配置文件

从`SpringApplication.run`函数的传参看，可以加载多个配置class，所以框架配置内容不是必须都配置于程序主类之中。

当我们创建多个配置类时，可以有两种方法进行引用：
- 在主类中通过`@Import`注解来引入附加的配置类
- 在主类中配置`@ComponentScan`对附加配置类所在的package进行扫描加载


## 自动配置

Spring Boot自动配置的意图是根据项目中JAR的依赖关系自动配置你的Spring应用程序。例如：当HSQLDB在你的classpath中，并且你没有配置数据源的bean，那么spring boot会自动的为你配置一个嵌入式数据源。

使用自动配置功能：需要在配置类上添加`@EnableAutoConfiguration`或者`@SpringBootApplication`注解。

#### 替代特定的自动配置

Spring Boot的自动配置通常并不能完全覆盖我们实际项目的配置需要，有的时候我们需要定义一些配置来取代自动配置的部分特定内容。例如：我们需要配置一个自己的数据源bean来替代默认嵌入式数据源。

如果你需要找出当前程序用了哪些自动化配置？那么可以通过bebug模式启动，控制台中会记录自动配置的报告。

#### 禁用特定的自动配置

如果你发现有些自动配置内容你不想要，那么你可以通过`@EnableAutoConfiguration`注解来禁用他们

```java
@Configuration 
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class}) 
public class MyConfiguration {

}

```





