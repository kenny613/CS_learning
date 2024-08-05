-  Cross-cutting concerns
	- Different breakpoint
	- during, before and after exception of a certain class or method
	- Usage
		- logging
		- Validation
		- Error/ Exception handling
	- 
- ==`@Aspect` and `@Componenet` must be added together so Spring will register them as `bean`==

## `@PointCut`
---
- Usually using `@Pointcut` return a dummy function
```java
@Pointcut("execution(public * com.codingmore.controller.*.*(..))") 
public void webLog() { } 

@Before("webLog()") 
public void doBefore(JoinPoint joinPoint) throws Throwable { } 

@AfterReturning(value = "webLog()", returning = "ret") 
public void doAfterReturning(Object ret) throws Throwable { }
```

```java
@Around("execution(* rewards.internal.*.*Repository.update*(..))")  
public Object monitor(ProceedingJoinPoint repositoryMethod) throws Throwable {  
    String name = createJoinPointTraceName(repositoryMethod);  
    Monitor monitor = monitorFactory.start(name);  
    try {  
       // Invoke repository method ...  
       return repositoryMethod.proceed();  
       //  TODO-08: Add the logic to proceed with the target method invocation.  
       //  - Be sure to return the target method's return value to the caller  
       //    and delete the line below.  
    } finally {  
       monitor.stop();  
       // Do not modify this log message or the test will fail  
       logger.info(AROUND + " advice implementation - " + monitor);  
    }  
}
```
## Advice 
---

| Advice            | Arguments                                |
| ----------------- | ---------------------------------------- |
| `@Before`         | `(JoinPoint joinPoint){ ... }`           |
| `@Around`         | `(ProceedingJoinPoint joinPoint){ ... }` |
| `@AfterReturning` | `(JoinPoint joinPoint){ ... }`           |
| `@AfterThrowing`  | `(JoinPoint joinPoint){ ... }`           |


## Logging of throwing Excepton
```java
@AfterThrowing(value="execution(public * rewards.internal.*.*Repository.*(..))", throwing="e")  
public void implExceptionHandling(RewardDataAccessException e) {   
    // Log a failure warning  
    logger.warn(EMAIL_FAILURE_MSG + e + "\n");  
}
```
- `throwing = "e"` have to match with the variable `Exception e` thwoing an exception