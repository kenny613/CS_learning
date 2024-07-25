---
aliases:
---

---
```java
import java.lang.annotation.Retention;
import java.lange.annotation.RetentionPolicy;

@Target(ElementType.METHOD) // only be used in method
@Retention(RetentionPolicy.RUNTIME) // retain only in runtime
public @interface MyAnnotation{
	int priority() default 1;
	String[] tags default {};
}
```
#### Target
Target 是用來告訴 Java 你的 Annotation 是想要標記在哪一些元素類別上，包括 TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, ANNOTATION_TYPE 等等…。在一般來說，我們最常用的應該也是有列出來的這些，像是 TYPE 其實就包括了我們常用的 Class, Interface, Enum 了。

#### Retention
Retention 字面上的意思是『保留』，而實際上真的也是在做 Annotation 的保留策略，主要有以下三種策略：SOURCE, CLASS (default), RUNTIME。
SOURCE 的意思就是你所使用的 Annotation 在 compile 後會被丟掉，如果要以最簡單的看法去理解這件事，可以看 IDE 在幫你 compile 後的 target 資料夾，會發現 @Data 的標記不見了，反而多了很多 Getter Setter。
另外 CLASS 與 RUNTIME 的差別就在 VM 是否會記得你所寫的 Annotation，並且只有**後者**能夠透過 reflection 去存取與使用元件。所以一般你若是需要進行一些業務邏輯的處理時，則都會宣告 ElementType.RUNTIME（但這就會很好奇為什麼 CLASS 會是預設值了）…。

#### interface
如果說 interface 是一個給 implemented class 的介面，那 @interface 就是一個給 Annotation 互動的介面，因此所有的 Annotation 在宣告時都需要使用 @interface。並且在現在會有越來越多人不想寫 Comment，反而透過這種方式寫註解。

## Reflection API
---
![[Pasted image 20240713170323.png]]
- Examine the behavior or modify the behavior of classes or methods
```java
import java.java.reflect.Method;

public class ReflectionExample{
	public static void main(String args[]){
		Class<?> infoClass = Class.forName("com.linkdein.mod3annotations.info");
		Object instance = infoClass.getDeclaredConstructor().newInstance();
		Method method = infoClass.getMethod("getDetailedInfo");
		method.invoke(instance);
	}
}
```
1. Get `Class`: `com.linkdein.mod3annotations.info` 
2. Create `Object` instance of `Class: `com.linkdein.mod3annotations.info` `
3. Get `Method`: `getDetailedInfo`
4. Invoke `Method`:`getDetailedInfo` into instance 
