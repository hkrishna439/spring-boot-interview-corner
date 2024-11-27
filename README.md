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
![img_6.png](img_6.png)
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

![img_4.png](img_4.png)

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
![img_5.png](img_5.png)

### 7. What is the Spring Boot Actuator, and how do you use it?

**Spring Boot Actuator** is a module in Spring Boot that provides a set of production-ready features to help monitor and manage applications. It exposes various endpoints that give insights into the application’s health, metrics, environment, configurations, and more.

This tool is particularly useful for operational purposes, such as debugging, auditing, performance monitoring, and diagnostics.


**Key Features of Spring Boot Actuator**

1. **Endpoints for Monitoring and Management:**

   - Provides REST API endpoints for various metrics and health checks.
   - Examples: ``/actuator/health, /actuator/metrics, /actuator/env.``
2. **Customizable Endpoints:**

    - You can enable, disable, or secure specific endpoints as needed.
3. **Integration with Monitoring Tools:**

    - Works seamlessly with tools like Prometheus, Grafana, and Micrometer for performance monitoring.
4. **Insight into Application State:**

    - Displays runtime details such as active beans, environment variables, memory usage, and thread details.


**How to Use Spring Boot Actuator**

**Step 1: Add Actuator Dependency**

Include the Spring Boot Actuator starter in your pom.xml or build.gradle.

**Maven:**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

```

**Gradle:**

```
implementation 'org.springframework.boot:spring-boot-starter-actuator'

```
**Step 2: Configure Actuator Endpoints**

By default, only the ``/actuator/health`` and ``/actuator/info`` endpoints are exposed. To enable or customize endpoints, update the ``application.properties`` or ``application.yml`` file.

**Example: Enable All Endpoints**

```
management.endpoints.web.exposure.include=*

```
**Example: Enable Specific Endpoints**

```
management.endpoints.web.exposure.include=health,info,metrics
```
**Example: Secure Endpoints** Use Spring Security to restrict access:

```
management.endpoint.health.roles=ADMIN

```

**Step 3: Access Actuator Endpoints**

Default Endpoints:

![img.png](img.png)

**Step 4: Customize Health Checks and Info**

**Custom Health Indicator:** You can create a custom health check by implementing the HealthIndicator interface:

```java
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.stereotype.Component;

@Component
public class CustomHealthIndicator implements HealthIndicator {
    @Override
    public Health health() {
        // Add custom logic
        return Health.up().withDetail("custom", "Everything is fine").build();
    }
}

```

**Custom Info:** Add custom application info in application.properties:

```
info.app.name=Demo Application
info.app.version=1.0.0

```
Access via ``/actuator/info.``


**Step 5: Integrate with Monitoring Tools**

**Micrometer:** Integrates with Actuator to provide application metrics.

**Prometheus:** Use the prometheus endpoint to export metrics.

**Grafana:** Visualize metrics using dashboards.

**Cloud Providers:** Integrate with AWS CloudWatch, Azure Monitor, etc.

**Advantages of Spring Boot Actuator**

1. **Quick Monitoring Setup:**

    - Minimal configuration required to enable health checks and metrics.
2. **Production Readiness:**

    - Provides detailed runtime insights to ensure application stability.
3. **Integration-Friendly:**

    - Works with many third-party monitoring and alerting tools.
4. **Customizable and Extendable:**

    -Create custom endpoints or health indicators based on business needs.

**Example Use Case**

Suppose you want to monitor an e-commerce application for uptime and performance. Using Actuator, you can:

- Check if the application is running (``/actuator/health``).
- Monitor request throughput and response times (``/actuator/metrics``).
- Diagnose memory leaks using a thread dump (``/actuator/threads``).

### 8. How do you handle application properties in Spring Boot?
Spring Boot provides a flexible way to configure application settings using property files. These configurations can be set in ``application.properties`` or ``application.yml`` files, externalized configurations, environment variables, or even command-line arguments.

**1. Configuring Properties in application.properties or application.yml**

   **Default Location:**
   These files are typically located in `src/main/resources`.

   **Example** `application.properties`:
```
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password
logging.level.org.springframework=DEBUG
```
**Example** `application.yml`:
```
server:
  port: 8081

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: password

logging:
  level:
    org.springframework: DEBUG

```
**2. Accessing Properties in Code**

**Using** `@Value` **Annotation**:

   You can inject individual properties directly into fields or methods.

**Example:**

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class MyService {
    @Value("${server.port}")
    private int serverPort;

    @Value("${spring.datasource.url}")
    private String dataSourceUrl;

    public void printProperties() {
        System.out.println("Server Port: " + serverPort);
        System.out.println("DataSource URL: " + dataSourceUrl);
    }
}

```
**Using** `@ConfigurationProperties`:

For managing multiple related properties, use the @ConfigurationProperties annotation. This maps property keys to fields in a class.

**Example:**

1. Enable configuration properties in the main class:

```java
@SpringBootApplication
@EnableConfigurationProperties(MyProperties.class)
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}

```
2. Create a class for properties:
```java
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@ConfigurationProperties(prefix = "myapp")
public class MyProperties {
    private String name;
    private int timeout;

    // Getters and Setters
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getTimeout() {
        return timeout;
    }
    public void setTimeout(int timeout) {
        this.timeout = timeout;
    }
}

```
3. Define properties in `application.properties`:
```
myapp.name=My Application
myapp.timeout=30

```
4. Use the properties:

```
@Autowired
private MyProperties myProperties;

System.out.println(myProperties.getName());
System.out.println(myProperties.getTimeout());

```
**3. Externalizing Configuration**

   Spring Boot allows external configuration of properties for easier environment-specific setups (e.g., dev, test, prod).

**Priority of Configuration Sources:**

1. Command-line arguments
2. Environment variables
3. `application.properties` or `application.yml`
4. Default settings

**Environment-Specific Properties:**

1. Create files like `application-dev.properties` or `application-prod.properties`.
2. Activate a profile in `application.properties`:
```
spring.profiles.active=dev

```
**4. Using Profiles for Environment Management**

   Profiles allow you to define separate configurations for different environments.

**Example Setup:**

1. `application-dev.properties`:
```
server.port=8082
logging.level.org.springframework=DEBUG

```
2. `application-prod.properties`:
```
server.port=8080
logging.level.org.springframework=ERROR

```
3. Activate the desired profile:
```
spring.profiles.active=prod
```

**5. Binding Complex Properties**

   You can define and bind hierarchical properties to Java classes using @ConfigurationProperties.

**Example for Nested Properties:**

`application.yml:`
```
app:
  settings:
    retries: 5
    timeout: 30

```
**Java Class:**
```java
@ConfigurationProperties(prefix = "app.settings")
@Component
public class AppSettings {
    private int retries;
    private int timeout;

    // Getters and Setters
}

```
**6. Overriding Properties**

   You can override properties using:

1. Command-line arguments:
```
java -jar app.jar --server.port=9090

```
2. Environment Variables:
```
export SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/anotherdb

```
3. System Properties:
```
java -Dspring.datasource.username=admin -jar app.jar

```
**7. Encrypting Sensitive Properties**

   Sensitive data like passwords can be encrypted using third-party tools like Jasypt or Spring Cloud Config.


### 9. What is the use of @RestController?
The `@RestController` annotation in Spring Boot is a specialized version of the `@Controller` annotation. It is used to create RESTful web services by combining the functionalities of` @Controller` and `@ResponseBody`.

When you annotate a class with `@RestController`, Spring Boot automatically handles HTTP requests and serializes Java objects into JSON (or other formats like XML) in the HTTP response body.

**Key Features of @RestController:**

1. **Simplifies REST API Development:**

    - No need to explicitly annotate methods with `@ResponseBody` as it's included in `@RestController`.
2. **Handles HTTP Requests**:

    - Maps HTTP requests (like `GET`, `POST`, `PUT`, `DELETE`) to specific methods using `@RequestMapping` or HTTP-specific annotations (`@GetMapping`, `@PostMapping`, etc.).
3. **Automatic JSON Conversion**:

    - Converts Java objects to JSON responses using the Jackson library (or other configured message converters).
