# **Spring Framework

[Baeldung Spring Tutorial](https://baeldung.com/spring-tutorial)

## **Main Parts**  

### **Modules**  

Spring framework is divided into modules:

- **Core**: Provides core features like DI (Dependency Injection), Inernationalization, Valudation, and AOP (Aspect Oriented Programming)
- **Data Access**: Supports data access through JTA (Java Transaction API), JPA (Java persistence API), and JDBC (Java Database Connectivity)
- **Web**: Supports both Servlet API (Spring MVC), Reactive API (Spring WebFlux), WebSockets, STOMP, and WebClient
- **Integration**: Supports integration to Enterprise Java through JMS (Java Message Service), JMX (Java Management Extension), and RMI (Remote Method Incovation)

### **Spring Projects**  

- **Boot**: Provides a set of highly opinionated but extensibles templates for creating carious projects based on Spring in little time. Makes it easy to create standalone Spring apps with embedded Tomcat or similar container.
- **Cloud**: Provides support to easily develop some of the common distributed system patterns like service discovery, circuit breaker, and API gateway. Helps cut down the effort to deploy boilerplate patterns in local, remote, or managed platforms.
- **Security**: Provides a robust mechanism to develop authentication and authorization for projects based on Spring in a customizable manner. With minimal declarative support, get protection againt common attacks like session fixation, click-jacking, and cross-site request forgery.
- **Mobile**: Provides capabilities to detect the device and adapt the app behavior accordingly. Supports device-aware view management for optimal user experience, site preference management, and site switcher. 
- **Batch**: Provides lightweight framework for developing batch apps for enterprise systems like data archival. Has intuitive support for scheduling, restart, skipping, collecting metrics, and logging. Support scaling up for high-volume jobs through optimization and partitioning.

## **Bean Annotations**  

Several ways to configure beans in a Spring container:

- Declare them using XML configuration
- `@Bean` annotation in a configuration class
- Mark the class with one of the annotations from the `org.sringframework.stereotype` package and leave the rest to component scanning

### **Component Scanning** 

Spring can automatically scan a package for beans if component scanning is enabled.

`@ComponentScan` configured which packages to scan for classes with annotation configuration. We can specify the base package names directly with one of the `basePackages` or `value` arguments (`value` is an alias for `basePackages`):

```java
@Configuration
@ComponentScan(basePackages = "com.fancyproject.annotations")
class VehicleFactoryConfig {}
```

Can also point to classes in the base packages with the `basePackageClasses` argument:

```java
@Configuration
@ComponentScan(basePackageClasses = "VehicleFactoryConfig.class")
class VehicleFactoryConfig {}
```

Both arguments are arrays - can provide multiple packages for each.

If no argument is specified, the scanning happens from the same package where the `@ComponentScan` annotated class is present. 

`@ComponentScan` leverages the Java 8 repeating annotations feature, which means we can mark a class with it multiple times:

```java
@Configuration
@ComponentScan(basePackages = "com.fancyproject.annotations")
@ComponentScan(basePackageClasses = "VehicleFactoryConfig.class")
class VehicleFactoryConfig {}
```

Alternatively, we can use `@ComponentScans` to specify multiple `@ComponentScan` configurations:

```java
@Configuration
@ComponentScans({
    @ComponentScan(basePackages = "com.fancyproject.annotations"),
    @ComponentScan(basePackageClasses = "VehicleFactoryConfig.class")
})

class VehicleFactoryConfig {}
```

XML configuration:

```xml
<context:component-scan base-package="com.fancyproject" />
```

### **@Component**

`@Component` is a class level annotation. During the component scan, Spring Framework automatically detects classes annotated with `@Component`:

```java
@Component
class CarUtility {
    // ...
}
```

By default, the bean instances of this class have the same name as the class name with a lowercase initital. A different name can be specified using the optional `value` argument of this annotation.

Since `@Repository`, `@Service`, `@Configuration`, and `@Controller` are all meta-annotations of `@Component`, they share the same bean naming behavior. Spring also automatically picks them up during the component scanning process. 

### **@Repository**

DAO or Repository classes usually represent the database access layer in an application, and should be annotated with `@Repository`:

```java
@Repository
class VehicleRepository {
    // ...
}
```

An advantage of using this annotation is that it has automatic persistence exception translation enabled. When using a persistence framework, such as Hibernate, native exceptions thrown within classes annotated with `@Repository` will automatically be translated into subclasses of Spring's `DataAccessException`.

To enable exception translation, we need to declare our own `PersistenceExceltionTRanslationPostProcessor` bean.

```java
@Bean
public PersistenceExceptionTranslationPostProcessor exceptionTranslation() {
    return new PersistenceExceptionTranslationPostProcessor();
}
```

Note that in most cases, Spring does the above step automatically.

Or via XML configuration:

```xml
<bean class="org.springframework.dao.annotation.PersistenceExceptionTranslationPostProcessor" />
```

### @service

The business logic of an app usually resides within the service layer. The `@Service` annotation indicates that a class belongs to that layer.

```java
@Service
public class VehicleService {
    // ...
}
```

### Controller
 
`@Controller` is a class level annotation. It tells Spring that this class serves as a controller in Spring MVC.

```java
@Controller
public class VehicleController {
    // ...
}
```

### @Configuration

Configuration classes can contain bean definition methods annotated with `@Bean`:

```java
@Configuration
class VehicleFactoryConfig {
    @Bean
    Engine engine() {
        return new Engine();
    }
}
```

### Stereotype Annotations and AOP

When we use Spring stereotype annotations, it's easy to create a pointcut that targets all classes that have a particular stereotype.

For instance, suppose we want to measure the execution time of methods from the DAO layer. We'll create the following aspect (using AspectJ annotations), taking advantage of the `@Repository` stereotype:

```java
@Aspect
@Component
public class PerformanceAspect {
    @Pointcut("within(@org.springframework.stereotype.Repository *)")
    public void repositoryClassMethods() {};

    @Around("repositoryClassMethods()")
    public Object measureMethodExecutionTime(ProceedingJoinPoint joinPoint) 
      throws Throwable {
        long start = System.nanoTime();
        Object returnValue = joinPoint.proceed();
        long end = System.nanoTime();
        String methodName = joinPoint.getSignature().getName();
        System.out.println(
          "Execution of " + methodName + " took " + 
          TimeUnit.NANOSECONDS.toMillis(end - start) + " ms");
        return returnValue;
    }
}
```

In this example, we created a pointcut that matches all the methods in classes annotated with `@Repository`. Then we used the `@Around` advice to target that pointcut, and determine the execution time of the intercepted methods calls.

Furthermore, using this approach, we can add logging, performance management, audit, and other behaviors to each application layer.