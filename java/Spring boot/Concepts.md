---

---
---
### `bean`
	-Me thod to get property of depedent child relaiohship 
### `@autowire`
- by name
- @autowired
- by type



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