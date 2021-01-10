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

> We generally use anonymous function rather than using an existing function as callback. Anonymous functions are just unnamed function and one time use function.

**Example 2**

```javascript
function callTwice(func) {
	func();
	func();
}

callTwice(function () {
	console.log("Ha ha ha");
}) // Calling anonymous

// Result
// Ha ha ha 
// Ha ha ha
```

**Example 3**

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

## Why do we need Callbacks?

JavaScript is synchronous by default and is single threaded. This means that code cannot create new threads and run in parallel.

Lines of code are executed in series, one after another, for example:

```javascript
const a = 1
const b = 2
const c = a * b
console.log(c)
doSomething()
```

But JavaScript was born inside the browser, its main job, in the beginning, was to respond to user actions, like onClick, onMouseOver, onChange, onSubmit and so on. How could it do this with a synchronous programming model?

The answer was in its environment. The browser provides a way to do it by providing a set of APIs that can handle this kind of functionality.

**There are some cases that code runs (or must run) after something else happens and also not sequentially. This is called asynchronous programming.**

**Let us take an example**

```javascript
function first(){
  console.log(1);
}
function second(){
  console.log(2);
}
first();
second();

// Returns

// 1
// 2 
```

As you would expect, the function first is executed first, and the function second is executed second — logging the following to the console:

> But what if function first contains some sort of code that can’t be executed immediately? For example, an API request where we have to send the request then wait for a response? 

To simulate this action, were going to use setTimeout which is a JavaScript function that calls a function after a set amount of time. We’ll delay our function for 500 milliseconds to simulate an API request. Our new code will look like this:

**Example 4**

```javascript
function first(){
  // Simulate a code delay
  setTimeout( function(){
    console.log(1);
  }, 500 );
}
function second(){
  console.log(2);
}
first();
second();

// Returns
// 2
// 1
```

Even though we invoked the first() function first, we logged out the result of that function after the second() function.

It’s not that JavaScript didn’t execute our functions in the order we wanted it to, it’s instead that JavaScript didn’t wait for a response from first() before moving on to execute second()

**We can’t just call one function after another and hope they execute in the right order. Callbacks are a way to make sure certain code doesn’t execute until other code has already finished execution.**

So to make sure, first function runs before the second one, we can pass second function as callback

**Example 5**

```javascript
function first(callback){
  // Simulate a code delay
  setTimeout( function(){
    console.log(1);
    callback();
  }, 500 );
}

first(function (){
  console.log(2);
});

// Returns
// 1
// 2
```

**JavaScript is an event-driven programming language. We also use callback functions for event declarations. For example, let’s say we want users to click on a button:**

> You can’t know when a user is going to click a button, so what you do is, you define an event handler for the click event. This event handler accepts a function, which will be called when the event is triggered:

**Example 6**

```javascript
const btn = document.querySelector('button');
btn.addEventListener('click', function() {
	console.log("Button is clicked");
})
```

This is the so-called callback.

> To Conclude: A callback is a function that is to be executed after another function has finished executing — hence the name ‘call back’.