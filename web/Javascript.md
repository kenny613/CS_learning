---
aliases:
---
---
https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9

# Interview Q&A
#### 

#### How does closure works?
In the following code, `inner` forms a closure with the lexical environment of the execution context created when `foo` is invoked, _closing over_ variable `secret`:
```javascript
function foo() {
  const secret = Math.trunc(Math.random() * 100)
  return function inner() {
    console.log(`The secret number is ${secret}.`)
  }
}
const f = foo() // `secret` is not directly accessible from outside `foo`
f() // The only way to retrieve `secret` is to invoke `f`
```

#### What is hoisting and `var`??
- `var x` declaration will always move to top
- `var`is in `function scope` not
- `let` allos closure scope
```javascript
var funcs = [];


function a(){
	var i;
	{
		console.log("i =", i);
		i=0;
		funcs[i] = function() {
			console.log("My value:", i);
		}
	}
	
	{
		i = 1;
		funcs[i] = function() {
		console.log("My value:", i);
		}
	}
	
	{
		i = 2;
		funcs[i] = function() {
		console.log("My value:", i);
		}
	}
	
	for (var j = 0; j < 3; j++) {
	  // and now let's run each one to see
	  funcs[j]();
	}
}


console.log(i);
a()
/* Output: 
My value: 3
My value: 3
My value: 3
*/
```
- The value `i` in `console.log("My value:", i);` 
- has **function scope** and is determined `funcs` is executed
- `var i` is hoisted to function level, so it will be `2`
##### How to solve it?
1. Use one more layer of closure, create new `lexical environment`
2. Use `let` or `const`
#### Using the `$` in the jQuery Library
One of the most well-known uses of the dollar sign in JavaScript is with the jQuery library.
In jQuery, the dollar sign is used as a shorthand alias for the `jQuery` object. jQuery is a powerful JavaScript library that simplifies DOM manipulation and provides a wide range of utility functions for web development.

#### What is a `promise`?
-  ==eventual completion or failure of an asynchronous operation==
A JavaScript Promise object can be:
- Pending
- Fulfilled
- Rejected

The Promise object supports two properties: **state** and **result**.
While a Promise object is "pending" (working), the result is undefined.
When a Promise object is "fulfilled", the result is a value.
When a Promise object is "rejected", the result is an error object.
- `new Promise(function(myResolve, myReject)` receive two callback to perform when resolved or rejected
- `.then()` accept a callback when `Promise` is full filled
- 
## True OR False
---

✅ JavaScript, variables can be used without declawing in 'use strict mode'

❌JavaScript implements inheritance by using [objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#objects). Each object has an internal link to another object called its _prototype_.

✅ In JavaScript, inheritance takes place by cloning the prototype of an object.

✅In JavaScript $a, x, Y, Z, With are valid variable names.

✅ var lang="Javascript"//line 1 lang="javascript"//line 2 Line 2 has a global variable whereas line 1 has a local variable.

✅ Javascript is OOP

❌ With Object.seal(), you can add new properties to objects, but you cannot delete its existing properties.
- sealed object has a fixed set of properties: new properties cannot be added, existing properties cannot be removed, their enumerability and configurability cannot be changed, and its prototype cannot be re-assigned



#### circle
---
1,3, 5
$("button").click(function(){ $("div").animate(
  {height: '200px', width: '200px', borderRadius: '50%'}); });
  
$.noConflict();
jQuery(document).ready(function($){
$("button").click(function(){
$("div").animate({height: '200px', width: '200px', borderRadius:'50%'});
});
});

## change=$.noConflict();
change(document).ready(function($){
$("button").click(function(){
change("div").animate({height: '200px', width: '200px', borderRadius:'50%'});
});
});


## React
---
**When anything new is added to the application, a virtual DOM is created and it is represented as a tree**
 The virtual DOM (VDOM) is **a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM**.
 render() is the entry point to load into the UI