4. **Lightweight:**

    - Primarily used for APIs, not for rendering web views like JSP or Thymeleaf.
   
**Usage Example**

1. Basic Example:
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class MyRestController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}

```
- URL to access: `http://localhost:8080/api/hello`
- Response: `Hello, World!`

**2. Returning JSON Data:**
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class UserController {

    @GetMapping("/user")
    public User getUser() {
        return new User(1, "John Doe", "john.doe@example.com");
    }
}

class User {
    private int id;
    private String name;
    private String email;

    // Constructor, Getters, and Setters

    public User(int id, String name, String email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }

    // Getters and setters (omitted for brevity)
}

```
- **URL to access:** `http://localhost:8080/user`
- **Response (JSON):**

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@example.com"
}

```
**Why Use `@RestController`?**

- To simplify the development of RESTful APIs.
- It reduces boilerplate code (no need to annotate each method with `@ResponseBody`).
- Ensures efficient and easy JSON serialization for HTTP responses.
- Widely used for microservices architecture where APIs communicate using JSON or XML.

### 10. Explain the difference between @Controller and @RestController.
`@Controller` and `@RestController` are both Spring annotations used to define controller classes, but they serve different purposes depending on the nature of the application (web-based vs. RESTful). Here's a detailed comparison:

![img_2.png](img_2.png)

**Examples**

1. **Example of** `@Controller`:

```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.ui.Model;

@Controller
public class WebController {

    @GetMapping("/home")
    public String homePage(Model model) {
        model.addAttribute("message", "Welcome to the home page!");
        return "home";  // Resolves to "home.html" or "home.jsp"
    }
}

```
**Purpose:**

- Used for applications that render views (e.g., an HTML page like `home.html`)

**Behavior:**

- The `return "home"` tells Spring to look for a view named home using the configured view resolver.


2. **Example of** `@RestController`:

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class ApiController {

    @GetMapping("/api/greeting")
    public String greeting() {
        return "Hello, World!";
    }
}

```
**Purpose:**

- Used for APIs that return data (e.g., `Hello, World!` as plain text or JSON).

**Behavior:**

- Automatically serializes the return value into the HTTP response body (e.g., JSON).

**Key Differences in Behavior**

**Without** @ResponseBody

If you use` @Controller` and don't specify `@ResponseBody`, Spring assumes the method is returning a view name, not raw data.

**With** `@RestController`

Using `@RestController` eliminates the need for `@ResponseBody` on each method because it’s implied that the controller handles RESTful responses.


**When to Use What?**

- **Use** `@Controller`:

    - For traditional web applications with a user interface that renders HTML or other view templates like Thymeleaf, JSP, etc.
- **Use** `@RestController`:

    - For RESTful services or microservices where the application primarily provides data as JSON or XML responses.


### 11. 	What is @RequestMapping and its variants?

`@RequestMapping` is an annotation in Spring Framework used to map HTTP requests to specific handler methods in a controller class. It allows developers to define the URL path, HTTP method, and other request-mapping details.

In addition to `@RequestMapping`, Spring provides method-specific variants like `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, and `@PatchMapping` for convenience.

**1. @RequestMapping**

   **Purpose:**
   Maps HTTP requests to controller methods.

- **Attributes:**
![img_7.png](img_7.png)
**Example:**
   ```java
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RequestMethod;
   import org.springframework.web.bind.annotation.RestController;
   
   @RestController
   @RequestMapping("/api")
   public class MyController {
   
       @RequestMapping(value = "/greet", method = RequestMethod.GET)
       public String greet() {
           return "Hello, World!";
       }
   }
   
   ```
  - URL to access: `http://localhost:8080/api/greet`
  - HTTP Method: `GET`

**2. Variants of @RequestMapping**

   Spring introduced method-specific annotations for common HTTP methods to make code more concise and readable.


**2.1 @GetMapping**

   - Used for handling GET requests.
   - **Example:**
   ```
@GetMapping("/users")
public List<String> getUsers() {
    return List.of("Alice", "Bob", "Charlie");
}
```
**2.2 @PostMapping**

   - Used for handling POST requests.
   - **Example:**
   ```java
   @PostMapping("/users")
   public String createUser(@RequestBody String user) {
      return "User " + user + " created!";
}

   ```
**2.3 @PutMapping**

   - Used for handling PUT requests.
   - **Example:**
   ```java
    @PutMapping("/users/{id}")
   public String updateUser(@PathVariable int id, @RequestBody String user) {
      return "User with ID " + id + " updated to " + user;
}

   ```
**2.4 @DeleteMapping**

   - Used for handling DELETE requests.
   - **Example:**


```java
@DeleteMapping("/users/{id}")
public String deleteUser(@PathVariable int id) {
    return "User with ID " + id + " deleted!";
}

```

**2.5 @PatchMapping**

   - Used for handling PATCH requests (partial updates).
   - **Example:**

```java
@PatchMapping("/users/{id}")
public String updateUserPartial(@PathVariable int id, @RequestBody Map<String, Object> updates) {
    return "User with ID " + id + " partially updated!";
}

```
**Advanced Examples**

**Mapping with Parameters:**
```java
@RequestMapping(value = "/filter", method = RequestMethod.GET, params = "type=admin")
public String filterAdmins() {
    return "Filtered admin users";
}

```
- Access URL:` /filter?type=admin`

**Mapping with Headers:**
```java
@RequestMapping(value = "/headers", headers = "X-Custom-Header=my-header")
public String withHeaders() {
    return "Custom header present!";
}

```
- Access URL: Add the header `X-Custom-Header=my-header` to the request.

**Mapping with Content Type (Consumes/Produces):**
```java
@RequestMapping(value = "/json", method = RequestMethod.POST, consumes = "application/json", produces = "application/json")
public String handleJson(@RequestBody String json) {
    return "{\"message\": \"Received JSON\"}";
}

```
- **Consumes**: Specifies the type of request body.
- **Produces**: Specifies the type of response body.

**When to Use @RequestMapping or Variants**

- Use `@RequestMapping`:

   - For complex mappings (e.g., with parameters, headers, or multiple attributes).
   - For backward compatibility with older Spring versions.
**Use HTTP-Specific Variants:**
   - For simple, single-method mappings (e.g., `GET`, `POST`).
   - To make code more readable and concise.

### 12. What is @PathVariable, and how is it used?

`@PathVariable` is an annotation in Spring Framework used to extract values from the URL path in a RESTful API. It binds the values from the URL directly to the method parameters, making it easy to handle dynamic parts of a URL.

**Key Features of @PathVariable:**

1. **Dynamic URL Parameters:**

    - Enables handling URLs with dynamic segments (e.g., `/users/{id}`).
2. **Binding Path Variables to Method Parameters:**

    - Automatically maps URL segments to method parameters.
3. **Customization:**

    - Allows specifying a different name for the variable in the URL and the method parameter.

**How to Use** `@PathVariable`

**Basic Example:**
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class UserController {

    @GetMapping("/users/{id}")
    public String getUserById(@PathVariable int id) {
        return "User with ID: " + id;
    }
}

```
- URL: `http://localhost:8080/users/101`
-  Response: `User with ID: 101`

**Using Multiple** `@PathVariable`:

```java
@GetMapping("/users/{userId}/orders/{orderId}")
public String getOrderDetails(@PathVariable int userId, @PathVariable int orderId) {
    return "Order " + orderId + " for User " + userId;
}

```
- URL: `http://localhost:8080/users/1/orders/45`
- Response: `Order 45 for User 1`

**Customizing the Path Variable Name:**

If the path variable name in the URL and the method parameter are different, you can specify the mapping explicitly.

```java
@GetMapping("/products/{productId}")
public String getProduct(@PathVariable("productId") int id) {
    return "Product with ID: " + id;
}

```
- URL: `http://localhost:8080/products/20`
- Response: `Product with ID: 20`

**Advanced Features**

**Path Variables with Regular Expressions:**

You can restrict the format of path variables using regular expressions.

