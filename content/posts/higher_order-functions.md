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