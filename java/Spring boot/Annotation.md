---

---

## Web
----
#### `@RestController`, meaning it is ready for use by Spring MVC to handle web requests. 
- Combining `@Controller` and `@ResponseBody` 
#### `@GetMapping` 
- maps `/` to the `index()` method. When invoked from a browser or by using curl on the command line, the method returns pure text. 
- 
#### `@RequestParam` 時，
- For URL：http://host:port/path?參數名=參數值
#### `@PathVariable`時，
- for URL：http://host:port/path/參數值
```java
@RequestMapping("/hello/{id}")
    public String getDetails(@PathVariable(value="id") String id,
    @RequestParam(value="param1", required=true) String param1,
    @RequestParam(value="param2", required=false) String param2){
.......
}
```