```java
@GetMapping("/users/{id:[0-9]+}")
public String getUserById(@PathVariable int id) {
    return "User ID: " + id;
}

```
- Acceptable URL:` http://localhost:8080/users/123`
- Invalid URL: `http://localhost:8080/users/abc` (will return a 404 error).

![img_8.png](img_8.png)

**Best Practices for Using @PathVariable:**
1. **Use** `@PathVariable` **for IDs or other essential URL parameters.**

    - E.g., /`users/{id}` is more intuitive than `/users?id=123`.
2. **Avoid overusing dynamic segments.**

    - Use query parameters (`@RequestParam`) for optional or non-essential data.
3. **Validate Path Variables.**

    - Use regular expressions in the mapping or add validation logic in the method.

**Common Interview Scenarios**

**Scenario 1: Explain PathVariable Usage**
- A candidate might explain the basics and demonstrate how `@PathVariable` maps dynamic URL parts to method parameters.

**Scenario 2: Handling Multiple Path Variables**
- Explain how to handle multiple dynamic segments in a URL and the mapping logic.

**Scenario 3: Custom Path Variable Names**
- Discuss how to map a differently named path variable to a method parameter.

### 13. How is @RequestParam used?
`@RequestParam` is an annotation in the Spring Framework used to extract query parameters from the URL of an HTTP request and bind them to method parameters in a controller. It is commonly used for retrieving optional or additional data sent along with the request.

**Key Features of `@RequestParam`**

1. **Maps Query Parameters:**
Extracts parameters from the query string of the URL (e.g., ?key=value).

2. **Binds Query Parameters to Method Parameters:**
Automatically binds query parameters to Java method parameters.

3. **Customization:**
Allows setting default values and marking parameters as required or optional.


**How to Use `@RequestParam`**

**Basic Example**
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class ExampleController {

    @GetMapping("/greet")
    public String greet(@RequestParam String name) {
        return "Hello, " + name + "!";
    }
}

```
- URL:` http://localhost:8080/greet?name=John`
- Response: `Hello, John!`

**Setting Default Values**

  You can provide a default value for a query parameter if it is not supplied in the request.
```java
@GetMapping("/greet")
public String greet(@RequestParam(defaultValue = "Guest") String name) {
    return "Hello, " + name + "!";
}

```
- URL without parameter: `http://localhost:8080/greet`
- Response: `Hello, Guest!`

**Optional Query Parameters**

  You can make a query parameter optional by setting required = false.
```java
@GetMapping("/greet")
public String greet(@RequestParam(required = false) String name) {
    if (name == null) {
        return "Hello, Guest!";
    }
    return "Hello, " + name + "!";
}

```
- URL without parameter: `http://localhost:8080/greet`
- Response: `Hello, Guest!`

**Multiple Query Parameters**

You can handle multiple query parameters in the same method.

```java
@GetMapping("/user")
public String getUserDetails(@RequestParam String name, @RequestParam int age) {
    return "User: " + name + ", Age: " + age;
}

```
- URL: `http://localhost:8080/user?name=Alice&age=25`
- Response: `User: Alice, Age: 25`

**Using Collections as Parameters**

You can bind query parameters to a List or Set.

```java
@GetMapping("/numbers")
public String getNumbers(@RequestParam List<Integer> nums) {
    return "Numbers: " + nums.toString();
}

```
- URL: `http://localhost:8080/numbers?nums=1&nums=2&nums=3`
- Response: `Numbers: [1, 2, 3]`

**Best Practices for @RequestParam**

1. **Use Default Values:**
Avoid `NullPointerException` or unnecessary validation checks by providing default values.

2. **Mark Optional Parameters:**
Use `required = false` for query parameters that may not always be present.

3. **Use Descriptive Parameter Names:**
Ensure parameter names are self-explanatory for better readability and usability.

4. **Validate Query Parameters:**
Use validation annotations like `@Min`,` @Max`, or custom validators for input validation.

**Common Interview Scenarios**

**Scenario 1: Explain Default Values**
- You may be asked how `@RequestParam` handles default values or optional parameters. Demonstrate by providing examples of `defaultValue` or `required = false`.

**Scenario 2: Collections in Query Parameters**
- Explain how `@RequestParam` supports handling multiple values (e.g., `?nums=1&nums=2`).

**Scenario 3: Compare `@RequestParam` with `@PathVariable`**
- Highlight when to use `@RequestParam` (e.g., filtering, pagination) and when `@PathVariable` is more appropriate (e.g., identifying resources).

### 14. What is the purpose of @Component and @Service?

In the Spring Framework, `@Component` and `@Service` are **stereotype annotations** that indicate a class is a Spring-managed bean. They allow Spring to detect and register these classes automatically in the **Spring Application Context** during component scanning

`@Component`

1.**Purpose:**

Marks a class as a Spring-managed bean. It's a generic stereotype that can be used for any class you want Spring to manage but doesn’t specify the role of the class in the application.

2.**Usage:**

Use `@Component` for general-purpose Spring beans when other specific stereotypes like `@Service`, `@Repository`, or `@Controller` don’t fit.

**Example:**
```java
import org.springframework.stereotype.Component;

@Component
public class EmailValidator {
    public boolean isValid(String email) {
        return email.contains("@");
    }
}

```
- **Key Feature**: The class `EmailValidator` will now be managed by Spring, meaning it can be injected into other components using `@Autowired.`

`@Service`

1.**Purpose:**

Specialization of @Component that is specifically intended for business logic and service-layer classes. It adds semantic meaning to the application, indicating that the class contains service logic.

2.**Usage:**

Use @Service to define a class as part of the service layer in your application.

**Example:**
```java
import org.springframework.stereotype.Service;

@Service
public class UserService {
    public String getUserById(int id) {
        return "User-" + id;
    }
}

```
- **Key Feature**: By marking this class with `@Service`, it becomes clear to developers that it belongs to the **business logic layer**

![img_9.png](img_9.png)

**How They Work in Spring**

1.**Component Scanning:**

Both @Component and @Service are discovered during Spring's component scanning process, which scans the classpath for annotated classes.

- This requires enabling component scanning using annotations like @ComponentScan or Spring Boot's default configuration.

2.**Bean Registration:**

Both annotations register the class as a bean in the Spring Application Context, making it eligible for dependency injection.


**Practical Example:**

- Consider an application with an email service.

**EmailValidator Class:**

- Handles general utility functionality.

```java
@Component
public class EmailValidator {
    public boolean isValid(String email) {
        return email.contains("@");
    }
}

```
**EmailService Class:**

- Handles the business logic for sending emails.
```java
@Service
public class EmailService {
    private final EmailValidator emailValidator;

    public EmailService(EmailValidator emailValidator) {
        this.emailValidator = emailValidator;
    }

    public String sendEmail(String email) {
        if (emailValidator.isValid(email)) {
            return "Email sent to " + email;
        } else {
            return "Invalid email address!";
        }
    }
}

```
**Interview Insights**

**Common Questions:**

1. What is the difference between `@Component `and` @Service`?

- `@Service` is a specialization of `@Component` used for the service layer. Both are managed by Spring.
2. **Why use @Service instead of `@Component`?**

- To indicate the specific role of the class in the application's architecture (business logic).
3. **Can you replace` @Service` with `@Component`?**

- Yes, technically. But using `@Service` adds semantic clarity, making the code more maintainable and understandable.
Summary

### 15. How does @Autowired work in Spring Boot?

`@Autowired` is an annotation in the Spring Framework used for **dependency injection**. It allows Spring to automatically resolve and inject a bean into another bean, reducing boilerplate code and making it easier to manage dependencies.

**Key Features of @Autowired:**

1. **Dependency Injection:**
Automatically injects required dependencies into a class.

2. **Bean Discovery:**
Spring looks for a matching bean in the **Application Context** (by type, and optionally by name) and injects it.

3. **Injection Points:**
Can be applied to constructors, fields, or setter methods.

4. **Optional Dependencies:**
Can handle optional dependencies with `required = false`.

**How @Autowired Works:**

1. **Default Behavior:**
   By default, `@Autowired` performs type-based injection:

    - It searches for a bean of the same type in the application context.
