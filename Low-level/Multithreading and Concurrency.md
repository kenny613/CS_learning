# Algorithms
---
## Peterson 

# Deadlock 
```java
public class Main {
    public static void main(String[] args) {

        Object obj1 = new Object();
        Object obj2 = new Object();

        Thread a = new Thread(() - > { // Runnable.run()
            String threadName = Thread.currentThread().getName();
            synchronized(obj1) {
                System.out.println(threadName + ": 取得 obj1 的鎖");
                try {
                    Thread.sleep(1000);
                } catch (Exception e) {
                    e.printStackTrace();
                }
                System.out.println(threadName + ": 等待 obj2 的鎖");
                synchronized(obj2) {
                    System.out.println(threadName + ": 取得 obj2 的鎖");
                }
            }
        }, "thread-a");

        Thread b = new Thread(() - > { // Runnable.run()
            String threadName = Thread.currentThread().getName();
            synchronized(obj2) {
                System.out.println(threadName + ": 取得 obj2 的鎖");
                try {
                    Thread.sleep(1000);
                } catch (Exception e) {
                    e.printStackTrace();
                }
                System.out.println(threadName + ": 等待 obj1 的鎖");
                synchronized(obj1) { 
                    System.out.println(threadName + ": 取得 obj1 的鎖");
                }
            }
        }, "thread-b");

        a.start();
        b.start();
    }
}
```
#### How to detect deadlock?
- thread dump in java
```cmd
jps // get PID
jcmd $PID Thread.print
```
-  jcmd $PID Thread.print
#### How to prevent deadlock?
- Avoid nested lock, rewrite as:
```java
synchronized(obj2) {
	System.out.println(threadName + ": 取得 obj2 的鎖");
	try {
		Thread.sleep(1000);
	} catch (Exception e) {
		e.printStackTrace();
	}
	System.out.println(threadName + ": 等待 obj1 的鎖");
	synchronized(obj1) { 
		System.out.println(threadName + ": 取得 obj1 的鎖");
	}
}
```

- Thread join with maximum time 