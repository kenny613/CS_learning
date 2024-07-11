
## Multiple Inheritance
---

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

#### Upcasting

#### Downcasting


```java
public class HelloWorld{
	// version 1: OK!
    public static void doSomethingWith(MyInterface thing) {
        thing.hi();
    }
    public static void main(String[] args) {
        MyInterface foo = new Foo();
        MyInterface bar = new Bar();
        doSomethingWith((Bar)bar);
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