2. **Matching by Name:**
   If there are multiple beans of the same type, Spring tries to resolve the conflict by matching the variable name to the bean name.

3. **No Matching Bean:**
   If no matching bean is found, Spring throws an exception unless `required = false` is specified.

**Examples of `@Autowired`**

**1. Field Injection (Not Recommended)**
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public void saveUser(User user) {
        userRepository.save(user);
    }
}

```
- Spring injects `UserRepository` directly into the field.
- **Drawback**: Difficult to test and violates the principles of Dependency Injection (DI).

**2. Setter Injection**
```java
@Component
public class UserService {

    private UserRepository userRepository;

    @Autowired
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void saveUser(User user) {
        userRepository.save(user);
    }
}

```
- Dependencies are injected through a setter method.
- Allows late injection and easier testing.

**3. Constructor Injection (Recommended)**
```java
@Component
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void saveUser(User user) {
        userRepository.save(user);
    }
}

```
- Preferred method as it ensures that dependencies are injected when the object is created.
- Enables immutability and simplifies testing


**Handling Multiple Beans with `@Autowired`**

If there are multiple beans of the same type, you can specify which bean to inject using:

1.` @Qualifier:`

```java
@Component
public class UserService {
    private final UserRepository userRepository;

    @Autowired
    public UserService(@Qualifier("myRepository") UserRepository userRepository) {
        this.userRepository = userRepository;
    }
}

```
2. **Bean Names:**

- If no qualifier is provided, Spring tries to match the bean by name.

**Optional Dependencies with `@Autowired`**

You can specify `required = false` to make a dependency optional:
```java
@Autowired(required = false)
private NotificationService notificationService;

```
If `NotificationService` is not available in the context, the field will be null instead of throwing an exception.

**Best Practices for `@Autowired`**

1. Prefer Constructor Injection:
It promotes immutability, makes dependencies explicit, and simplifies testing.

2. Avoid Field Injection:
It makes unit testing harder and violates DI principles.

3. Use `@Qualifier` for Multiple Beans:
Resolve ambiguity when there are multiple beans of the same type.

4. Validate Optional Dependencies:
Ensure proper handling of optional dependencies when `required = false`.

**Common Interview Questions**

1. **What is `@Autowired?`**

- `@Autowired `is used to inject dependencies automatically in Spring beans.
2. **What are the different ways to use `@Autowired`?**

- Field injection, setter injection, and constructor injection.
3. **What happens if Spring finds multiple beans of the same type?**

- Spring throws a `NoUniqueBeanDefinitionException` unless a specific bean is specified using `@Qualifier`.
4. **How do you handle optional dependencies?**

- Use `@Autowired(required = false)` to allow for optional dependencies.
5. **Why is constructor injection preferred over field injection?**

- Constructor injection ensures immutability, makes dependencies explicit, and simplifies testing.

### 16. What is the difference between @Bean and @Component?
Both `@Bean` and `@Component` are used to define Spring beans, but they serve different purposes and are used in different contexts. Here's a detailed explanation:


**1.** `@Component`

   1.**Definition**:
   `@Component` is a stereotype annotation used to indicate that a class is a Spring-managed component (or bean). It allows the class to be automatically detected and registered as a bean during component scanning.

   2.**Use Case:**

    - Applied at the class level to make a class a Spring-managed bean.
    - Suitable for self-contained components such as services, repositories, or controllers.
   
   3.**Example:**
```java
import org.springframework.stereotype.Component;

@Component
public class EmailService {
    public void sendEmail(String email) {
        System.out.println("Sending email to: " + email);
    }
}

```
  4. **Bean Registration:**
 Beans are registered automatically via classpath scanning and require @ComponentScan or Spring Boot’s default scanning configuration.


**2.** `@Bean`
1.**Definition:**

`@Bean` is used to **explicitly define a bean** in a Spring **configuration class**. It provides finer control over bean creation and initialization.

2.**Use Case:**

- Used in **Java-based configuration classes** to manually define beans.
- Useful for beans that are created using a third-party library or require custom initialization logic.

3.**Example:**
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public EmailService emailService() {
        return new EmailService();
    }
}

```
4.**Bean Registration:**

Beans are registered explicitly using the `@Bean` annotation in a configuration class.

![img_10.png](img_10.png)

**When to Use `@Component`**

- Use @Component when:
    - The class is part of your application and follows Spring's stereotype conventions (e.g., `@Service`, `@Repository`, `@Controller`).
    - The bean can be easily registered through component scanning.
  
**When to Use `@Bean`**

- Use `@Bean` when:
    - The bean needs custom logic during initialization.
    - You need to configure third-party library beans.
    - The class is not under your control and cannot be annotated with @Component.

**Practical Example**

**Scenario: Registering a** `RestTemplate`
1. **Using**` @Component:`

```java
@Component
public class RestTemplateComponent {
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}

```
- Less commonly used since the method needs to be static or non-annotated.

2. **Using** `@Bean`
```java
@Configuration
public class AppConfig {

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}

```
- Preferred approach for beans like `RestTemplate` as it offers more flexibility and clarity.

**Best Practices**

- Use `@Component` (or its specializations like `@Service`, `@Repository`, `@Controller`) for **application-level beans** that are directly written by you.
- Use `@Bean` for:
  - **Third-party beans** that you can't annotate.
  - Complex initialization scenarios.
  - Dynamic or programmatically controlled bean creation.

**Interview Insights**

**Common Questions:**
1. **Can `@Component` and `@Bean` be used interchangeably?**

- No. While both result in Spring-managed beans, their use cases and contexts differ.
2. **When would you use `@Bean` over `@Component`?**

- For third-party library classes or when beans need custom initialization logic.
3. **What happens if both `@Component` and `@Bean` define the same bean?**

- Spring will throw a `BeanDefinitionOverrideException` unless explicitly allowed via configuration.

### 17. Explain the use of @Configuration in Spring Boot.

In Spring Boot, `@Configuration` is an annotation used to indicate that a class contains **Spring Bean definitions**. These bean definitions are processed by the Spring IoC (Inversion of Control) container to manage and provide dependencies throughout the application.

It is a part of Spring's Java-based configuration approach and is an alternative to the older XML-based configuration.


**Purpose of `@Configuration`**

1. **Java-based Configuration:**
Replaces XML-based configuration by defining beans directly in Java code.

2. **Defines Beans:**
Marks a class as a source of bean definitions using `@Bean` methods.

3. **Centralized Configuration:**
Acts as a central location to configure and manage beans.

4. **Enable Dependency Injection:**
Works seamlessly with Spring's dependency injection mechanism.

**How** `@Configuration` **Works**

When a class is annotated with `@Configuration`:

- Spring recognizes it as a **configuration class** during component scanning.
- The methods annotated with `@Bean` inside this class are processed, and the returned objects are registered as beans in the **Spring Application Context.**
  
**Example Usage of `@Configuration`**
1. **Basic Example**
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public String greetingMessage() {
        return "Hello, Spring Boot!";
    }
}

```
- Here, the `AppConfig` class is marked as a configuration class.
- The `greetingMessage` method defines a bean of type `String` with the value `"Hello, Spring Boot!".`

2. **Configuring a Third-Party Bean**
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.client.RestTemplate;

@Configuration
public class RestTemplateConfig {

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}

```
- The `RestTemplate` bean is manually configured and registered in the application context.


**Features of @Configuration**
1. **Bean Lifecycle Management:**
Ensures that beans are managed by Spring and their lifecycle (creation, initialization, and destruction) is controlled.

2. **Singleton Behavior:**
By default, beans defined in a` @Configuration `class are **singleton**, meaning only one instance is created and shared across the application.

3. **Proxy Enhancements:**
Spring uses **CGLIB proxies** to ensure that bean definitions in the configuration class are processed correctly, even if methods are called multiple times.


![img_11.png](img_11.png)


**Advantages of Using `@Configuration`**
1. **Code Readability:**
Configuration is centralized in a single Java class, making it easier to understand.

