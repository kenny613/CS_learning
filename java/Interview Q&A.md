
## Java Basics
---
#### Call by references or call by value?
- Pass by value, The object reference (aka. address) is passed by value in the method
```java
public static void main(String[] args) {
    Dog aDog = new Dog("Max");
    foo(aDog);
}
```
- Version 1: `d` is assigned to new object, object referred by `aFog` wont get updated
```java
public static void foo(Dog d) {
    d.getName().equals("Max"); // true
    // change d inside of foo() to point to a new Dog instance construct red with name member variable set to "Fifi"
    d = new Dog("Fifi");
    d.getName().equals("Fifi"); // true
}
```
 Version 2: `d` is NOT assigned to new object, object referred by `aFog` get updated
```java
public static void foo(Dog d) {
    d.getName().equals("Max"); // true
    // change d inside of foo() to point to a new Dog instance construct red with name member variable set to "Fifi"
    d = new Dog("Fifi");
    d.getName().equals("Fifi"); // true
}
```

#### How is **Type coercion** in java?
![[Pasted image 20240728195013.png|500]]

#### How to handle integer overflow?
- Use BigInteger
https://archive.ph/4vZBs

#### Difference between segmentation fault and stack overflow?
- Segmentation fault: Invalid memory access, access outside program reserved memeory
	- Accessing non-reserved memory
		- `int *p = (int*)0xC0000fff; *p = 10;
		- `char c[10]; printf("%c", c[180000]);`
	
- Stack overflow: Exhausted all stack space, segment outside reserved area will be access
	- Will cause segmentation fault
	- e.g. : `int array[1000000];`


#### what does `final` keywords and immutability?
- `final` disallow us to change the **reference** of the variable but not immutability
```java
final StringBuffer a = new StringBuffer("immutable"); 
a = new StringBuffer(""); // Error, cannot change reference
StringBuffer b = new StringBuffer("immutable"); 
b = new StringBuffer(""); // Ok, create new memory and change references
a.append(" broken!"); // ok because final != immutability
```

#### Why is `String` immutable
- Security
- Thread-safe
- Cache 

#### `equals` VS `==`
- `==` compares the exact reference
- `equals` as an API to compare content of two objects
 
#### `public` vs `protected` vs `friendly` vs `private`

| 作用域       | 当前类 | 同一package | 子孙类 | 其他package |
| :-------- | :-- | :-------- | :-- | :-------- |
| public    | √   | √         | √   | √         |
| protected | √   | √         | √   | ×         |
| friendly  | √   | √         | ×   | ×         |
| private   | √   | ×         | ×   | ×         |

#### Overriding vs overloading
|                    | Method Overloading                                                                | Method Overriding                                                                                                                         |
| ------------------ | --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| compile vs runtime | Compile-time polymorphism.                                                        | Run-time polymorphism.                                                                                                                    |
| Why?               | Method overloading helps to increase the readability of the program.              | Method overriding is used to grant the specific implementation of the method which is already provided by its parent class or superclass. |
| Within class?      | It occurs within the class.                                                       | It is performed in two classes with inheritance relationships.                                                                            |
| Inheritance.       | Method overloading may or may not require inheritance.                            | Method overriding always needs inheritance.                                                                                               |
| Signatures.        | Same name but different signatures.                                               | Same name and same signature.                                                                                                             |
| Return type        | Return type can or can not be the same, but we just have to change the parameter. | Return type must be the same or co-variant.                                                                                               |
| Blindg             | **Static binding** is being used for overloaded methods.                          | **Dynamic binding** is being used for overriding methods.                                                                                 |
| Scope              | Private and final methods can be overloaded.                                      | Private and final methods can’t be overridden.                                                                                            |
| Arguemnts          | The argument list should be different while doing method overloading.             | The argument list should be the same in method overriding.                                                                                |
**Static method** CANNOT be overriden


```java
   private static long[] waysToChooseSum(long left, long right) {
        long ways = 0;
        long maximumWinners = 0;

        String s1 = String.valueOf(left);
        String s2 = String.valueOf(right);

        for(int sum = 1; sum <= 9 * s2.length(); sum++) {
            long winners = solve(s2, right, sum) - solve(s1, left, sum);
            if (winners > maximumWinners) {
                ways = 1L;
                maximumWinners = winners;
            } else if(maximumWinners == winners) {
                ways++;
            }
        }
        return new long[] { ways, maximumWinners };
    }

    private static long solve(String s, long n, int sum) {
        return solve(s, n, 0, sum, 1, new Integer[s.length()][9 * 19 + 1][2]);
    }

    private static int solve(String s, long n, int pos, int sum, int tight, Integer[][][] dp) {
        if(sum < 0) return 0;
        if(pos == s.length()) return sum == 0 ? 1 : 0;
        if(dp[pos][sum][tight] != null) return dp[pos][sum][tight];

        int ans = 0;
        int maxLimit = tight == 1 ? s.charAt(pos) - '0' : 9;
        for(int i = 0; i <= maxLimit; i++) {
            int nextTight = tight == 1 && i == maxLimit ? 1 : 0;
            int nextSum = sum - i;
            int nextPos = pos + 1;
            ans += solve(s, n, nextPos, nextSum, nextTight, dp);
        }

        return dp[pos][sum][tight] = ans;
    }
