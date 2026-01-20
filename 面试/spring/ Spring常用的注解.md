Spring 框架提供了丰富的注解来简化开发和配置。以下是一些常用的 Spring 注解及其说明：

## 核心组件注解

1.  **`@Component`**：
    *   **用途**：标记一个类为 Spring 容器管理的组件。它是所有组件注解的通用形式。
    *   **说明**：当 Spring 进行组件扫描时，会检测到被 `@Component` 及其派生注解（`@Controller`, `@Service`, `@Repository`）标记的类，并将其注册为 Bean。

2.  **`@Controller`**：
    *   **用途**：标记一个类为 Spring MVC 控制器。
    *   **说明**：通常用于处理 Web 请求，返回视图或 JSON/XML 数据。它会自动包含 `@Component` 的功能。

3.  **`@Service`**：
    *   **用途**：标记一个类为业务逻辑层组件。
    *   **说明**：通常用于封装业务逻辑，提供服务层的方法。它会自动包含 `@Component` 的功能。

4.  **`@Repository`**：
    *   **用途**：标记一个类为数据访问层（DAO）组件。
    *   **说明**：通常用于与数据库进行交互，提供数据持久化操作。它会自动包含 `@Component` 的功能，并支持将持久化层的异常转换为 Spring 的 `DataAccessException`。

5.  **`@Configuration`**：
    *   **用途**：标记一个类为配置类，等同于 XML 配置文件。
    *   **说明**：结合 `@Bean` 注解使用，用于定义 Bean 的创建逻辑。

6.  **`@Bean`**：
    *   **用途**：在 `@Configuration` 类的方法上，标记该方法的返回值作为 Spring Bean 注册到容器中。
    *   **说明**：方法的名称通常是 Bean 的名称，方法体中包含了 Bean 的实例化和初始化逻辑。

7.  **`@Autowired`**：
    *   **用途**：用于自动装配 Bean，通过类型匹配进行依赖注入。
    *   **说明**：可以用于构造器、字段、Setter 方法或任意参数方法上。默认情况下是按类型装配，如果发现多个相同类型的 Bean，会尝试根据名称匹配。

8.  **`@Qualifier`**：
    *   **用途**：结合 `@Autowired` 使用，当存在多个相同类型的 Bean 时，指定具体要注入的 Bean 的名称。
    *   **说明**：解决 `NoUniqueBeanDefinitionException` 问题。

9.  **`@Value`**：
    *   **用途**：将外部化配置（如 `application.properties` 或 `application.yml` 中的值）注入到 Bean 的字段或方法参数中。
    *   **说明**：支持 SpEL (Spring Expression Language) 表达式。例如：`@Value("${my.property.name}")`。

## Spring Boot 相关注解

10. **`@SpringBootApplication`**：
    *   **用途**：一个复合注解，包含了 `@SpringBootConfiguration`, `@EnableAutoConfiguration`, `@ComponentScan`。
    *   **说明**：通常用于 Spring Boot 应用的主类上，快速启动和配置 Spring Boot 应用。
        *   `@SpringBootConfiguration`: 标记为配置类。
        *   `@EnableAutoConfiguration`: 启用 Spring Boot 的自动配置机制。
        *   `@ComponentScan`: 启用组件扫描，默认扫描当前包及其子包。

11. **`@EnableAutoConfiguration`**：
    *   **用途**：根据 classpath 和定义的 Bean 自动配置 Spring 应用。
    *   **说明**：Spring Boot 的核心特性之一，极大地简化了配置。

12. **`@ComponentScan`**：
    *   **用途**：指定 Spring 扫描组件的包路径。
    *   **说明**：默认扫描被注解类所在的包及其子包。可以通过 `basePackages` 或 `basePackageClasses` 属性指定其他扫描路径。

## Web/REST 相关注解

13. **`@RequestMapping`**：
    *   **用途**：映射 Web 请求到处理器方法或类。
    *   **说明**：可以指定请求路径、HTTP 方法、请求参数、请求头、媒体类型等。

14. **`@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping`**：
    *   **用途**：是 `@RequestMapping` 的快捷方式，分别用于处理 GET, POST, PUT, DELETE, PATCH 请求。
    *   **说明**：简化了 HTTP 方法的声明。

15. **`@RestController`**：
    *   **用途**：是 `@Controller` 和 `@ResponseBody` 的组合注解。
    *   **说明**：专门用于构建 RESTful Web 服务，所有处理器方法的返回值都会直接写入 HTTP 响应体，而不会解析为视图名称。

16. **`@ResponseBody`**：
    *   **用途**：标记一个方法或类的返回值直接作为 HTTP 响应体，通常用于返回 JSON 或 XML 数据。
    *   **说明**：结合 `@Controller` 使用，或直接使用 `@RestController`。

