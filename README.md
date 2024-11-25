# spring-boot-interview-corner

### 1. What is Spring Boot, and why is it used?
- Spring boot is Java-based framework built on top of the Spring Framework. It simplifies the development of spring applications by providing features like auto-configuration, embedded servers, and pre-configured templates.
  It eliminates the need for extensive XML or annotation-based configuration, allowing developers to focus on writing business logic.

  #### Why is Spring Boot used?
  Spring Boot is used to accelerate the development of production-ready applications with minimal effort. It offers

  ##### 1. Ease of Development:
    - Reduces boilerplate code and setup time.
  ##### 2. Embedded Servers:
    - Applications can run independently without external server deployment (e.g., Tomcat).
  ##### 3. Microservices-Friendly:
    - It’s ideal for developing lightweight microservices.
  ##### 4. Production-Ready Tools:
    - Includes monitoring, metrics, and health checks via Actuator.
  ##### 5. Integration:
    - Leverages the power of the Spring ecosystem, making it easy to implement features like security, data access, or messaging.

### 2.	Explain the difference between Spring Framework and Spring Boot.
![Screenshot 2024-11-24 201851.png](..%2F..%2FPictures%2FScreenshots%2FScreenshot%202024-11-24%20201851.png)

#### Interview Explanation:
Spring Framework is a robust framework for building Java-based applications, but it often requires significant manual configuration and setup. In contrast, Spring Boot is designed to streamline and simplify the development process by offering opinionated defaults, auto-configuration, and embedded servers.

For example:

In **Spring Framework**, you need to configure a DataSource, EntityManagerFactory, and TransactionManager manually.

In **Spring Boot**, you only need to add dependencies like spring-boot-starter-data-jpa and provide application properties (e.g., database URL). Everything else is auto-configured.

**Why Spring Boot?**

Spring Boot addresses the complexity of configuring Spring Framework and speeds up development, making it particularly useful for modern microservices-based architectures.

### 3. What is the role of @SpringBootApplication?

**Role of** @SpringBootApplication **Annotation**

**@SpringBootApplication** is a composite annotation in Spring Boot that marks a class as the main entry point of a Spring Boot application. It combines three important annotations and provides default configurations to bootstrap the application.

**Breakdown of** @SpringBootApplication

@SpringBootApplication is equivalent to using the following three annotations together:

1. ``@EnableAutoConfiguration``

    - Enables Spring Boot's auto-configuration feature.
    - Automatically configures Spring components and beans based on the dependencies in the classpath (e.g., setting up a ``DataSource`` if JDBC is present).

2. ``@ComponentScan``

    - Scans the package of the annotated class and its sub-packages for Spring components like ``@Component,`` ``@Service,`` ``@Repository,`` and ``@Controller.``
    - Ensures all required beans are discovered and registered in the application context.
3. ``@Configuration``

    - Indicates that the class can define **Spring configuration** using Java-based configuration (instead of XML).
    - Allows defining`` @Bean ``methods to provide custom bean definitions.

**Why Use @SpringBootApplication?**

1. **Convenience:**

    - Instead of using ``@EnableAutoConfiguratio``,  ``@ComponentScan,`` and ``@Configuration`` separately, you can use the single ``@SpringBootApplication`` annotation to achieve the same functionality.
2. **Entry Point:**
    - It marks the main class of the application where the main method resides.
    - This is the starting point for the **SpringApplication.run()** method, which bootstraps the application.

**Example Usage**

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MySpringBootApplication {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}

```

Here’s what happens when the application starts:

**Auto-Configuration:** Configures beans automatically based on classpath dependencies.

**Component Scanning:** Detects Spring-managed components in the current package and sub-packages.

**Configuration Loading:** Loads custom configurations defined in the application class or elsewhere.

### Customizing Behavior
**Excluding Auto-Configuration:**
- If you want to exclude specific auto-configurations, you can do this:
```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
public class MyApp { ... }

```
**Custom Component Scanning:**
- If your components are in a different package, specify the base package:
```java
@SpringBootApplication(scanBasePackages = "com.example.mycomponents")
public class MyApp { ... }

```
### 4. How does Spring Boot simplify dependency management?

**How Spring Boot Simplifies Dependency Management**

Spring Boot simplifies dependency management through Starter Dependencies, Maven BOM (Bill of Materials), and its opinionated approach to pre-configuring commonly used libraries. This significantly reduces the effort required to manage dependencies in your project.

**Key Features of Dependency Management in Spring Boot**

1. **Starter Dependencies**

    - Spring Boot provides starter dependencies, which are curated sets of commonly used libraries bundled together.
    - These starters eliminate the need to specify individual dependencies for a specific functionality.
    - **Example:**
        - To build a web application, you only need to add spring-boot-starter-web to your pom.xml or build.gradle.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

``` 
This starter automatically includes dependencies like:

