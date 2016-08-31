# 依赖注入

在Spring Boot中可以自由的使用Spring的注解来定义bean和进行依赖注入配置。

在配置文件中我们可以通过`@ComponentScan`配置来发现和创建bean，在关联类中通过`@Autowired`来注入bean。

**如果你的工程结构是按上一节中的建议来构建的（主函数配置与root package下），那么`@ComponentScan`就不需要配置任何参数。你应用中的所有配置的构建（`@Component`,`@Service`,`@Repository`,`@Controller`等）都会自动地被注册为Spring Bean**

```
欠你一个例子！！







```


具体的Spring IOC详见Spring Framework文档。
