---
aliases:
---
---
https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9

## T OR F
---

✅ JavaScript, variables can be used without declawing in 'use strict mode'

❌JavaScript implements inheritance by using [objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#objects). Each object has an internal link to another object called its _prototype_.
- JavaScript implements inheritance by using [objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#objects). Each object has an internal link to another object called its _prototype_.
- 
✅ In JavaScript, inheritance takes place by cloning the prototype of an object.

✅In JavaScript $a, x, Y, Z, With are valid variable names.

✅ var lang="Javascript"//line 1 lang="javascript"//line 2 Line 2 has a global variable whereas line 1 has a local variable.

✅ Javascript is OOP

❌ With Object.seal(), you can add new properties to objects, but you cannot delete its existing properties.
- sealed object has a fixed set of properties: new properties cannot be added, existing properties cannot be removed, their enumerability and configurability cannot be changed, and its prototype cannot be re-assigned


## CSS
---
a[ref]

## HTLM5
---
#### When is DOMContentLoaded?
- The **`DOMContentLoaded`** event fires when the HTML document has been completely parsed, and all deferred scripts ([`<script defer src="…">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#defer) and [`<script type="module">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#module)) have downloaded and executed. It doesn't wait for other things like images, subframes, and async scripts to finish loading.
#### NEw HTML5 tags
https://www.tutorialspoint.com/html5/html5_new_tags.htm

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