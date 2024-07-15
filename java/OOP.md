## Interface VS Composition
---

## Multiple Inheritance
---
- A class can inherit from only one abstract class, but it can implement multiple interfaces. This is because an abstract class represents a type of object, while an interface represents a set of behaviors.
## Object casting
---
type only use typed method
```java
interface MyInterface {
    void hi();
}

 class Foo implements MyInterface {
    private void fooFun() {
        System.out.println("foo");
    }
    public void hi() {
        fooFun();
    }
}

 class Bar implements MyInterface {
     public void barFun(){
         System.out.println("bar!");
     }
    public void hi() {
        barFun();
    }
}
```

#### Object Casting
```java
public class HelloWorld{
	// version 1: OK!
    public static void doSomethingWith(MyInterface thing) {
        thing.hi();
    }
    public static void main(String[] args) {
        MyInterface foo = new Foo();
        MyInterface bar = new Bar();
        doSomethingWith(bar);
    }


	// version 2: OK! Upcasting
    public static void doSomethingWith(MyInterface thing) {
	    // Object upcasting Bar -> MyInterface
        thing.hi();
    }
    public static void main(String[] args) {
        MyInterface foo = new Foo();
        MyInterface bar = new Bar();
        doSomethingWith((Bar)bar);
    }


	// version 3: ERROR: Implicit downcasting 
    public static void doSomethingWith(Bar thing) {
        thing.hi();
    }
    public static void main(String[] args) {
        MyInterface foo = new Foo();
        MyInterface bar = new Bar();
        // incompatible types: MyInterface cannot be converted to Bar
        // doSomethingWith(bar);
    }


	// version 4: OK! Explicit downcasting 
    public static void doSomethingWith(Bar thing) {
        thing.hi();
    }
    public static void main(String[] args) {
        MyInterface foo = new Foo();
        MyInterface bar = new Bar();
        // Explicit Downcasting is required
        doSomethingWith((Bar)bar);
    }
}
```
