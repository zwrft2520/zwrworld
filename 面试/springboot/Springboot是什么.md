Spring Boot 是一个框架，旨在简化 Spring 应用程序的创建、配置和部署。它基于 Spring 框架，但移除了大量繁琐的 XML 配置，使得开发人员能够更快地构建独立的、生产级别的 Spring 应用程序。

Spring Boot 的主要特点包括：

1.  **独立运行 (Standalone)**：
    *   Spring Boot 应用程序可以打包成可执行的 JAR 文件，包含所有依赖项（包括嵌入式 Web 服务器如 Tomcat、Jetty 或 Undertow），无需部署到传统的应用服务器。
2.  **自动配置 (Auto-configuration)**：
    *   根据项目中添加的依赖项，Spring Boot 会自动配置 Spring 应用程序的许多方面。例如，如果检测到 `spring-webmvc` 依赖，它会自动配置 DispatcherServlet；如果检测到数据库依赖，它会尝试配置数据源等。这大大减少了显式配置的需求。
3.  **起步依赖 (Starter Dependencies)**：
    *   Spring Boot 提供了一系列“starter”POM 文件，它们是预配置的依赖集合，可以快速集成特定功能。例如，`spring-boot-starter-web` 包含了构建 Web 应用程序所需的所有常用依赖，包括 Spring MVC 和嵌入式 Tomcat。
4.  **无代码生成和 XML 配置 (No Code Generation or XML Configuration)**：
    *   Spring Boot 采用“约定优于配置”的原则，大量使用 Java Config 和注解，极大地减少了 XML 配置文件的使用，甚至可以完全避免。
5.  **开箱即用 (Opinionated Defaults)**：
    *   提供了一套默认配置，让你无需过多思考就能快速启动项目。当然，这些默认值都是可以轻松覆盖和自定义的。
6.  **生产就绪特性 (Production-ready Features)**：
    *   内置了许多生产环境所需的功能，如健康检查、度量指标、外部化配置、安全特性等。Spring Boot Actuator 模块提供了对应用程序的监控和管理能力。
7.  **内嵌服务器 (Embedded Servers)**：
    *   默认支持内嵌 Tomcat、Jetty 或 Undertow，简化了 Web 应用程序的部署。