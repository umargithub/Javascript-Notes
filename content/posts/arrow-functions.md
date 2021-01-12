---
title: 'Arrow Functions'
date: 2021-01-13T00:50:05+05:30
draft: false
---

There’s another very simple and concise syntax for creating functions, that’s often better than Function Expressions.

**Example 1**

```javascript
const square = (x) => {
  return x * x;
}
square(9); // 81

// Using Function Expression

const square = function (x) {
  return x * x;
}
square(9); // 81

```

**Example 2**

```javascript
const sum = (x, y) => {
  return x + y;
}
sum(1, 4); // 5
```

**Example 3**

```javascript
const isEven = (num) => {
  return num % 2 === 0
}

isEven(2); // true
isEven(9); // false
```

> Parens are optional if there's only one parameter:

**Example 4**

```javascript
const square = x => {
  return x * x;
}
square(9); // 81
```

> Use empty parens for function with no paramters: 

**Example 5**

```javascript
const greet = () => {
  console.log("Hello");
}
greet(); // Hello
```

## Implicit Return 

If there is single expression to return, we can rewrite the arrow function using paranthesis insted of curly braces, andif we do that we need to remove return keyword. We can even make simple by removing the parens and making it one liner.

**Example 6**

```javascript
const square =  x => ( 
  x * x
)
square(3) // 9

const square = x => x * x;
square(4); // 16

const add = (x, y) => x +  y;
add(2, 3) // 5
```

All these functions do the same thing:

```javascript

// regular function expression

const isEven = function(num) {
	return num % 2 === 0;
}

// arrow function with parens around param

const isEven = (num) => {
	return num % 2 === 0;
}

// no parens around param

const isEven = num => {
	return num % 2 === 0;
}

// implicit return

const isEven = num => (
	num % 2 === 0;
);

// one-liner implicit retun

const isEven = num => num % 2 === 0;

```

**Example 5**

```javascript
const nums = [1, 2, 3, 4, 5, 6, 7, 8];

const doubles = nums.map(num => {
  return num * num
})

doubles; // [1, 4, 9, 16, 25, 36, 49, 64]

const nums = [1, 2, 3, 4, 5, 6, 7, 8];

const doubles = nums.map(num =>  num * num)

doubles // [1, 4, 9, 16, 25, 36, 49, 64]
```