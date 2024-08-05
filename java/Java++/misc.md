## Regex `String.matches(regex)`
---
```java
String regex = "cat|dog|fish";

System.out.println("cat".matches(regex));
System.out.println("dog".matches(regex));
System.out.println("catfish".matches(regex));
System.out.println("doggy bag".matches(regex));
```


## List of situations that cause a `NullPointerException` to occur
---
Here are all the situations in which a `NullPointerException` occurs, that are directly* mentioned by the Java Language Specification:

1. Accessing (i.e. getting or setting) an _instance_ field of a null reference. (static fields don't count!)
2. Calling an _instance_ method of a null reference. (static methods don't count!)
3. `throw null;`
4. Accessing elements of a null array.
5. Synchronizing on null - `synchronized (someNullReference) { ... }`
6. Any integer/floating point operator can throw a `NullPointerException` if one of its operands is a boxed null reference
7. Conversion throws a `NullPointerException` if the boxed value is null.
8. Calling `super` on a null reference throws a `NullPointerException`. If you are confused, this is talking about qualified superclass constructor invocations:

```java
class Outer {
    class Inner {}
}
class ChildOfInner extends Outer.Inner {
    ChildOfInner(Outer o) { 
        o.super(); // if o is null, NPE gets thrown
    }
}
```

9. Using a `for (element : iterable)` loop to loop through a null collection/array.
10. `switch (foo) { ... }` (whether its an expression or statement) can throw a `NullPointerException` when `foo` is null.
11. `foo.new SomeInnerClass()` throws a `NullPointerException` when `foo` is null.
12. Method references of the form `name1::name2` or `primaryExpression::name` throws a `NullPointerException` when evaluated when `name1` or `primaryExpression` evaluates to null.
- 