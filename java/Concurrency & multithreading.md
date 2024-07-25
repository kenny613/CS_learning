## Synchronized 
---
- Mutual exclusive, locked resouce with one thread is accessing
- like a toilet, the object can be used by only one person (thread). However it is sharable even only one person can use it at one time.
## Concurrent
---
- Allows multiple thread
- like pond, where many person (threads) can solve their different needs. Like washerman washes, some take bath and so on.

## Thread
---
```java
public class ThreadExample extends Thread{
	@Override
	public void run(){
		System.out.println("HEllo");
	}
}

Thread one = new ThreadExample();
Thread two = new ThreadExample();
one.start();
two.start();
```

https://segmentfault.com/a/1190000016611415

## `implements Runnable` vs `extends Thread`
---
- `Runnable` is `interface`, `Thread` is `class`. Able to extend from another class as well
- `Runnalbe` is passed into `thread`, achieving `Composition`
	- `Compoisiton` is believed to be more flexible than `interface`



## `ConcurrentHashMap` vs `SynchronizedHashMap`?
Both maps are thread-safe implementations of the `Map` interface. `ConcurrentHashMap` is implemented for higher throughput in cases where high concurrency is expected.

Brian Goetz's [article](http://www.ibm.com/developerworks/java/library/j-jtp08223/index.html) on the idea behind `ConcurrentHashMap` is a very good read. Highly recommended

#### volitable


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

## Concurrency & multithreading
----
- Doing multiple tasks at the same time, when waiting for external resources, do other things
- `java.util.concurrency`
```java
public class MyThread extends Thread{
	public void run{
		System.out.println("run from thread #" + Thread.currentThread().getId());
	}
}

public class Hi {
	public static void main(String[] args){
		MyThread t1 = new MyThread();
		t1.start();
		MyThread t2 = new MyThread();
		t2.start();
	}
}
```

#### Synchronization
---
```java
public class Hi{
	private int counter = 0;
	
	public synchronized void increment(){
		coutner++;	
	}
}
```
#### Creating ThreadPool
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

#### Timeout and Future
- Goodread on timeout with multithreading
https://stackoverflow.com/questions/22863965/how-future-get-method-works-with-timeout

### How does it works?
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
                executor.shutdown();
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

#### Volatile Keywords