- Spring MVC
- Embedded Tomcat server
- Jackson for JSON processing

2. **Version Management with BOM**

    - Spring Boot uses a Bill of Materials (BOM) to manage dependency versions.
    - This ensures that all dependencies in your project are compatible with each other.
    - Developers don’t have to worry about version conflicts or manually specifying versions for Spring-related libraries.

Example in ``pom.xml``

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>3.1.4</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

```

3. **Opinionated Defaults**

    - Spring Boot chooses the most suitable libraries and versions for you based on its opinionated model.
    - For example, if you use spring-boot-starter-data-jpa, it automatically includes Hibernate, eliminating the need to figure out and configure dependencies manually.
4. **Reduced Boilerplate**

    - Without Spring Boot, you'd need to manage several individual dependencies for a simple feature.
    - Spring Boot bundles related dependencies under a single starter, minimizing the number of lines in the dependency list.

   Example Comparison: **Without Starter Dependencies (Traditional Spring):**
```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
</dependency>
<!-- And more... -->

```
**With Starter Dependency (Spring Boot):**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

```

5. **Simplified Upgrades**

    - Upgrading Spring Boot versions automatically updates the versions of all related dependencies, ensuring compatibility.
    - This reduces the risk of runtime errors caused by version mismatches.
6. **Custom Starters**

    - Developers can create their own custom starter dependencies to package specific functionality, enabling consistent dependency management across teams or projects.

**Advantages in Real-World Use**

**Time Savings:** Developers focus on building features instead of managing dependency conflicts.

**Reduced Complexity:** No need to research and configure individual library versions.

**Consistency:** Projects built with the same Spring Boot version maintain consistent dependencies.

### 5. What is the Spring Boot Starter? Give examples.
A **Spring Boot Starter** is a **pre-defined set of dependencies** provided by Spring Boot to simplify project setup and configuration. These starters bundle commonly used libraries and frameworks needed for a specific functionality into a single dependency, eliminating the need to include and configure each dependency manually.

**Key Features of Spring Boot Starters**

**Convenience:** Simplifies dependency management by bundling related libraries.

**Auto-Configuration:** Works with Spring Boot's auto-configuration to reduce boilerplate setup.

**Version Management:** Ensures all included libraries are compatible with each other.

**Time-Saving:** Developers can add one dependency to enable specific features instead of adding multiple related dependencies.

![Screenshot 2024-11-24 214727.png](..%2F..%2FPictures%2FScreenshots%2FScreenshot%202024-11-24%20214727.png)

### 6. Explain auto-configuration in Spring Boot.
Auto-configuration is a key feature of Spring Boot that automatically configures your application based on the dependencies and settings available in your project. It eliminates the need for manual configuration by providing sensible defaults and enabling required beans and configurations automatically.

**How Does Auto-Configuration Work?**

1. **Dependency Detection:**

    - Spring Boot examines the dependencies in the classpath (e.g., spring-boot-starter-web).
    - Based on these dependencies, it identifies the components or beans needed for the application.

2. **Conditional Beans:**

    - Auto-configuration classes include conditional logic using annotations like ``@ConditionalOnClass,`` ``@ConditionalOnMissingBean,`` and ``@ConditionalOnProperty.``
    - Example:
        - If ``spring-boot-starter-web`` is on the classpath, Spring Boot auto-configures beans for Spring MVC, an embedded web server (like Tomcat), and Jackson for JSON processing.

3. **Configuration Classes:**

    - Auto-configuration is driven by classes annotated with ``@EnableAutoConfiguration.``
    - These classes are listed in ``META-INF/spring.factories`` in the Spring Boot JARs.
    - Example: ``WebMvcAutoConfiguration``, ``DataSourceAutoConfiguration``.

4. **Customization:**

    - Defaults can be overridden by providing custom beans or configuration in your application.

**Example of Auto-Configuration**

Without Auto-Configuration (Traditional Spring): In a traditional Spring application, you must configure a DataSource manually for database connectivity:

```java
@Configuration
public class DataSourceConfig {
    @Bean
    public DataSource dataSource() {
        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/mydb");
        dataSource.setUsername("root");
        dataSource.setPassword("password");
        return dataSource;
    }
}

```
**With Auto-Configuration (Spring Boot):** Spring Boot automatically configures the DataSource if it detects the necessary dependencies (spring-boot-starter-data-jpa and mysql-connector-java) and properties (spring.datasource.*) in application.properties:
```java
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=update

```

**Key Annotations Used in Auto-Configuration**

``@EnableAutoConfiguration``:

- Enables Spring Boot’s auto-configuration feature.
- Usually included via @SpringBootApplication.
-
``@ConditionalOnClass:``

- Configures beans only if a specific class is present in the classpath.

``@ConditionalOnMissingBean:``

- Configures a bean only if it’s not already defined in the application context.

``@ConditionalOnProperty:``

