# 使用JdbcTemplate


Spring Boot中JdbcTemplate是自动配置的，你可以直接使用`@Autowired`来注入到你自己的bean中来使用。

举例：我们在创建`User`表，包含属性`name`、`age`，下面来编写数据访问对象和单元测试用例。

- 定义包含有插入、删除、查询的抽象接口UserService

```java
public interface UserService {

    /**
     * 新增一个用户
     * @param name
     * @param age
     */
    void create(String name, Integer age);

    /**
     * 根据name删除一个用户高
     * @param name
     */
    void deleteByName(String name);

    /**
     * 获取用户总量
     */
    Integer getAllUsers();

    /**
     * 删除所有用户
     */
    void deleteAllUsers();

}
```

- 通过JdbcTemplate实现UserService中定义的数据访问操作


```java
@Service
public class UserServiceImpl implements UserService {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public void create(String name, Integer age) {
        jdbcTemplate.update("insert into USER(NAME, AGE) values(?, ?)", name, age);
    }

    @Override
    public void deleteByName(String name) {
        jdbcTemplate.update("delete from USER where NAME = ?", name);
    }

    @Override
    public Integer getAllUsers() {
        return jdbcTemplate.queryForObject("select count(1) from USER", Integer.class);
    }

    @Override
    public void deleteAllUsers() {
        jdbcTemplate.update("delete from USER");
    }
}
```

- 创建对UserService的单元测试用例，通过创建、删除和查询来验证数据库操作的正确性。

```java

@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(Application.class)
public class ApplicationTests {

	@Autowired
	private UserService userSerivce;

	@Before
	public void setUp() {
		// 准备，清空user表
		userSerivce.deleteAllUsers();
	}

	@Test
	public void test() throws Exception {
		// 插入5个用户
		userSerivce.create("a", 1);
		userSerivce.create("b", 2);
		userSerivce.create("c", 3);
		userSerivce.create("d", 4);
		userSerivce.create("e", 5);

		// 查数据库，应该有5个用户
		Assert.assertEquals(5, userSerivce.getAllUsers().intValue());

		// 删除两个用户
		userSerivce.deleteByName("a");
		userSerivce.deleteByName("e");

		// 查数据库，应该有5个用户
		Assert.assertEquals(3, userSerivce.getAllUsers().intValue());

	}

}

```

*上面介绍的`JdbcTemplate`只是最基本的几个操作，更多其他数据访问操作的使用请参考：[JdbcTemplate API](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/jdbc/core/JdbcTemplate.html)*


通过上面这个简单的例子，我们可以看到在Spring Boot下访问数据库的配置依然秉承了框架的初衷：简单。我们只需要在pom.xml中加入数据库依赖，再到application.properties中配置连接信息，不需要像Spring应用中创建JdbcTemplate的Bean，就可以直接在自己的对象中注入使用。

[本文完整示例](http://git.oschina.net/didispace/SpringBoot-Learning/tree/master)