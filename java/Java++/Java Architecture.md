![[Pasted image 20240727235159.png|600]]
# JVM
---
- Interpreter + JIT (Just-in-time compiler)
- Interpret and compile Java bytecode (.class files)
- In short run, interpreter is fast, in long run, compiler is faster
	- Run 1 times: Interpreter takes10ms，Compiler takes 102ms 
	- Run 100x times: Interpreter takes 1000ms，Compiler takes 300ms + memoery
	- A counter is used to record the number of execution, if exceed threshold, use compiler
		- The machine code is cached and reused in the future, much faster
		- Further optimize if second threshold has exceed
## JVM Tuning
---
1. Memory
2. Latency (responsiveness)
3. throughput (amount of time)
#### Heap size
- `java -XmX128m`
#### Metaspace size
- `java -XX:MaxMetaspaceSize=4m`
#### GC Type
- `-XX:+UseSerialGC`
- `-XX:+UseParallelGC`
- `-XX:+UseConcMarkSweepGC`


# Garbage Collection
---
- GC on Heap memory
## GC Root
---
- Starting points for GC
- Possible types:
	- Class: Classes loaded by a system class loader; contains references to static variables as well
	- Stack Local: Local variables and parameters to methods stored on the local stack
	- Active Java Threads: All active Java threads
	- JNI References: Native code Java objects created for JNI calls; contains local variables, parameters to JNI methods, and global JNI references
	- Objects used as monitors for synchronization
	- Specific objects defined by the JVM implementation that are not garbage collected for its purpose. That might contain important exception classes, system class loaders, or custom class loaders
- Traverse live objects through object graph, GC root is the starting node
- https://www.jyt0532.com/2020/03/12/garbage-collector/

## Young generation
---
#### Eden space and Survivor space
	- Newly created object will be placed in Eden space
	- After GC, active memory that are still reachable in **Eden space** will be put into survivor space
#### Scavenging
- Copying memory from young generation to old generation

## Old generation
---
- After GC, active memory that are still reachable in **Survivor space** will be put into old generation

## Metaspace (Perm Gen)
---
- Storing these metadata:
	- Klass structure
	- Methods of classes
	- Constants
	- Annotations
	- Optimization
- How metadata is removed after GC?
	![[Pasted image 20240727225215.png|600]]
	- After GC, If there is no more O object references, Metadata O is also removed
	![[Pasted image 20240727225319.png|600]]

- Trigger scenario
1. ==**Metaspace size grow beyond certain threshold**==
2. ==**Metaspace out of memory**==
- E.g. `finalize` to save from dying zone 
```java
public class GarbageCollector {
 public static void main(String... args) throws InterruptedException {
   {
     CustomClassLoader cl;

     for (int i = 0; i < 2; i++) {
       cl = new CustomClassLoader();
       cl = new CustomClassLoader();
       triggerGC();
     }
   }
   triggerGC();
 }

 private static void triggerGC() throws InterruptedException {
   System.out.println("GC start");
   System.gc();
   Thread.sleep(1000);
   System.out.println("GC end");
 }

 private static class CustomClassLoader extends ClassLoader {
   public CustomClassLoader() {
     super();
     System.out.println(this.toString() + " - CL Constructor called.");
   }
   @Override
   protected void finalize() throws Throwable {
     super.finalize();
     System.out.println(this.toString() + " - CL Finalized.");
   }
 }
}
```
![[Pasted image 20240728020701.png|600]]

#### Generational Garbage Collector
- Not focusing on full memory (i.e. only young generation)
- Performance: When to promote memory from young to old???
	- just OK: Memory that died young can be collected
	- Too long: 
		- Take up lots of space, OOM
		- Too long promoting to old generation 
#### Remember set
- Keep ref from objs to young
- Helps the garbage collector to only scan the young generation without needing to scan the old generation for indirect relationships to the stack. These relationships are in the remembered set.
Example:
![[Pasted image 20240804010901.png|500]]
- `E` and `G` are unreachable, when collecting `E` and `G`, `H` and `J` are no longer pointing to `E` and `G`, memory crash
- Remember set records `H->E` and `J->G` from non collected area
- 

## Different GC implementations
---
#### Serial GC
- Young Generation: Mark and Copy
- Old generation: Mark sweep compact
- Single-threaded
- Stop-the-world implementation

#### Parallel GC
- Multiple-threaded serial GC

#### Concurrent Mark Sweep GC 
- Young Generation: Mark and Copy
- Old generation: Mark sweep and mostly concurrent
	- Concurrent with the application
- Multiple-threaded
- Stop-the-world and mostly concurrent
	- Prefer concurrent but stop-the-world if necessary

#### Garbage-First GC
- Divides heap into ==small segments==
- Keep track of amount of live and dead objects
- Concurrent and sop-the-word but shortest pauses possible

#### Z GC
- max 10 ms
- Reference coloring
	- Only works on 64-bit system
- Sweep and copy
- Load barriers 
	- Avoid parallel
- Multiple-threaded
- Concurrent

## Metrics for GC
---
- Allocation rate
- Heap populate
- Mutation rate
- Object life span

## Memory leakage
#### Solution
1. set object = null
2. Close unclosed resources such as `stream`. e.g. `finally`
3. avoid string concat and use string builder
4. avoid static collection holding objects
```java
public static List<Double> list = new ArrayList<>();
```
5. Overwrite `hashCode` and `equal`\
	- without `hashcode`, `Person("jon")` is duplicated in `hashMap`
```java
public void givenMap_whenEqualsAndHashCodeNotOverridden_thenMemoryLeak() { 
	Map<Person, Integer> map = new HashMap<>(); 
	for(int i=0; i<100; i++) { 
		map.put(new Person("jon"), 1); 
	} 
	Assert.assertFalse(map.size() == 1); 
}```

# Question & Answers
---
#### After the deletion of dead objects, live objects get reorganized in the memory to not leave any gaps in between them. What type of sweeping is described here?
- Sweep and compacting (Mark sweep)

#### When is object eligible for garbage collection
- When an object no longer has a direct or indirect relation to the stack, it's eligible for garbage collection.