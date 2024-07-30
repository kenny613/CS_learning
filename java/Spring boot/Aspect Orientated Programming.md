## `@PointCut`
---
```java
@Pointcut("execution(public * com.codingmore.controller.*.*(..))") 
public void webLog() { } 

@Before("webLog()") 
public void doBefore(JoinPoint joinPoint) throws Throwable { } 

@AfterReturning(value = "webLog()", returning = "ret") 
public void doAfterReturning(Object ret) throws Throwable { }
```


## Appendix
---
https://www.edureka.co/blog/spring-aop-tutorial/

@ContextConfiguration
