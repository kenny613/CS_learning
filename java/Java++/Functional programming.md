---

---

## Method References
---
```java
numbers.forEach((number) -> NumberUtils.evenOrOdd(number));
// Change to method references
numbers.forEach(NumberUtils::evenOrOdd);
```

## `Consumer & BiConsumer` 
---
- `functional interface` used in `forEach`
```java
public void forEach(
	java. util. function. BiConsumer<? super K, ? super V> action )
public void forEach( 
	java. util. function. Consumer<? super T> action )
```
## Lambda Expression
---
```java
Predicate<String> largerThan5 = 5 -> s.length() > 5;
boolean result = largerThan5.test("test");
System.out.println(result);

Consumer<String> printUpperCase = s -> System.out.println(s.toUpperCase());
printUpperCase.accept("hello functional programming");

doSomething(largerThan5);
doSomething(s -> s.startsWith("A"));

public static void doSomething(Predicate<String> p){
	System.out.println(p.test("doSomething"));
}

## Stream API
---
```java
// Stream from collection
List<String> names = Arrays.asList("Lori", "Christa", "Maaike");
Stream<String> nameStream = names.stream();

// Creating a Stream from an Array
String[] namesArray={"Isra", "Jonsa", "Gaia"};
Stream<String> nameArrayStream = Arrays.stream(namesArray);

// Creating a Stream using Stream.of()
Stream<String> namesOfStream = Stream.of("Ismael", "David", "Andreas");
```
#### Intermediate Operations
- `filter`
- `map`
- `flatMap`
#### Terminal Operations
- `forEach`
- `collect`
- `reduce`

#### Exercise: using `flatMap` to split `List<String>` into `List` of character
```java
List<String> messi = Arrays.asList("Leo","Messi");
List<String> messiSplit = hi.stream()
					.flatMap(s -> Arrays.stream(s.split("")))
					.collect(Collectors.toList());		
```

#### Exercise: Sort object based on particular attributes
```java
// Easiest
objs.stream.sorted().collect(Collectors.toList());
// More fancy
List<Obj> res = objs.stream().sorted((a,b)->a.val.compareTo(b.val)).collect(Collectors.toList())
```
- `(a,b)->a.val.compareTo(b.val)` is a `Comparator`
