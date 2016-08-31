# 工程结构

Spring Boot框架本身并没有对工程结构有特别的要求，但是按照最佳实践的工程结构可以帮助我们减少可能会遇见的坑，并且您会在后面章节中体会到该工程结构可以免去不少特殊的配置工作。


## 典型示例

- root package结构：`com.example.myproject`
- 应用主类`Application.java`置于root package下，通常我们会在应用主类中做一些框架配置扫描等配置，我们放在root package下可以帮助程序减少手工配置来加载到我们希望被Spring加载的内容
- 实体（Entity）与数据访问层（Repository）置于`com.example.myproject.domain`包下
- 逻辑层（Service）置于`com.example.myproject.service`包下
- Web层（web）置于`com.example.myproject.controller`包下


```
com
  +- example
    +- myproject
      +- Application.java
      |
      +- domain
      |  +- Customer.java
      |  +- CustomerRepository.java
      |
      +- service
      |  +- CustomerService.java
      |
      +- web
      |  +- CustomerController.java
      |
      
```

