 ## Synchronized 
---
- Mutual exclusive, locked resource with one thread is accessing
- like a toilet, the object can be used by only one person (thread). However it is sharable even only one person can use it at one time.
## Concurrent
---
- Allows multiple thread
- When two or more tasks can start, run, and complete in overlapping time **periods**. It doesn't necessarily mean they'll ever both be
- like pond, where many person (threads) can solve their different needs. Like washerman washes, some take bath and so on.
## Parallelism
---
- when tasks _literally_ run at the same time, e.g., on a multicore processor
## `Thread` & `Runnable`
---
```java
public class ThreadExample extends Thread{
	@Override
	public void run(){
		System.out.println("Hello fro");
	}
}

public class RunnableExample implements Ruunnable{
	@Override
	public void run(){
		System.out.println("HEllo");
	}
}

Thread one = new ThreadExample();
Thread two = new ThreadExample(new RunnableExample());
Thread three = new Thread(() -> {System.out.println("Runnable with Lambda Expression");}) // Runnable Lambda expression
    
one.start();
two.start();
three.start()'
```
- Use `Thread.sleep()`
https://segmentfault.com/a/1190000016611415
https://stackoverflow.com/questions/9072422/difference-between-synchronized-and-re-entrant-lock

#### `implements Runnable` vs `extends Thread`
- `Runnable` is `interface`, `Thread` is `class`. Able to extend from another class as well
- `Runnalbe` is passed into `thread`, achieving `Composition`
	- `Compoisiton` is believed to be more flexible than `interface`


## `Executor` & `ThreadPool`
---
```java
public class ExceutiorsExample{
	public static main void(String[] args){
		ExecutorsService executor = Executors.newFixedThreadPool(5);
		Runnable task = () -> System.out.println("Hello from" + Thread.currentThread().getId());
		for(int i = 0; i < 10; i++){
			executor.exceute(task);
		}
		executor.shutdown();
	}
}

''' Result are different everytime
Output:
Hello from 15
Hello from 17
Hello from 18
Hello from 16
Hello from 19
Hello from 19
Hello from 19
Hello from 19
Hello from 16
Hello from 19
'''
```

## `ReenterLock`
---
- Allow acquiring lock multiple times
- Useful in situation we that we want two operation to be atomic/synchronized, we need to acquire the lock twice
	- Call `get()` and then `set()`
