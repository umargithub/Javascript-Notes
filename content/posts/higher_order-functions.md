---
title: 'Higher Order Functions'
date: 2021-01-10T14:38:05+05:30
draft: false
---

## What is Higher Order Functions

Functions that operate on/with other functions. They can:

- Accept other functions as arguments
- Returns a function

### Functions as Arguments

#### Example 1

```javascript
function callTwice(func) {
	func();
	func();
}

function laugh() {
	console.log("Ha ha ha");
}

callTwice(laugh) // passing a function as an argument

// Result
// Ha ha ha 
// Ha ha ha
```
#### Example 2

```javascript
function callNTimes(func, num) {
	for(let i = 0; i < num; i++) {
		func();
	}
}

function laugh() {
	console.log("Ha ha ha");
}

callNTimes(laugh, 3) // passing a function as an argument

// Result
// Ha ha ha 
// Ha ha ha
// Ha ha ha
```

#### Example 3

```javascript
function pickOne(f1, f2) {
   Math.random() > 0.5 ? f1() : f2()
}

function f1() {
  console.log("I am First Function");
}
  
function f2() {
  console.log("I am Second Function");
}

pickOne(f1, f2) 

// Result 
//Pick a Random Function
```