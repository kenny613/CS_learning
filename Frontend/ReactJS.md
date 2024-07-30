## Hooks
---
## What are Hooks?
- Managing `state` by `useState`

## `UseRef`
- Wont trigger re-render
- Very useful as `HTNL selector`, we dont want DOM get reredner

## LifeCycle
---
1. The **Mounting Phase** begins when a component is created and inserted into the DOM. 
2. The **Updating Phase** occurs when a component's state or props change. 
3. The **Unmounting Phase** occurs when React removes it from the DOM.
![[Pasted image 20240730225055.png|500]]
1. 橘色框框的內容為 `componentDidMount` ，會在 `render` 後執行。
2. 綠色框框的內容為 `componentWillUnmount` ，會在 `components` 移除時執行。
3. 紅色框框的內容為 `componentDidUpdate` ，會在 `State` 改變時執行，執行順序為綠色框框到橘色框框。

## Effect LifeCycle
---
```javascript
function ChatRoom({ roomId /* "general" */ }) {  
	// Run every refresh of state OR pops
	useEffect(() => {  
		const connection = createConnection(serverUrl, roomId); // Connects to the "general" room  
		connection.connect();  
		return () => {  connection.disconnect(); } // Disconnects from the "general" room  
	};
	// Run once
	useEffect(()=>{  
		console.log(`只執行第一次`)  
	},[])
```
- Resynchronized after new pops, e.g. from `general` to `travel`
- How? 
	- Every time after your component re-renders, React will look at the **array of dependencies** that you have passed. 
	- If any of the values in the array is different from the value at the same spot that you passed during the previous render, React will re-synchronize your Effect

# Interview Q&A
--- 
#### What is virtual DOM?
