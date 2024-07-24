---

---
An "object" managed by Spring IOC container used for **Dependency injection**.
- A: 老師
	- 想用影印機影印，A會depent on B, 但係A唔需要理B係咩configuration
- B: 影印機
- IOC container: 影印機舖
 Same context下share嘅object, created for once, reused for all (唔同instance會用)
	- e.g. `chromeDriver()`, `DBConnection()`, `Config`

### LifeCycle
 ![[Pasted image 20240723223744.png\|500]] 
 
```sheet
{
    classes: { 
        class1: { 
            "color": "cyan",
        },
        class2: {
            backgroundColor: "#555",
        }
    },
}
| ----------------- | --- |
| ![[Pasted image 20240723223744.png\|500]]     |                        |
|^ |    |
|^ |    |
|^ |    |
|^ |    |
|^ |    |
|^ |    |
|^ |    |
|^ |    |
|^ |    |
|^ |    |
|^ |    |
```


#### `@Scopes`
- `singleton`: Default, Only one instance is created during the lifetime
- `Prototype`: New object every request of the bean, 
	- NOT managed by lifecycle of spring, need to handled from user
	- Similar to `new`
	- Multi-thread, assign new instance to new thread
### `@autowire`
- 
- `@Autowire` method is called on bean instantiation after
- by name
- @autowired
- by type
- 如果有autowire, object會自己assign from spring ioc

#### Benefits
- Loose coupling
- Reusability of A
	- Do not need to modify, duplicate another A for different configuration of B 

https://stackoverflow.com/questions/32381843/autowired-on-method-in-spring
any method annotated with `@Autowired` is a config method. It is called on bean instantiation after field injection is done. The arguments of the method are injected into the method on calling.

`@Component` and `@Autowired`
https://ithelp.ithome.com.tw/m/articles/10322852
![[Pasted image 20240717031710.png]]

|                                                                                                                                  |                                                                                                                                                                                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [singleton](https://docs.spring.io/spring-framework/reference/core/beans/factory-scopes.html#beans-factory-scopes-singleton)     | (Default) Scopes a single bean definition to a single object instance for each Spring IoC container.                                                                                                                                                         |
| [prototype](https://docs.spring.io/spring-framework/reference/core/beans/factory-scopes.html#beans-factory-scopes-prototype)     | Scopes a single bean definition to any number of object instances.                                                                                                                                                                                           |
| [request](https://docs.spring.io/spring-framework/reference/core/beans/factory-scopes.html#beans-factory-scopes-request)         | Scopes a single bean definition to the lifecycle of a single HTTP request. That is, each HTTP request has its own instance of a bean created off the back of a single bean definition. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| [session](https://docs.spring.io/spring-framework/reference/core/beans/factory-scopes.html#beans-factory-scopes-session)         | Scopes a single bean definition to the lifecycle of an HTTP `Session`. Only valid in the context of a web-aware Spring `ApplicationContext`.                                                                                                                 |
| [application](https://docs.spring.io/spring-framework/reference/core/beans/factory-scopes.html#beans-factory-scopes-application) | Scopes a single bean definition to the lifecycle of a `ServletContext`. Only valid in the context of a web-aware Spring `ApplicationContext`.                                                                                                                |
| [websocket](https://docs.spring.io/spring-framework/reference/web/websocket/stomp/scope.html)                                    | \|   \|<br>\|---\|<br>\|Scopes a single bean definition to the lifecycle of a `WebSocket`. Only valid in the context of a web-aware Spring `ApplicationContext`.\|                                                                                           |
which statement are true?
 yes: Prototype Bean Scope: Only one instance is created ever
 yes : Request Bean Scope: Instance will create and used by every HTTP request. 
 no: Prototype Bean Scope: New instance will create every time. 
yes:  Session Bean Scope: New instance will create and used by single HTTP Session.


```java
@Component
public class RaceTrack {
  private String location;
  private int miles;
  private String trackType;
}

@Component
public class Driver {
  private String name;
  private String team;
  private int yearsExperience;
}

// Then we remove the actual instantiation code from `RaceRound`, instead using the `@Autowired` annotation:
public class RaceRound {
  private String startTime;
  @Autowired
  private RaceTrack currentRaceTrack;
  @Autowired
  private Driver currentDriver;
}
```

- Usage: Share single instance across the context or appllication



If a beans have two constructor, need to explicitly define `@Autowire`. If only one, annotation can be omit
```java
@Component  
public class JdbcRestaurantRepository implements RestaurantRepository {  
  
    private DataSource dataSource;  
	private Map<String, Restaurant> restaurantCache;  

    @Autowired  
    public JdbcRestaurantRepository(DataSource dataSource) {  
       this.dataSource = dataSource;  
       this.populateRestaurantCache();  
    }  
  
    public JdbcRestaurantRepository() {  
    }
```


@PreConstruct
- Execute after bean is created (construcotr is called)
@PreDestroy
## Inversion of control
---
_dependency injection_ (DI)