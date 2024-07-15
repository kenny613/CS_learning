---

---
---
https://sites.google.com/im.fju.edu.tw/web/spring-framework-web/spring-controller
## Model

```java
package com.example.demo.entity;

public class Customer {
	private String name;
	private String address;
	private int weight;
	
	public String getName() {
		return name;
	 }

	public void setName(String name) {
		this.name = name;
	 }

	public String getAddress() {
		return address;
	}

	public void setAddress(String address) {
		this.address = address;
	}

	public int getWeight() {
		return weight;
	}

	public void setWeight(int weight) {
		this.weight = weight;
	}
}
```

## Controller
---
```java
package com.example.demo.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.servlet.ModelAndView;

import com.example.demo.entity.Customer;

@Controller
public class CustomerController {
    @RequestMapping(value = "/customerCreate", method = RequestMethod.GET)
    public ModelAndView openForm() {
       ModelAndView model = new ModelAndView("customerCreate");
       return model;
    }

    @RequestMapping(value = "/customerCreate", method = RequestMethod.POST)
    public ModelAndView processForm(@ModelAttribute Customer cus) {
       ModelAndView model = new ModelAndView("customerDone");
       model.addObject(cus);
       return model;
    }
    
}
```
## View
---
- In `application.properties`, we use  `thymeleaf` and specific the html file directory to use 
```java
spring.thymeleaf.cache=false  
spring.thymeleaf.enabled=true spring.thymeleaf.prefix=classpath:/templates/  
spring.thymeleaf.suffix=.html  
spring.application.name=Bootstrap Spring Boot
```
- add `html` in `main/java/resources/templates/`
1. `customerDone.html`
```html
<!DOCTYPE html>  
<html lang="en" xmlns:th="http://www.thymeleaf.org">  
<head>  
    <meta charset="UTF-8"/>  
    <title>Create New Customer</title>  
</head>  
<body>  
  
name: <span th:text="${customer.name}">Wu</span>  
address: <span th:text="${customer.address}">Fu Jen</span>  
weight: <span th:text="${customer.weight}">56</span>  
  
</body>  
</html>
```
3. `customerCreate.html`
```html
<!DOCTYPE html>  
<html lang="en" xmlns:th="http://www.thymeleaf.org">  
<head>  
    <meta charset="UTF-8"/>  
    <title>Create New Customer</title>  
</head>  
<body>  
  
<form action="customerCreate" method ="post">  
  
    name:<input type="text" name="name"/><br/>  
    address:<input type="text" name = "address"/><br/>  
    weight:<input type="text" name ="weight"/><br/>  
    <input type="submit" value="Submit"/>  
  
</form>  
  
</body>  
</html>
```