- Activates configuration based on specific properties.

**Advantages of Auto-Configuration**

1. **Reduces Boilerplate Code:**
- You don’t need to write extensive configuration classes for common setups.

2. **Quick Setup:**

- Applications can be up and running with minimal configuration.

3. **Customizable**:

- bDefaults can be overridden to suit specific needs.

4. **Scalable:**

- Simplifies adding new features by enabling relevant starters.

**Disabling Auto-Configuration**

If auto-configuration is not desired, you can disable it:

1. Using ``@SpringBootApplication:``

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
public class MyApplication { }

```

2. Using ``application.properties:``

```java
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration

```
![Screenshot 2024-11-25 084053.png](..%2F..%2FPictures%2FScreenshots%2FScreenshot%202024-11-25%20084053.png)


### @Scope
- scope annotations define the lifecycle and visibility of beans. By default, Spring beans are singleton, but you can use different scope annotations to modify the behavior according to your needs.

#### Types of Scope Annotations
1. @Singleton (Default Scope)
2. @Prototype
3. @RequestScope
4. @SessionScope
5. @ApplicationScope
6. @RefreshScope (from Spring Cloud)

#### 1. Singleton Scope (Default)
- Annotation: No special annotation required (default behavior).
- Description: Only one instance of the bean is created and shared across the entire Spring context.

```java
@Component
public class MySingletonService {
    // Default singleton scope
}
```
- Use Case: Use for stateless services or shared resources.

#### 2. Prototype Scope
- Annotation: @Scope("prototype")
- Description: A new instance of the bean is created every time it is requested from the container.
```java
@Component
@Scope("prototype")
public class MyPrototypeService {
}
```
- Use Case: Use when you need a new instance for every request, such as in multi-threaded environments.
#### 3. Request Scope
- Annotation: @RequestScope
- Description: A new bean instance is created for each HTTP request. After the request is completed, the bean is discarded.

```java
@Component
@RequestScope
public class MyRequestScopedService {
}

```
- Use Case: Use for request-specific data, such as user session details in web applications.

#### 4. Session Scope
- Annotation: @SessionScope
- Description: A new bean instance is created for each HTTP session. The bean will last as long as the session is active.

```java
@Component
@SessionScope
public class MySessionScopedService {
}
```
- Use Case: Use to store session-specific data (e.g., user preferences or shopping cart details).

#### 5. Application Scope
- Annotation: @ApplicationScope
- Description: A singleton bean, shared across the entire application (similar to @Singleton but specific to web applications).

```java
@Component
@ApplicationScope
public class MyApplicationScopedService {
}

```
- Use Case: Use for global application-wide state, like configuration or settings shared across multiple sessions.

#### 6. Refresh Scope (Spring Cloud)
- Annotation: @RefreshScope (from org.springframework.cloud.context.config.annotation)
- Description: Allows a bean to be refreshed at runtime when there are changes in configuration (useful for configurations from external sources like Config Server).

``` java
@RefreshScope
@Component
public class MyConfigService {
    @Value("${my.config.value}")
    private String configValue;
}

```
- Use Case: Use for applications that need to refresh beans dynamically when configuration changes without restarting the app.

#### Example: Injecting Different Scoped Beans
```java
@RestController
public class DemoController {

    private final MySingletonService singletonService;
    private final MyPrototypeService prototypeService;

    public DemoController(MySingletonService singletonService, MyPrototypeService prototypeService) {
        this.singletonService = singletonService;
        this.prototypeService = prototypeService;
    }

    @GetMapping("/test")
    public String testScopes() {
        return "Singleton: " + singletonService.hashCode() + 
               ", Prototype: " + prototypeService.hashCode();
    }
}

```

#### output

```
Singleton: 12345678, Prototype: 87654321

```
- Note: On every request, the prototype bean will have a different hash code, but the singleton bean will retain the same hash code.

  <img width="849" alt="image" src="https://github.com/user-attachments/assets/21f716bf-7ab5-4d5a-b9c2-a7cac2fcf5e4">

### @Bean
- @Bean annotation is used in @Configuration classes to define beans that will be managed by the Spring container. 
 @Bean annotation is a method-level annotation that indicates that a method will create, configure, and initialize a new object to be managed by the Spring IoC container.
#### Why Use @Bean?
- Manual Bean Creation: Sometimes, Spring’s automatic configuration isn't enough, and you need to create beans manually. This is where @Bean comes into play.
- Flexibility: You can use @Bean to control the exact behavior of the objects created, offering more customization than component-scanning-based beans.
- Dependency Injection: Beans defined using @Bean can be injected into other parts of the application using @Autowired or constructor injection.
#### When to Use @Bean?
- When you want to configure an external library's object that Spring cannot automatically configure.
- When you need fine control over the instantiation logic of an object.
For objects like services, repositories, or utilities that require specific configurations