2. **Strongly Typed Configuration:**
Unlike XML, Java-based configuration benefits from type checking and IDE support.

3. **Integration with Third-Party Libraries:**
Allows seamless integration by defining third-party beans like `RestTemplate`, `ObjectMapper`, or `DataSource`.

4. **Improved Testability:**
Java-based configurations can be modified or extended in unit tests to simulate different environments.

5. **Cleaner Code:**
Eliminates the need for verbose XML configuration.

**Common Interview Questions**
1. **What is the role of `@Configuration` in Spring Boot?**

- `@Configuration` is used to define and register Spring beans in a Java-based configuration class.
2. **What is the difference between `@Configuration` and `@Component`?**

- `@Configuration` is specifically for defining bean methods, while `@Component` is for general components like services or controllers.
3. **Can a `@Component` class have `@Bean` methods?**

- Yes, but it’s not recommended as it mixes roles. `@Bean` methods should ideally reside in a `@Configuration` class.
4. **What happens if a method in a `@Configuration` class is called multiple times?**

- Spring ensures the method returns the same singleton bean instance, thanks to proxy enhancements.


### 18. What is the purpose of @Entity in Spring Boot?

In Spring Boot (and the broader Java Persistence API - JPA), the `@Entity` annotation is used to mark a Java class as a **persistent entity** or **domain model**. It indicates that the class is mapped to a table in a relational database, enabling object-relational mapping (ORM).

**Purpose of** `@Entity`
1. **Define a Database Table:**
`@Entity` maps a Java class to a corresponding table in the database. Each instance of the class represents a row in the table.

2. **Enable ORM:**
Bridges the gap between Java objects and relational database tables using JPA.

3. **Used with JPA/Hibernate:**
It works in conjunction with other annotations like `@Table`, `@Id`, `@Column`, etc., to customize the mapping between the class and the table.

**How to Use `@Entity`**

To use `@Entity`, follow these steps:

1. Add the `@Entity` annotation to the class.
2. Define a primary key using the `@Id` annotation.
3. Optionally, customize the table or column mapping with annotations like `@Table` or `@Column`.

**Example: Basic Entity Class**
```java
import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class User {

    @Id
    private Long id;
    private String name;
    private String email;

    // Getters and Setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}

```
- Here, the `User` class is marked as an entity.
- It maps to a table named `user` in the database.
- The `id`, `name`, and `email` fields represent columns in the table.

**Customizing Table and Column Mapping**

**Using `@Table` to Customize Table Name**
```java
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name = "users_table") // Custom table name
public class User {

    @Id
    private Long id;
    private String name;
    private String email;
}

```
- The `@Table` annotation customizes the table name to `users_table` instead of the default (`user`).

**Using `@Column` to Customize Column Name**
```java
import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class User {

    @Id
    private Long id;

    @Column(name = "full_name") // Custom column name
    private String name;

    @Column(nullable = false) // Mark as NOT NULL
    private String email;
}

```
- The `@Column `annotation customizes column names or constraints (e.g., `nullable`).

**Why is `@Entity` Important?**

1. **Object-Relational Mapping:**
It allows Java objects to be directly mapped to database tables, simplifying CRUD operations.

2. **Database Independence:**
Applications can work with various relational databases (MySQL, PostgreSQL, etc.) without changing the Java code.

3. **Works Seamlessly with JPA Repositories:**
In Spring Boot, you can use `JpaRepository` or `CrudRepository` to perform database operations on entities.

![img_12.png](img_12.png)

**Spring Boot Example with Repository**

**Entity Class**
```java
import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class Product {

    @Id
    private Long id;
    private String name;
    private Double price;

    // Getters and Setters
}

```
**Repository**

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
}

```
**Service**
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class ProductService {

    @Autowired
    private ProductRepository productRepository;

    public List<Product> getAllProducts() {
        return productRepository.findAll();
    }
}

```

**Key Considerations**
1. **Primary Key Required:**
Every `@Entity` class must have a field marked with `@Id`.

2. **Hibernate Under the Hood:**
Spring Boot uses Hibernate as the default JPA implementation.

3. **Lazy vs. Eager Loading:**
Use `@OneToMany`, `@ManyToOne`, etc., carefully to manage how data is loaded.

4. **Database Schema Generation:**
Spring Boot can auto-generate schema using the `spring.jpa.hibernate.ddl-auto` property (e.g., `create`, `update`).

**Common Interview Questions**
1. **What is the role of `@Entity` in Spring Boot?**

- It marks a class as a persistent entity mapped to a database table.
2. **Can a class without `@Entity` be used as a database table?**

- No. Without `@Entity`, the class will not be recognized by JPA as a database entity.
3. **How does `@Entity` work with `@Table`?**

- `@Table` is used to customize the table name, schema, or catalog for the entity.
4. **What are the requirements for a class annotated with `@Entity`?**

- It must have a primary key field annotated with `@Id`.
5. **What happens if there are no tables corresponding to an `@Entity`?**

- You may encounter an error unless the schema is explicitly created or auto-generation is enabled.


### 19. How do you externalize configuration in Spring Boot?
In Spring Boot, externalizing configuration means storing application settings (like database credentials, server ports, etc.) outside the application code, so they can be easily modified without changing the code. This flexibility allows applications to adapt to different environments, such as development, testing, or production.

**Ways to Externalize Configuration**
1. Application Properties or YAML File
2. Command-Line Arguments
3. Environment Variables
4. Java System Properties
5. Custom Configuration Files
6. Spring Cloud Config Server
7. `@PropertySource` for Custom Properties
8. Programmatically Using `Environment` or `@Value`

**1. Application Properties or YAML File**
   - The most common way to externalize configuration is by using `application.properties` or application.yml in the `src/main/resources` directory.
   
**Example:** `application.properties`
```
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password

```
Example: `application.yml`
```yaml
server:
  port: 8081
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: password

```
- **Advantage**: Simple and supports profiles (e.g., `application-dev.properties` for development).

**2. Command-Line Arguments**

   You can pass properties as command-line arguments when running the application.\
**Example:**
```
java -jar myapp.jar --server.port=9090 --spring.datasource.username=admin

```
- Advantage: Overrides values in a`pplication.properties.`

**3. Environment Variables**\
   Spring Boot automatically picks up configuration values from environment variables.

**Example**:
Set the following environment variables:
```
export SERVER_PORT=8082
export SPRING_DATASOURCE_USERNAME=admin
```
- **Advantage**: Works well in containerized environments like Docker or Kubernetes.

**4. Java System Properties**\
   You can specify configuration as JVM system properties when running the application.

**Example:**

```
java -Dserver.port=9090 -Dspring.datasource.username=admin -jar myapp.jar

```
- **Advantage**: Useful for quick testing and overriding defaults.

**5. Custom Configuration Files**\
   You can create custom property files and load them using @PropertySource or Spring's Environment.

**Example**: Custom File (`custom-config.properties`)
```
custom.greeting=Hello, World!

```
**Loading with** `@PropertySource`
```java
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

@Configuration
@PropertySource("classpath:custom-config.properties")
public class AppConfig {
}

```
**Accessing the Property**
```java
@Value("${custom.greeting}")
private String greetingMessage;

```
**6. Spring Cloud Config Server**\
   For distributed systems, Spring Cloud Config Server provides centralized configuration management.

- Store configuration in a Git repository.
- Different applications and environments can pull their respective configurations.\
**Example**:\
A Git file for production: `application-prod.properties`
```
server.port=8083

```
**7. Using @PropertySource**\
   `@PropertySource `is used to load custom property files into the application context.

**Example**
```java
@Configuration
@PropertySource("classpath:custom.properties")
public class CustomConfig {
}

```
**8. Accessing Properties Programmatically**\
   You can access configuration programmatically using Environment or `@Value`.

**Using** `@Value`
```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class ConfigService {

    @Value("${server.port}")
    private String serverPort;

    public void printConfig() {
        System.out.println("Server Port: " + serverPort);
    }
}

```
**Using `Environment`**
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;
import org.springframework.stereotype.Component;

@Component
public class ConfigService {

    @Autowired
    private Environment environment;

