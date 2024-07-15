---

---
---
- `@RestController`, meaning it is ready for use by Spring MVC to handle web requests. 
	- Combine of `@Controller` and `@ResponseBody`
- `@GetMapping` maps `/` to the `index()` method. When invoked from a browser or by using curl on the command line, the method returns pure text. 