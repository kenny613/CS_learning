---

---
---
- Ensure only ONE instance is presence
```java
class DataBaseConnection{
	// static acts like class variable, shared within instance
	// volatile is allos immeditae visibility between thread, volatile doe not preseirve atomicity
	private static volatile DataBaseConnection instance;
	private String databaseURL;

	private DatabaseConnection(String databaseURL) {
		if(instance != null)
			throw new IllegalStateException("Instance already created")
		this.databaseURL = databaseURL;
	}


	public DataBaseConnection getInstance(){
		if(instance == null){
			// make DataBaseConnection.class synchornized for instance to prevent race confition of multi-threads
			synchronized(DataBaseConnection.class){
				if(instance == null){
					instance = new DataBaseConnection("jdbc:q://...");
				}
			}
		}
		return instance;
	
		
	}

}
```