    public void printConfig() {
        System.out.println("Server Port: " + environment.getProperty("server.port"));
    }
}

```

**Profiles for Environment-Specific Configurations**\
Spring Boot supports profiles to manage environment-specific configurations.

**Example:**
- `application-dev.properties` for development:

```
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/devdb

```
- `application-prod.properties` for production:
```
server.port=9090
spring.datasource.url=jdbc:mysql://localhost:3306/proddb

```

**Activating Profiles**
- Using `application.properties:`

```
spring.profiles.active=dev

```
- Using command-line argument:
```
java -jar myapp.jar --spring.profiles.active=prod

```
**Advantages of Externalizing Configuration**
1. **Environment-Specific Configurations:**
Allows seamless switching between environments like dev, test, and prod.

2. **Centralized Management:**
Makes configuration changes easier without modifying code.

3. **Security:**
Sensitive information (e.g., credentials) can be externalized and secured using environment variables or secrets.

4. **Flexibility:**
Configurations can be overridden at runtime using various methods (e.g., command-line arguments).

5. **Scalability:**
Works well with cloud-native applications and containerized deployments.


**Common Interview Questions**
1. Why do we externalize configuration in Spring Boot?

- To make applications adaptable to different environments without code changes.
2. What is the difference between `application.properties` and `application.yml`?

- Both serve the same purpose but differ in syntax; `application.yml` is more structured and hierarchical.
3. How do you handle sensitive information like passwords?

- Use environment variables, encrypted values, or external secrets management tools (e.g., AWS Secrets Manager, HashiCorp Vault).
4. What is the role of profiles in Spring Boot?

- Profiles allow environment-specific configurations, such as `dev`, `test`, or `prod`.
5. How can you access a custom property in Spring Boot?

- Using `@Value` or the `Environment` object.

### 20. What is the difference between application.properties and application.yml?

Both `application.properties` and `application.yml` are used in Spring Boot to configure application settings. The primary difference lies in **syntax**, **structure**, and **readability**. Here's a detailed comparison:

**1. Syntax and Format**\
       `application.properties:`
   - **Key-Value Pair Format**\
   Configuration is written as simple key-value pairs, where each property is specified on a separate line.\
   Example:

```
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password

```
`application.yml:`

- **YAML Format (Hierarchical)**\
Configuration is written in YAML format, using a hierarchical structure with indentation.
Example:
```yaml
server:
  port: 8080
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: password

```
- **Difference in Syntax:** YAML is more structured and uses indentation for hierarchy, while `properties` uses flat key-value pairs.

**2. Readability and Maintainability**
   - `application.properties:`\
   Simple and straightforward, but can become hard to read and maintain for nested or complex configurations.

- `application.yml:`\
Easier to read for complex configurations due to its hierarchical structure. More suitable for nested properties.

**3. Support for Nested Properties**\
   `application.properties:`\
   Nested properties must be written with a **dot (.) notation.**

```
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password

```

`application.yml:`\
Supports **natural nesting** using indentation:
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: password

```
**4. Profiles and Environment-Specific Configurations**\
   Both formats support profiles for environment-specific configurations, but the syntax differs:

`application.properties:`
- Profiles are specified using filenames, like` application-dev.properties` or `application-prod.properties`.
- Activate profiles via `spring.profiles.active`:

```
spring.profiles.active=dev

```
`application.yml:`
- Profiles are embedded within the file using the `---` separator:

```yaml
spring:
  profiles: dev
server:
  port: 8080
---
spring:
  profiles: prod
server:
  port: 9090

```
**5. Error Handling**\
   - ` application.properties:`
   Easier to debug for syntax errors since it's simple key-value pairs.

- ` application.yml:`
YAML is strict about formatting (e.g., indentation, spacing). Improper indentation can lead to runtime errors.

**6. File Size for Complex Configurations**
   - `application.properties:`
   May become lengthy and repetitive when dealing with hierarchical or complex configurations.

- `application.yml:`
More concise due to its hierarchical structure, reducing redundancy.

**7. Compatibility**\
   Both formats are fully supported by Spring Boot. The choice between them depends on personal or team preferences.

![img_13.png](img_13.png)

**Example: Same Configuration in Both Formats**\
`application.properties`
```
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=update

```
`application.yml`
```yaml
server:
  port: 8080
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: password
  jpa:
    hibernate:
      ddl-auto: update

```
**Interview Perspective**
1. **Why does Spring Boot support both `application.properties` and `application.yml`?**

- To provide flexibility. While `properties` is simple and widely used, `YAML` offers better readability for hierarchical data.
2. **Which is better: `application.properties` or `application.yml`?**

- It depends on the use case. For simple flat configurations, `properties` is sufficient, but for complex configurations, `YAML` is more maintainable.
3. **What are the common issues when using `application.yml`?**

- YAML is sensitive to indentation and spacing errors, which can cause runtime exceptions.
4. **Can you use both formats in the same application?**

- Yes. Spring Boot allows the use of both files simultaneously. Properties in `application.properties` will override those in `application.yml` if there are conflicts.

### 21. How to define a custom property in Spring Boot?

Defining a custom property in Spring Boot is straightforward. Spring Boot allows you to declare custom configurations in the `application.properties` or `application.yml` file, and then access these properties in your application using `@Value`, `Environment`, or custom configuration classes.


**Steps to Define a Custom Property**
1. Ad**d the Custom Property**
  - In `application.properties:`

  ```
  app.custom.message=Welcome to Spring Boot!
app.custom.version=1.0.0
```
- In `application.yml`:
```yaml
app:
  custom:
    message: Welcome to Spring Boot!
    version: 1.0.0

```

**2. Access Custom Property in the Application**\
   **Option 1: Using `@Value` Annotation**\
   The `@Value` annotation directly injects the property value into a field or method.

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class CustomPropertyService {

    @Value("${app.custom.message}")
    private String message;

    @Value("${app.custom.version}")
    private String version;

    public void printCustomProperties() {
        System.out.println("Message: " + message);
        System.out.println("Version: " + version);
    }
}

```
**Option 2: Using `Environment` Interface**\
The Environment interface allows you to programmatically fetch property values.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;
import org.springframework.stereotype.Component;

@Component
public class CustomPropertyService {

    @Autowired
    private Environment environment;

    public void printCustomProperties() {
        String message = environment.getProperty("app.custom.message");
        String version = environment.getProperty("app.custom.version");
        System.out.println("Message: " + message);
        System.out.println("Version: " + version);
    }
}
```
**Option 3: Using a Custom Configuration Class**\
Create a POJO (Plain Old Java Object) to bind the custom properties using the `@ConfigurationProperties` annotation.

**Step 1: Create a Configuration Class**
```java
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@ConfigurationProperties(prefix = "app.custom")
public class CustomProperties {

    private String message;
    private String version;

    // Getters and Setters
    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        this.message = message;
    }

    public String getVersion() {
        return version;
    }

    public void setVersion(String version) {
        this.version = version;
    }
}

```
**Step 2: Use the Configuration Class**

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class CustomPropertyService {

    @Autowired
    private CustomProperties customProperties;

    public void printCustomProperties() {
        System.out.println("Message: " + customProperties.getMessage());
        System.out.println("Version: " + customProperties.getVersion());
    }
}

```
**Why Use Custom Configuration Classes?**
1. **Type Safety**: Ensures properties are mapped correctly to fields.
2. **Readability**: Cleaner code compared to `@Value` or `Environment`.
3. **Reusability**: The configuration class can be reused in multiple components.


**Validation for Custom Properties**\
You can add validation constraints to ensure the correctness of property values.

**Example: Add Validation Annotations**
```java
import jakarta.validation.constraints.NotNull;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.validation.annotation.Validated;

@Component
@ConfigurationProperties(prefix = "app.custom")
@Validated
public class CustomProperties {

    @NotNull
    private String message;

    @NotNull
    private String version;

    // Getters and Setters
}

```
**Enable Validation in the Main Application Class**
```java
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}

```
required property is missing, Spring Boot will throw a validation error at startup.

**Example Output**\
Assume the custom properties are defined as:

```
app.custom.message=Welcome to Spring Boot!
app.custom.version=1.0.0

