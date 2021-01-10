---
title: 'Callback Functions'
date: 2021-01-10T14:38:05+05:30
draft: false
---

## What are Callback Functions

A callback functions is a function passed into another functions as an argument, which is then invoked inside the outer function.

**Example 1**

```javascript
function callTwice(func) {
	func();
	func();
}

function laugh() {
	console.log("Ha ha ha");
}

callTwice(laugh) // Laugh is callback function

// Result
// Ha ha ha 
// Ha ha ha
```

> We generally use anonymous function rather than using an existing function as callback. Anonymous functions are unnamed function and just one time use function.

**Example 2**

```javascript
function sayHello() {
	console.log("Hello");
}

setTimeout(sayHello, 5000); // says "Hello" after 5 seconds

// Calling it anonymous

setTimeout(function() {
	console.log("Hello");
}, 5000) // says "Hello" after 5 seconds
```