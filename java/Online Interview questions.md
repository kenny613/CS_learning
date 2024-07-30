---
aliases:
---
![[Pasted image 20240715021745.png]]```java
@SharedResource(allowOrigins = "https://www.mystore.com")
```

```java
@CORS(value = "https://www.mystore.com")
```

```java
@AccessControl(allowOrigins = "https://www.mystore.com")
```

```java
@CrossOrigin(origins = "https://www.mystore.com")
```

---
![[Pasted image 20240715021820.png]]

`   @Service`

`@Controller`

`@Configuration`

`@Repository`

---
![[Pasted image 20240715021851.png]]
` @ApiEndpoint("widget")`

`@RestEndpoint("api/widget")`

`@GetMapping("api/widget")`

`@RequestMapping("api/widget")`    

---
![[Pasted image 20240715021929.png]]A
dd `@JsonIgnore` to the getters for `userName` and `timestamp` in `AccessLogData`

Add `mapper.setSerializationInclusion(Include.NON_NULL)` in `JsonConfig.configureJackson()`

Add `@JsonInclude(JsonInclude.Include.NON_NULL)` as a class-level annotation to `AccessLogData`

Add `@JsonFilter(null)` as a class-level annotation to `AccessLogData`

--
![[Pasted image 20240715022000.png]]  
It sets up a complete application context for integration testing

It is required to allow mock services for unit testing

It starts a Spring Boot REPL for manual application probing

It allows application startup if a test case fails

---
![[Pasted image 20240715022024.png]]

---
![[Pasted image 20240715022039.png]]
```java
@CachePut("inventory")
```


```java
@CacheUpdate("inventory")
```

```java
@Cacheable("inventory", operation = CacheOperation.PUT)
```

```java
@CacheRevoke("inventory")
```

---
![[Pasted image 20240715022212.png]]

---
![[Pasted image 20240715022433.png]]

---  
![[Pasted image 20240715022447.png]]

@FunctionalInterface

@lambda

@abstract

@Functional

---
![[Pasted image 20240715022504.png]]

---
![[Pasted image 20240715022551.png]]
---

![[Pasted image 20240715022639.png]]
--
 diff between string andn ew string
---

![[Pasted image 20240715023559.png]]

---
![[Pasted image 20240715025245.png]]

```java
@OneToMany(mappingRelationshipOwner = User.class)
```

```java
@OneToMany(mappedBy = "user")
```

```java
@OneToMany(mappingRelationshipOwner = Address.class)
```

```java
@OneToMany(useParentId = true)
```

---
![[Pasted image 20240715025350.png]]

  
Auto-configuration

Scheduled tasks

Dependency injection

Component scan

---
![[Pasted image 20240715025404.png]]

---

![[Pasted image 20240715025413.png]]

`   EnableWebProcessing`

`EnableBatchProcessing`

`EnableBatch`

`EnableSpringProcessing`

---

![[Pasted image 20240715025428.png]]  
@OAuth2Client

@EnableSso

@EnableOAuth2Client

@OAuth2ClientAutoConfiguration

---
![[Pasted image 20240715025445.png]]
  
Spring Discovery

Spring Boot does it automatically

Spring dev tools

Spring Actuator

---
![[Pasted image 20240715025503.png]]

---
![[Pasted image 20240715025525.png]]

`   UserAuthenticationToken`

`UsernamePasswordAuthenticationToken`

`FilterAuthenticationToken`

`AuthenticationToken`

---
![[Pasted image 20240715025543.png]]


`   @Named`

`@Candidate`

`@Injectable`

`@Validateable`

---
![[Pasted image 20240715030049.png]]![[Pasted image 20240715030058.png]]
---
![[Pasted image 20240715030241.png]]
BigDeciaml