```
**Output:**
```
Message: Welcome to Spring Boot!
Version: 1.0.0

```

**Common Interview Questions**
1. How do you define and use a custom property in Spring Boot?

- Define it in `application.properties` or `application.yml` and use `@Value`, `Environment`, or a custom configuration class.
2. What is the advantage of using `@ConfigurationProperties` over `@Value`?

- `@ConfigurationProperties` provides type safety, better readability, and reusability for structured configurations.
3. How do you validate custom properties in Spring Boot?

- Use `@Validated` on the configuration class and add constraints like `@NotNull`.
4. How does Spring Boot handle missing property values?

- If a property is missing, and no default value is provided, Spring Boot may throw an exception, depending on the access method used.


### 22. What is the use of @Value annotation?

The` @Value` annotation in Spring Framework is used to **inject values into fields, methods, or constructor parameters** from a variety of sources, including:

- Application properties (`application.properties` or `application.yml`).
- cSystem environment variables.
- Inline default values.
- SpEL (Spring Expression Language) expressions.

It simplifies the process of externalizing and managing configurations for Spring-based applications.

**Syntax**
```java
@Value("${property.key:default_value}")
private String variableName;

```
**Primary Use Cases of `@Value`**
1. **Injecting Values from** `application.properties` **or** `application.yml`
   `@Value` allows you to load values directly from your configuration files.

**Example**: In `application.properties:`
```
app.name=SpringBootApp
app.version=1.0.0

```
In the Java class:
```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class AppConfig {

    @Value("${app.name}")
    private String appName;

    @Value("${app.version}")
    private String appVersion;

    public void printConfig() {
        System.out.println("App Name: " + appName);
        System.out.println("App Version: " + appVersion);
    }
}

```
**Output:**
```yaml
App Name: SpringBootApp
App Version: 1.0.0

```
**2. Providing Default Values**\
   You can provide a default value to be used when a property is not found in the configuration.

**Example:**
```java
@Value("${app.description:No description provided}")
private String appDescription;

```
If `app.description` is missing in the configuration file, the value will default to "No description provided".

**3. Reading System Environment Variables**
   You can inject system environment variables using `@Value`.

**Example:**
```java
@Value("${JAVA_HOME}")
private String javaHome;

```
**Output:**
```
JAVA_HOME: /usr/lib/jvm/java-11-openjdk

```
**4. Using Spring Expression Language (SpEL)**\
   `@Value` supports SpEL expressions for dynamic evaluations.

**Example:**
```java
@Value("#{10 + 20}")
private int sum;

@Value("#{systemProperties['user.name']}")
private String userName;

```
**Output:**
```yaml
Sum: 30
User Name: john_doe

```
**5. Injecting Lists or Arrays**
   You can inject comma-separated values into lists or arrays.

**Example:** In `application.properties:`

```
app.supportedLanguages=en,fr,de

```

In the Java class:
```java
@Value("${app.supportedLanguages}")
private String[] supportedLanguages;

```
**Output:**
```
Supported Languages: [en, fr, de]

```
**Advantages of Using `@Value`**
1. **Simplifies Configuration Management:** Easily inject configuration values without boilerplate code.
2. **Supports Default Values:** Ensures no errors occur if a property is missing.
3. **Dynamic Calculations:** With SpEL, you can perform calculations or fetch values dynamically.
4. **Environment Flexibility:** Access environment variables and system properties directly.

**Limitations of `@Value`**
1. **No Type Safety**:` @Value` does not validate property types at compile-time.
2. **Limited to Simple Configurations:** Not ideal for injecting structured configurations (e.g., nested properties).
3. **Hard to Test:** Properties directly injected using `@Value` can be challenging to mock in unit tests.

**Best Practices**
1. Use `@Value` for simple property injections.
2. For complex or structured configurations, prefer `@ConfigurationProperties`.
3. Provide default values to prevent runtime errors if a property is missing.
4. Avoid hardcoding property names; centralize them in configuration files.

**Common Interview Questions**
1. **What is `@Value` used for in Spring Boot?**

- `@Value` is used to inject property values from configuration files, system environment variables, or SpEL expressions into Spring components.
2. **How do you handle missing properties with `@Value`?**

- Provide a default value using the syntax` @Value("${property.key:default_value}")`.
3. **What are the alternatives to @Value for managing configurations in Spring Boot?**

- The `@ConfigurationProperties` annotation is a better alternative for handling complex and nested configurations.
4. **Can you inject lists or arrays using `@Value`?**

- Yes, by providing comma-separated values in the configuration and mapping them to a `String[]` or `List`.


### 23. How to use profiles in Spring Boot?
Profiles in Spring Boot allow you to segregate parts of your application configuration and make it environment-specific. For example, you can have different configurations for **development**, **testing**, and **production** environments.

**Steps to Use Profiles in Spring Boot**\
**1. Define Profile-Specific Configuration Files**\
   You can create separate configuration files for each profile. These files follow the naming convention:
  ` application-{profile}.properties` or` application-{profile}.yml`.

**Example:**

- `application-dev.properties` (for development)
- `application-test.properties` (for testing)
- `application-prod.properties` (for production)

**Content of** `application-dev.properties`:
```
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/dev_db
spring.datasource.username=dev_user
spring.datasource.password=dev_pass

```
**Content of `application-prod.properties:`**

```
server.port=9090
spring.datasource.url=jdbc:mysql://prod.server:3306/prod_db
spring.datasource.username=prod_user
spring.datasource.password=prod_pass

```
**2. Activate a Profile**
   You can activate a specific profile using the spring.profiles.active property.

**Ways to Activate a Profile:**

**a. In** `application.properties`\
Set the active profile globally:
```
spring.profiles.active=dev

```
**b. As a Command-Line Argument**\
While running the application, specify the profile:

```
java -jar myapp.jar --spring.profiles.active=prod

```
**c. As an Environment Variable**\
Set the profile as an environment variable:

```
export SPRING_PROFILES_ACTIVE=test

```
**d. Using VM Options**\
Specify the profile in JVM options:
```
-Dspring.profiles.active=dev

```
**3. Use Profile-Specific Beans**\
   You can define beans that are created only for a specific profile using the @Profile annotation.

**Example:**
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;

@Configuration
public class DataSourceConfig {

    @Bean
    @Profile("dev")
    public DataSource devDataSource() {
        // Configure development DataSource
        return new DataSource("jdbc:mysql://localhost:3306/dev_db", "dev_user", "dev_pass");
    }

    @Bean
    @Profile("prod")
    public DataSource prodDataSource() {
        // Configure production DataSource
        return new DataSource("jdbc:mysql://prod.server:3306/prod_db", "prod_user", "prod_pass");
    }
}

```
When the application is running with the `dev` profile, only `devDataSource()` will be loaded. Similarly, for the `prod` profile, only `prodDataSource()` will be loaded.

**4. Use the @Profile Annotation on Classes**\
   You can annotate entire configuration classes with `@Profile`.

**Example:**
```java
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;

@Configuration
@Profile("test")
public class TestConfig {
    // Beans and configurations specific to the 'test' profile
}

```
**5. Include Multiple Profiles**\
   You can include multiple profiles in the spring.profiles.active property by separating them with commas.

**Example:**

```
spring.profiles.active=dev,test

```
This merges the configurations of the `dev` and `test` profiles.

**6. Use Default Profile**\
   If no profile is explicitly activated, the configuration in the **default profile** (in `application.properties` or` application.yml`) is used.

**Example: Using Profiles in** `application.yml`
```yaml
spring:
  profiles:
    active: dev

---

spring:
  profiles: dev
  datasource:
    url: jdbc:mysql://localhost:3306/dev_db
    username: dev_user
    password: dev_pass

---

spring:
  profiles: prod
  datasource:
    url: jdbc:mysql://prod.server:3306/prod_db
    username: prod_user
    password: prod_pass

```
**When to Use Profiles**
1. Environment-Specific Configurations:

   - Development (`dev`), Testing (`test`), Production (`prod`).