```

#### Difference between Comparator and Comparable
https://medium.com/@kulkarnishruti/ubs-interview-question-associate-director-role-why-do-we-need-both-comparable-and-comparator-d0e2d2db094b
- `Comparable` is for `compareTo(Object obj)`, needs to `implement` for custom class
- `Comparator` is for `compare(Object obj1, Object obj2)`, needs to `implement` for custom class
- Overriding `CompareTo`
```java
@Override
public int compareTo(Person o) {
	if (this.age > o.getAge()) {
		return 1;
	}
	if (this.age < o.getAge()) {
		return -1;
	}
	return 0;
}

class RatingCompare implements Comparator<Movie> 
{ 
	public int compare(Movie m1, Movie m2) { 
		if (m1.getRating() < m2.getRating()) return -1; 
		if (m1.getRating() > m2.getRating()) return 1; 
		else return 0; 
	} 
}
// Method 1 
Collections.sort(movies, ratingCompare);
// Method 2
movies.stream().sorted((m1,m2) -> {
	if (m1.getRating() < m2.getRating()) return -1; 
	if (m1.getRating() > m2.getRating()) return 1; 
	else return 0; 
}).collect(Collectors.toList())
// Method 3 with Comparator
movies.sort(ratingCompare);
```


## Data Structure
---
#### How to use object as `hashMap`key?
	- Need to implement `hashCode` and `equals`

## OOP
---
#### Inheritance vs Polymorphism
Inheritance 
- _using the structure and behavior of a super class in a subclass.
Polymorphoism
- changing the behavior of a super class in the subclass.
- requires inheritance
- `Overloading`: Compile-time poly
- `Overrriding`: run-time poly


## Multithreading
#### What is the difference between `submit()` and `execute()` in `ExecutorService`?
- `submit` return `Future` that the return value can be obtain using `get()`, while `execute` could not
---
#### What is the difference between `synchronzied` and `RetenterLock`?
- `Thread` can acquire a `ReenterLock` multiple times, useful in a `Thread` calling two method that is supposed to be `suycrhonized` or atomic
	- e.g.  A thread call`get()` in method A  and `set()` in method B

- 
- Spring Framework - Java 8 features - Database Optimization - Java Collections

- stream()
- https://www.youtube.com/watch?v=0wN8ruggQxE&ab_channel=Let%27sEase
- https://www.youtube.com/watch?v=EIk7StpEO6k&ab_channel=MCAboyonRoad
- https://www.youtube.com/watch?v=dDYrbuyGoyw&ab_channel=minoractivity
- https://www.udemy.com/course/java-interview-questions-and-answers/?couponCode=ST9MT71624
- https://medium.com/@kulkarnishruti/ubs-java-developer-hackerrank-mcq-on-concurrent-threads-9407965cf4b5
- https://github.com/Devinterview-io/java-interview-questions

Q. What is Java?

Q. What is JVM and JRE?

Q. What does platform independence mean, is java fully platform independent. Explain?

Q. What is object oriented programming mean? Difference between Structured programming and Object oriented programming.

Q. Difference between object oriented programming and object based programming?

Q. What is an object. explain with real world example?

Q. What is class, interface, abstract class?

Q. Difference between abstract class and interface?

Q. What is inheritance, polymorphism, encapsulation, abstraction and there real world examples?

Q. What is method overloading and overriding, Difference between them? Can you give a real world example?

Q. Explain public static void main( String args{}){}. If I change args with anything will it compile, and why its is public and why it is void and static?

Q. Is main a keyword?

Q. If I change main with your name will it compile? yes or no with explanation?

Q. Explain System.out.println()?

Q. How many public classes can there be in a program file?

Q. My class name is A, Can I save it with other name?

Q. There are multiple classes in a program let say A, B, C and I have main in A can I save it with name of class like B and C?

Q. There are multiple Classes in a program A, B , C and class B is public can I save it with A’s name or C’s name?

Q. There are multiple Classes in a program A, B , C and non of them is public will it compile?

Q. Write command to compile and execute java program on command line interface?

Q. How many main() can there be in a class?

Q. Can main() be overloaded?

Q. Is null a keyword? is main a keyword?

Q. What is transient keyword?

Q. What is volatile keyword?

Q. Explain assert keyword.

Q. Explain difference between Class variable, instance variable, and reference variable.

Q. What is an array?

Q Difference between ++i and i++.

Q. Write syntax for an array of size 10;

Q. What is static keyword?

Q. Explain final, finally and finalize?

Q. Name few final classes.

Q. Difference between final and static.

Q. What is constructor? What is return type of constructor?

Q. What is default constructor?

Q. What is Parameterized constructor?

Q. Syntax for inheritance of class.

Q. Class A extends B and Class C extends Class A. What is the order of execution of constructor? or Similar to this question.

Q. If I want to use a method of class without its instance what should I do.

Q. When I use static method what happens in the memory.

Q. how can I create an instance variable?

Q. Syntax for interface inheritance.

Q. Can we declare data members in interface? and what type of?

Q. What is default access modifier of interface methods?

Q. Can interface extends other interface?

Q. Difference between public and default ?

Q. Can we create reference variable of interface and abstract class?

Q. How can we make a class abstract?

Q. What is concrete class? What is a factory method?

Q. What is Object class? What methods it provide.

Q. What is Singleton Class? Write a Singleton class. Name a single class.

Q. Create a class such that there can be only 5 instances of it created.

Q. Can Constructor be inherited?

Q. What is super keyword? What is this keyword?

Q. Can I write super() and this() both in the same constructor?

Q. How can prevent a method from method overriding?

Q. What is an Exception?

Q. If divide double a=0.0/0.0, will it throw exception , if yes then what?

Q. What exception will be thrown when you try to access element of array length?

Q. What exception is thrown when a number is divided by 0?

Q. What is a NullPointerException?

Q. Explain try, catch, finally, throw, throws?

Q. How many catch blocks can there be for a try block?

Q. Can there be no catch block?

Q. How can you create you own exception?

Q. Custom created exceptions are checked or unchecked?

Q. Does finally always executes?

Q. If I write System.exit(1), will finally block execute.

Q. What we generally write in finally block?

Q. How is Garbage collection performed in Java. Explain behind the scene mechanism.

Q. How JVM decides which object is eligible for garbage collection?

Q. If I call System.gc(); will there be garbage collection?

Q. What are memory block is Java? How memory is allocated, explain?

Q. What is String?

Q. Are String s=”Quora” and String s= new(“Quora”); same?

Q. Can we change String after its creation or Strings are immutable explain?

Q. How can we create mutable Strings?

Q. Explain is equals() method?

Q. Exaplain is toString method? and show its usage in example?

Q. Explain is hashcode()?

Q. Difference Between StringBuffer and StringBuilder and String.

Q. How can we compare two Strings?

Q. Questions related to String operations like replace, getting Character at specific position , concatenation of strings etc.

Q. What is a Thread? What is a Process? How thread is different from Process.

Q. What is multithreading?

Q. What is deadlock? How can you prevent it, avoid it?

Q. Explain Life Cycle of Thread.

####  **Q. What is synchronization? What is mutex? What is semaphore? What is monitor? What is Critical Section?**

Q. Explain creation of a thread?

Q. What is wait, notify, notifyall, join?

Q. How to suspend a thread?

#### Q. Which is better for creation of a Thread, extends Thread Class or implement Runnable interface? Why?**

Q. How many thread we can create?

Q. Give real world example of Mutlithreading?

Q. What is serialization? What is deserialization?

Q. How can you create a synchronized object?

Q. Explain synchronized keyword.

####  **Q. Explain synchronized method, object, block.**

Q. Explain hierarchy of InputStream and OutputStream?

Q. What is Autoboxing and Unboxing?

Q. Write examples of Autobxing and unboxing.

Q. What is Collections?

Q What is collection?

Q. Explain Hierarchy of Collection?

Q. What is List, ArrayList, LinkedList, Queue, Deque, Set, HashSet, Map, Tree, TreeSet?

Q. Difference between ArrayList and Array.

Q. Difference between List and LinkedList.

Q. Difference between List, Set, Map?

Q. Difference between Vector and ArrayList.

Q. Difference between HashMap and HashSet.

Q. Difference between Comparator and Comparable.

Q. How can you sort a collection?

Q. How TreeSet sort object to store in TreeSet?

Q. What are Legacy classes? Name some Legacy Classes.

Q. What is super class of Stack? or Name sub classes of Vector.

Q. How will you get a synchronized collection or how can you synchronize collections?

Q. How will you create a file?

Q. Advantages of Character based Stream over Byte based Stream?

Q. Write a program of Stack and Queue?

Q. Difference between Iterator and ListIterator?

Q. How many types of database connections are there in java?

Q. Exaplain type 1 and type 4 Database connctions?

Q. How a database is connected in java?

Q. Explain rawQuerry, statement, prepareStatement,ResultSet.

If I will remember more Questions later , then I will edits questions