```java
final ReentrantLock lock = new ReentrantLock();

final Object[] objects = new Object[10]
public Object setAndReturnPrevious(int index, Object val){
   lock.lock();
      Object prev = get(index);
      set(index,val);
      return prev;
   lock.unlock();
}
public void set(int index, Object val){
    lock.lock();
         objects[index] = val;
    lock.unlock();
}
public Object get(index index){...}
```
- If `ReentrantLock` wasn't reentrant you would deadlock at `set(index)` 
	- [https://stackoverflow.com/questions/18596080/java-concurrent-reentrantlock-why-we-want-to-acquire-the-same-lock-multiple-ti|]
#### Conditional (like a signal) with `RenenterLock`
```java
@Override
public void t1Run() {
   try {
	   this.lock.lock();
		   System.out.println("RUN THREAD 1-1");
		   this.condition.await(); // Wait for the signal
		   System.out.println("RUN THREAD 1-2");
   } catch(Exception e) {
	   throw new RuntimeException(e);
   } finally {
	   this.lock.unlock();
   }

}

  public void t2Run() {
    try {
      this.lock.lock();
	      System.out.println("RUN THREAD 2");
	      this.condition.signal(); // Fire a signal
    } catch(Exception e) {
      throw new RuntimeException(e);
    } finally {
      this.lock.unlock();
    }
  }
```


## `Future`
---
1. Create Pool of thread `ExecutorService executor = Executors.newFixedThreadPool(5);`
2. Obtain `Future<T>` object by `executor.submit(Callable<T>)`
3. We also need to define the our own `Callcable` task, each to be submit for multi-threads to execute
4. Using `Future.get()` to collect the `<T>`result

#### Exercise: Concurrently compute factorial from input `List<Integer>`
```java
import java.math.BigInteger;
import java.util.*;
import java.util.concurrent.*;

class Answer {
    static boolean showExpectedResult = false;
    static boolean showHints = false;

    static Map<Integer, BigInteger> findAnswer(List<Integer> numbers) {
        HashMap<Integer, BigInteger> m = new HashMap<>();
        ExecutorService executor = Executors.newFixedThreadPool(5);
        List<Future<Map.Entry<Integer, BigInteger>>> futures = new ArrayList<>();

        for(Integer num : numbers){
            futures.add(executor.submit(new FactorialTask(num)));
        }
        for(Future<Map.Entry<Integer, BigInteger>> future: futures){
	        // Try-ctach is a must for future.get()
            try{
                Map.Entry<Integer, BigInteger> entry = future.get();
                m.put(entry.getKey(),entry.getValue());
            }catch (Exception e){
                e.notify();
            }
            finally{
                executor.shutdown(); // Remember to shutdown
            } 
        }
        return m;
    }
}

class FactorialTask implements Callable<Map.Entry<Integer, BigInteger>> {
    public Integer number;

    public FactorialTask(Integer number){
        this.number = number;
    }

    @Override
    public Map.Entry<Integer, BigInteger> call() throws Exception {
        BigInteger result = BigInteger.ONE;
        for (int i = 2; i <= number; i++)
            result = result.multiply(BigInteger.valueOf(i));
        return new AbstractMap.SimpleEntry<Integer, BigInteger>(number, result);
    }
}
```



## `ConcurrentHashMap` vs `SynchronizedHashMap`?
---
Both maps are thread-safe implementations of the `Map` interface. `ConcurrentHashMap` is implemented for higher throughput in cases where high concurrency is expected.

Brian Goetz's [article](http://www.ibm.com/developerworks/java/library/j-jtp08223/index.html) on the idea behind `ConcurrentHashMap` is a very good read. Highly recommended

#### `Volatile` Keywords
---
- "Real-time" Visible to all thread in concurrent scenario
- Does not allow atomic operation
- e.g. `a++` :  Thread 2 read `a` right after Thread 1 read `a`, they both add 1 to a on the old value
## `newWorkStealingPool`
---
- Calling `ForkJoinPool`
- ![[Pasted image 20240730150345.png|500]]

## Thread-safe Collection
---

| synchronized | unsynchronized | concurrentCollection |
| ------------ | -------------- | -------------------- |
| `hashTable`  | `hashMap`      |                      |
| `Stack`      | `Deque`        |                      |
| `Vector`     | `ArrayList`    | `synchronizedList`   |

`hashTable`  is thread-safe, `hashMap` is not. (For concurrency, better to use `concurrentHashMap`)
`Stack` is thread-safe, `Deque` is not
`Vector` is thread-safe, `ArrayList` is not (For concurrency, better to use `concurrentHashMap`)
#### Concurrent collection
---
```java
import java.util.concurrent.ConcurrentHashMap;

public class Hi{
	public static void main(String[] args){
		ConcurrentHashMap<String, Integer> concurrentMap = new ConcurrentHashMap<>();
		concurrentHashmap.add("one", 1);
		concurrentHashMap.forEach((key,value) -> system.out.println(key + ": " + value);
	}
}
```



# Interview Q&A
---
#### What is the difference between `submit()` and `execute()` in `ExecutorService`?
- `submit` return `Future` that the return value can be obtain using `get()`, while `execute` could not
---
#### What is the difference between `synchronzied` and `RetenterLock`?
- `Thread` can acquire a `ReenterLock` multiple times, useful in a `Thread` calling two method that is supposed to be `suycrhonized` or atomic
	- e.g.  A thread call`get()` in method A  and `set()` in method B
---