2. Feature-Specific Configurations:

   - Enable/disable certain features based on profiles.
3. Test Isolation:

   - Run different test configurations with profiles like `integration-test` or `unit-test`.

**Advantages of Using Profiles**
1. **Environment-Specific Behavior:** Easily manage configurations for multiple environments.
2. **Modularity:** Simplifies switching configurations without modifying the codebase.
3. **Flexibility:** Activate profiles dynamically at runtime.

**Common Interview Questions on Profiles**
1. **What are profiles in Spring Boot, and why are they used?**

- Profiles allow environment-specific configurations to segregate settings for development, testing, and production environments.
2. **How do you activate a profile in Spring Boot?**

- Using `spring.profiles.active` property in `application.properties`, as a command-line argument, or as an environment variable.
3. **How do you define beans specific to a profile?**

- Use the `@Profile` annotation on bean definitions or configuration classes.
4. **What happens if no profile is activated?**

- The default configuration in `application.properties` or `application.yml` is used.

### 24. What is the role of @Profile annotation?

The `@Profile` annotation in Spring Boot is used to conditionally enable or disable **components**, **beans**, or **configuration** classes based on the currently active profile. It ensures that specific parts of the application are only loaded for certain environments, such as **development**, **testing**, or **production**.

**Key Features of `@Profile`**
1. **Environment-Specific Configurations:**
Load different beans or configurations depending on the active profile.
2. **Conditional Bean Creation:**
Create beans only when the application is running with a specific profile.
3. **Improves Modularity:**
Separates environment-specific logic, making applications more maintainable and scalable.

**How to Use `@Profile`**
1. **On a Configuration Class**\
   Annotate an entire configuration class with @Profile to activate it for a specific environment.

**Example:**
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;

@Configuration
@Profile("dev")
public class DevConfig {

    @Bean
    public String devBean() {
        return "Development Bean";
    }
}

```
In this example, the `DevConfig` class is only active when the `dev` profile is enabled.

**2. On a Bean Definition**\
   You can annotate individual beans within a configuration class.

**Example:**
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;

@Configuration
public class DataSourceConfig {

    @Bean
    @Profile("dev")
    public DataSource devDataSource() {
        return new DataSource("jdbc:mysql://localhost:3306/dev_db", "dev_user", "dev_pass");
    }

    @Bean
    @Profile("prod")
    public DataSource prodDataSource() {
        return new DataSource("jdbc:mysql://prod.server:3306/prod_db", "prod_user", "prod_pass");
    }
}
```
When the `dev` profile is active, `devDataSource()` is used. For the prod profile, `prodDataSource()` is created instead.

**3. For Multiple Profiles**\
   You can specify multiple profiles in the `@Profile `annotation using a comma-separated list.

**Example:**
```java
@Bean
@Profile({"dev", "test"})
public DataSource devAndTestDataSource() {
    return new DataSource("jdbc:mysql://localhost:3306/test_or_dev_db", "test_user", "test_pass");
}

```
This bean will be loaded when either the `dev` or `test` profile is active.

**4. With Default Profile**\
   When no profile is explicitly active, Spring Boot uses the configuration in the **default profile** (`application.properties` or `application.yml`).

**Example:**
```java
@Bean
@Profile("default")
public DataSource defaultDataSource() {
    return new DataSource("jdbc:mysql://localhost:3306/default_db", "default_user", "default_pass");
}

```
**How to Activate Profiles**\
Profiles are activated using the `spring.profiles.active` property.

1. **In** `application.properties` **or** `application.yml`:

```
spring.profiles.active=dev

```
2. **Via Command Line:**
```
java -jar app.jar --spring.profiles.active=prod

```
3. **Environment Variable:**

```
export SPRING_PROFILES_ACTIVE=test

```

**Advantages of` @Profile`**
1. **Environment-Specific Logic:**
Allows you to separate environment configurations without altering the main code.
2. **Reduced Complexity:**
Eliminates the need for conditional checks (`if-else`) in the application logic.
3. **Dynamic Switching:**
Activate or deactivate specific beans or configurations at runtime.

**Common Interview Questions on @Profile**
1. **What is the purpose of `@Profile` in Spring Boot?**

- `@Profile` is used to enable or disable components or beans based on the currently active profile.
2. **Can you use multiple profiles with` @Profile`?**

- Yes, by providing a comma-separated list of profile names in the annotation.
3. **How do you activate a Spring profile?**

- Use the `spring.profiles.active` property in configuration files, as a command-line argument, or as an environment variable.
4. **What happens if no profile is active?**

- Spring Boot falls back to the default profile (defined in `application.properties` or` application.yml`).


### 25. How to use CommandLineRunner in Spring Boot?
The `CommandLineRunner` interface in Spring Boot is a functional interface used to execute code after the application context has been loaded and the application has started. It provides a way to run custom code during the startup of a Spring Boot application.

**Key Features of `CommandLineRunner`**
1. **Runs Code on Application Startup:** Useful for initializing resources, loading data, or performing tasks at startup.
2. **Simplifies Execution:** Runs after all beans are initialized and the application context is ready.
3. **Receives Command-Line Arguments:** You can access the arguments passed to the `main()` method.


**Implementation of `CommandLineRunner`**
1. **Creating a Class That Implements** `CommandLineRunner`\
   You can create a Spring Bean by implementing the CommandLineRunner interface.

**Example:**
```java
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

@Component
public class StartupRunner implements CommandLineRunner {

    @Override
    public void run(String... args) throws Exception {
        System.out.println("Application has started!");
        for (String arg : args) {
            System.out.println("Argument: " + arg);
        }
    }
}

```
**How It Works:**

- The `run()` method is executed after the Spring Boot application has started.
- The `args` parameter contains command-line arguments passed to the application.


**2. Using Lambda Expressions**\
   If you prefer concise code, you can define a CommandLineRunner bean as a lambda expression.

**Example:**

```java
import org.springframework.boot.CommandLineRunner;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class StartupConfig {

    @Bean
    CommandLineRunner runner() {
        return args -> {
            System.out.println("Application started with arguments:");
            for (String arg : args) {
                System.out.println(arg);
            }
        };
    }
}

```
**Passing Command-Line Arguments**\
You can pass arguments when running your Spring Boot application. The `CommandLineRunner` will capture these arguments in its `run()` method.

**Example:** Run the application with arguments:

```
java -jar myapp.jar arg1 arg2 arg3

```
**Output:**
```
Application has started!
Argument: arg1
Argument: arg2
Argument: arg3
```

**Use Cases for `CommandLineRunner`**\
1. **Initializing Data:** Load initial data into the database when the application starts.

```java
@Component
public class DataLoader implements CommandLineRunner {
    @Override
    public void run(String... args) throws Exception {
        System.out.println("Loading initial data...");
        // Add logic to populate the database
    }
}

```
2. **Performing Cleanup Tasks:** Execute tasks such as clearing temporary files or logs at startup.

3. **Debugging or Logging:** Log application configurations or runtime details at startup.

4. **Running Startup Scripts:** Execute custom scripts or tasks when the application is launched.

**Differences Between `CommandLineRunner` and `ApplicationRunner`**
- `CommandLineRunner:`
    - Provides raw command-line arguments as a String[].
- `ApplicationRunner`:
  - Provides parsed command-line arguments via `ApplicationArguments`.
Both serve the same purpose but differ in how they handle arguments.


**Common Interview Questions on `CommandLineRunner`**
1. **What is the purpose of `CommandLineRunner` in Spring Boot?**

- It allows you to run custom code after the application context has been initialized and the application has started.
2. **How do you access command-line arguments in `CommandLineRunner`?**

- Use the `args` parameter of the `run() `method, which contains an array of String arguments.
3. **What is the difference between `CommandLineRunner` and `ApplicationRunner`?**

- `CommandLineRunner` provides raw command-line arguments, while ApplicationRunner provides parsed arguments.
4. **Can you have multiple `CommandLineRunner` beans in a Spring Boot application?**

- Yes, and they will run in the order defined by the `@Order` annotation or their default order.


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