17. **`@RequestBody`**：
    *   **用途**：将 HTTP 请求体的内容绑定到方法参数上。
    *   **说明**：常用于接收客户端发送的 JSON 或 XML 数据，并将其反序列化为 Java 对象。

18. **`@PathVariable`**：
    *   **用途**：绑定 URI 模板变量到方法参数上。
    *   **说明**：例如：`/users/{id}`，`@PathVariable("id") Long id`。

19. **`@RequestParam`**：
    *   **用途**：绑定 HTTP 请求参数到方法参数上。
    *   **说明**：例如：`/users?name=test`，`@RequestParam("name") String name`。

20. **`@RequestHeader`**：
    *   **用途**：绑定 HTTP 请求头到方法参数上。

21. **`@CookieValue`**：
    *   **用途**：绑定 HTTP Cookie 值到方法参数上。

## AOP 与事务注解

22. **`@Aspect`**：
    *   **用途**：标记一个类为切面。
    *   **说明**：结合 `@Pointcut`, `@Before`, `@After`, `@AfterReturning`, `@AfterThrowing`, `@Around` 等注解来定义切面逻辑。

23. **`@Pointcut`**：
    *   **用途**：定义切入点表达式，指定哪些方法会被拦截。

24. **`@Before`, `@After`, `@AfterReturning`, `@AfterThrowing`, `@Around`**：
    *   **用途**：定义不同类型的通知（advice），在切入点方法执行前、后、返回后、抛出异常时或环绕执行时插入逻辑。

25. **`@EnableAspectJAutoProxy`**：
    *   **用途**：在配置类上启用 Spring 对 AspectJ 风格的 AOP 代理支持。

26. **`@Transactional`**：
    *   **用途**：用于声明式事务管理，标记一个类或方法需要事务支持。
    *   **说明**：可以配置事务的传播行为、隔离级别、只读属性、回滚规则等。

27. **`@EnableTransactionManagement`**：
    *   **用途**：在配置类上启用 Spring 的事务管理功能。

## 生命周期与JSR-250注解

28. **`@PostConstruct`**：
    *   **用途**：标记一个方法，在 Bean 的依赖注入完成之后，执行初始化操作。
    *   **说明**：属于 JSR-250 规范，在 `InitializingBean` 的 `afterPropertiesSet()` 和自定义 `init-method` 之前执行。

29. **`@PreDestroy`**：
    *   **用途**：标记一个方法，在 Bean 被销毁之前，执行清理操作。
    *   **说明**：属于 JSR-250 规范，在 `DisposableBean` 的 `destroy()` 和自定义 `destroy-method` 之前执行。

## 异步处理注解

30. **`@Async`**：
    *   **用途**：标记一个方法为异步执行。
    *   **说明**：Spring 会在单独的线程中执行被 `@Async` 标记的方法。需要配合 `@EnableAsync` 使用。

31. **`@EnableAsync`**：
    *   **用途**：在配置类上启用 Spring 的异步方法执行功能。

## 缓存注解

32. **`@EnableCaching`**：
    *   **用途**：在配置类上启用 Spring 的缓存抽象。

33. **`@Cacheable`**：
    *   **用途**：标记一个方法的返回值可以被缓存。
    *   **说明**：在方法执行前，Spring 会先检查缓存，如果命中则直接返回缓存值；否则执行方法并将返回值存入缓存。

34. **`@CachePut`**：
    *   **用途**：标记一个方法总是会被执行，并将返回值存入缓存。
    *   **说明**：适用于更新操作，确保方法执行后缓存被更新。

35. **`@CacheEvict`**：
    *   **用途**：标记一个方法，其执行会触发缓存清除操作。
    *   **说明**：适用于删除操作，清除指定缓存或所有缓存。

## 测试注解

36. **`@RunWith(SpringRunner.class)` / `@ExtendWith(SpringExtension.class)` (JUnit 5)**：
    *   **用途**：将 JUnit 测试与 Spring TestContext Framework 集成。
    *   **说明**：`SpringRunner` (JUnit 4) 或 `SpringExtension` (JUnit 5) 允许在测试中使用 Spring 的特性，如依赖注入和事务管理。

37. **`@SpringBootTest`**：
    *   **用途**：提供 Spring Boot 应用的集成测试能力。
    *   **说明**：它会启动一个完整的 Spring 应用程序上下文，并提供各种配置选项（如端口、环境属性等）。

38. **`@WebMvcTest`**：
    *   **用途**：专门用于测试 Spring MVC 控制器。
    *   **说明**：只加载与 Web 层相关的 Bean，提供 `MockMvc` 用于模拟 HTTP 请求。

39. **`@DataJpaTest`**：
    *   **用途**：专门用于测试 JPA 持久层组件。
    *   **说明**：只加载与 JPA 相关的 Bean，默认使用内存数据库，并为每个测试方法回滚事务。

这些注解极大地提高了 Spring 应用的开发效率和可维护性。