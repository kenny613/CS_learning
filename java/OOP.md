## Interface VS Composition 
---


## Interface VS Abstract Class
---

|          | Interface                            | Abstract Class                                                                        |
| -------- | ------------------------------------ | ------------------------------------------------------------------------------------- |
| Multiple | Multiple `implement` allowed         | Multiple `extends` NOT allows                                                         |
| Field    | Must be `public static`              | No Restriction                                                                        |
| Method   | Must be implemented in derived class | Must be `@override `with `abstract` *(`default` method in Java 8 without overriding)* |


## Functional Interface
---
- **Runnable –>** This interface only contains the run() method.
- **Comparable –>** This interface only contains the compareTo() method.
- **ActionListener –>** This interface only contains the actionPerformed() method.
- **Callable –>** This interface only contains the call() method.

```java

```
## Multiple Inheritance
---
- A class can inherit from only one abstract class, but it can implement multiple interfaces. This is because an abstract class represents a type of object, while an interface represents a set of behaviors.
## Object casting
---
- `A a = new B()`
	- Call `B` only method return error
	- `a instanceOf B == true`

```java
class A{
    public void sayHi(){ "Hi from A"; }
}
class B extends A{
    public void sayHi(){ "Hi from B"; 
    public void sayGoodBye(){ "Bye from B"; }
}
class C extends A{
    public void sayHi(){ "Hi from C"; 
    public void sayGoodBye(){ "Bye from C"; }
}
main(){
	A a = new B();

	// Call sayHi() in B because overrided
	a.sayHi(); 
	// Compile error because 'a' is declared to be of type 'A' which doesn't have the
	a.sayGoodBye(); 
	// Works as long as the object pointed to by the a variable is an instanceof B. This is
	((B)a).sayGoodBye();
	
	System.out.println(a instanceof A); // true  
	System.out.println(a instanceof B); // true
	System.out.println(a instanceof C); // false  
}
```

#### Downcasting & upcasting

| Upcasting   | Child cast -> Parent |
| ----------- | -------------------- |
| Downcasting | Parent cast -> Child 

- TLDR: If Type definition is **parent** class, cannot pass to **child** class argument, reverse is ok

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
    
	// version 5: OK! parent class arguemnt type accept child class 
	public static void doSomethingWith(MyInterface thing) {  
	    // Object upcasting Bar -> MyInterface  
	    thing.hi();  
	}  
	public static void main(String[] args) {  
	    MyInterface foo = new Foo();  
	    Bar bar = new Bar();  
	    doSomethingWith(bar);  
	}
}
```
