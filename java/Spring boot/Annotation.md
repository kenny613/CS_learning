---

---
---

- `@RestController`, meaning it is ready for use by Spring MVC to handle web requests. 
	- Combine of `@Controller` and `@ResponseBody`
- `@GetMapping` maps `/` to the `index()` method. When invoked from a browser or by using curl on the command line, the method returns pure text. 
- `@RequestParam` 時，URL 是這樣的：http://host:port/path?參數名=參數值
- `@PathVariabl`e時，URL是這樣的：http://host:port/path/參數值
```java
@RequestMapping("/hello/{id}")
    public String getDetails(@PathVariable(value="id") String id,
    @RequestParam(value="param1", required=true) String param1,
    @RequestParam(value="param2", required=false) String param2){
.......
}
```