## Array
---
```java
// array of string with 
String[] foo = new String[7];

// for loop of array
for(i = 0; i < foo.length; i++){
	// do your stuff
}
```

## String
---
```java
String word = "dlln"
char x = word.charAt(0); // "d"
```
## Collection Interface
---
![[Pasted image 20240711030857.png]]
These classes implement `collection` and share the following basic APIs but with different implementation 
	- `add()`
	- `clear()`
	- `size()`
	- `remove()`
	- `contains()`
	- `isempty()`
	- `contains()`
	
`Iterable` is the **Superinterface** of `Collection`, 
	- `forEach()` can be used
	
Cannot hold primitive type
	- `List<int>` is not ok
	- `List<Integer>` is good to go

Hierarchy
![[Pasted image 20240711175756.png]]
## `Deque`
---
Implement `Iterable<E>, Collection<E>, Queue<E>`

This interface extends the [`Queue`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html "interface in java.util") interface. When a deque is used as a queue, FIFO (First-In-First-Out) behavior results. Elements are added at the end of the deque and removed from the beginning. The methods inherited from the `Queue` interface are precisely equivalent to `Deque` methods as indicated in the following table:


Comparison of Queue and Deque methods

| **`Queue` Method**                                                                      | **Equivalent `Deque` Method**                                                                   |
| --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| [`add(e)`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html#add-E-)       | [`addLast(e)`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#addLast-E-)       |
| [`offer(e)`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html#offer-E-)   | [`offerLast(e)`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#offerLast-E-)   |
| [`remove()`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html#remove--)   | [`removeFirst()`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#removeFirst--) |
| [`poll()`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html#poll--)       | [`pollFirst()`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#pollFirst--)     |
| [`element()`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html#element--) | [`getFirst()`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#getFirst--)       |
| [`peek()`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html#peek--)       | [`peekFirst()`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#peek--)          |


## `LinkedList<T>`
---
#### Implemented interfaces:
```java
[Iterable]<E>, [Collection]<E>, [Deque]<E>, [List]<E>, [Queue]<E>
```

#### How to use:
```java
LinkedList<String> foo = new LinkedList<> ();
foo.add("timber");
foo.add(1, "shakes"); // add to position 1
foo.removeFirst();
```



Common methods
- `addFirst`, `addLast()`, `removeFirst()`, `removeLast()`

`LinkedList` is not synchronized, not thread-safe, to make it synchronized:
```java
List<String> syncList = Collections.synchronizedList(foo);
```

`LinkedList` to be used as [[java/Data Structure#`Deque`|`Queue`]]
```java
Queue<Integer> queue = new LinkedList<>();
queue.offer(1);
queue.offer(2);
queue.offer(3);
System.out.println(new ArrayList<>(deque));  // [1,2,3]
queue.peek(); // 1
queue.poll();
System.out.println(queue);
```

#### Time complexity
- **_add()_** – appends an element to the end of the list. It only updates a tail, and therefore, it’s _O(1)_ constant-time complexity.
- _**add(index, element)**_ – on average runs in _O(n)_ time
- **_get()_** – searching for an element takes _O(n)_ time.
- **_remove(element)_** – to remove an element, we first need to find it. This operation is _O(n)._
- _**remove(index)**_ – to remove an element by index, we first need to follow the links from the beginning; therefore, the overall complexity is _O(n)._
- **_contains()_** – also has _O(n)_ time complexity

## `ArrayDeque`
---
Implement `Iterable<E>, Collection<E>, Deque<E>, Queue<E>`

Can be used as queue or stack

## `Stack`
---
```java
// using Stack
Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.push(3);
System.out.println(stack); // prints 1, 2, 3

// using ArrayDeque
Deque<Integer> deque = new ArrayDeque<>();
deque.push(1);
deque.push(2);
deque.push(3);
System.out.println(deque); // prints [3, 2, 1]

queue.peek(); // 1
queue.poll();
System.out.println(queue);
// [2,3]
```

`Stack` is subclass of `vector` , `vector` implements `Deque`
```java
public class Stack<E>
extends [Vector]
```

Why `ArrayDeque` over `Stack`?
1. Better OOP
2. Print in order from top to bottom

Why `Stack` over `ArrayDeque`?
- **[[Concurrency & multithreading#Thread-safe|thread safe]]**

`stack.seek()` to check the top element
`stack.pop()` to pop the top element
`stack.poll()` is Exception free

`ArrayDeque` is not **[[Concurrency & multithreading#Thread-safe|thread safe]]** but **stack** is

## `Queue`
---
```java
Queue<Integer> queue = new ArrayDeque<>();
queue.offer(1);
queue.offer(2);
queue.offer(3);
System.out.println(new ArrayList<>(deque));  // [1,2,3]
queue.peek(); // 1
queue.poll();
System.out.println(queue);
// [2,3]
```


## `Set`
---
```java
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(1);
treeSet.add(2);

Set<String> wordSet = new TreeSet<>(Comparator.comparing(String::length))
wordSet.add("Messi");
wordSet.add("Yaml");
wordSet.add("FDJ");
System.out.println(wordSet); // ["FDJ", "Yaml", "Messi"]
wordSet.add("Xavi");

System.out.println(wordSet); // ["FDJ", "Yaml", "Messi"], unchange because same length is treated as duplicate

```

## `HashMap`
```java
List<String> ips = new ArrayList<String>(); 
Map<String, Integer> m = new HashMap<String, Integer>();
	for(String ip: ips)
    if (!map.containsKey(clazz))
        classes.put(clazz, 0);
    classes.put(clazz, classes.get(clazz)+1);
```

Allows `null` but `hashTable` does not

## StringBuilder
---


## Collection comparison
---
#### `hashTable` vs `hashMap`

| `hashtable`           | `hashMap`     |
| --------------------- | ------------- |
| Synchronized          | Unsychronized |
| does not allow `null` | Allows `null` |
|                       |               |
|                       |               |

### `List` vs `ArrayList` vs `LinkedList`
- `List` is an `interface`
- 
#### `LinkedList` vs `ArrayList`
	- Adding element
		`LinkedList` is quicker than `ArrayList` because `ArrayList` can get resized (Amortized time complexity)
	- Random element access
		`ArrayList` is quicker than `LinkedList` because `ArrayList` is in **locality of reference**
		
#### `LinkedList` vs `ArrayDeque`

|                                         | `LinkedList` | `ArrayDeque` |                                                                                                                                                                                                                                            |
| --------------------------------------- | ------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Element access                          | Slower       | Faster       | [[java/Data Structure#Locality of references\|contiguous space]], $O(n)$ for `Linkedlist`                                                                                                                                                  |
| Adding/Removing element at start or end | Slower       | Faster       | Node (memory) has to be created/ removed for `LinkedList`                                                                                                                                                                                  |
| Adding/Removing element in the middle   | Faster       | Slower       | 1. create a new node to hold the element;<br>2. set the _next_ pointer of the previous node to the new node;<br>3. set the _next_ pointer of the new node to the next element in the list.<br>while `ArrayDeque` has to shrift the element |
| `null`-able?                            | Yes          | No           |                                                                                                                                                                                                                                            |

# Glossary
---
#### Locality of references
-  contiguously in memory