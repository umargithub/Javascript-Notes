---
title: 'Hoisting'
date: 2021-01-10T14:38:05+05:30
draft: false
---

## What is Hoisting

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.

Inevitably, this means that no matter where functions and variables are declared, they are moved to the top of their scope regardless of whether their scope is global or local.

**Example 1 - Variables declared with var are moved to top**

```javascript
console.log(animal);
var animal = "Rabbit"

// Returns undefined
```

If we comment variable animal of the above code, then it will return error

```javascript
console.log(animal);
// var animal = "Rabbit"

// Returns Uncaught ReferenceError: animal is not defined
```
We can imagine the code to be like

```javascript
var animals; //JS interpreter will run this part first (Hositing)
console.log(animal); // undefined
animal = "Rabbit"; // Here interpreter wil assign the vaue

// Returns Uncaught ReferenceError: animal is not defined
```
## Hositing with Let and Const

They’re also hoisted — in fact, var, let, const, function and class declarations are hoisted — what we have to remember though is that the concept of hosting is not a literal process (ie, the declarations themselves do not move to the top of the file — it is simply a process of the JavaScript compiler reading them first in order to create space in memory for them).

### let

Variables defined with let and const are hoisted to the top of the block, but not initialized.

**For Example**

```javascript
console.log(hoist); // Output: ReferenceError: hoist is not defined ...
let hoist = 'The variable has been hoisted.';
```

> This ensures that we always declare our variables first.

However, we still have to be careful here. An implementation like the following will result in an ouput of undefined instead of a Reference error.

**For Example**

```javascript
let hoist;

console.log(hoist); // Output: undefined
hoist = 'Hoisted'
```

### const

With const, just as with let, the variable is hoisted to the top of the block.

**For Example**

```javascript
console.log(hoist); // Output: Uncaught ReferenceError: Cannot access 'hoist' before initialization
const hoist = 'The variable has been hoisted.';
```

Instances of var and let can be initialised without a value, while const will throw a Reference error if you try to declare one without assigning it a value at the same time.

```javascript
const myName; // Output: Uncaught SyntaxError: Missing initializer in const declaration
myName = 'Umar';
```

## Hoisting functions

JavaScript functions can be loosely classified as the following:

* Function declarations
* Function expressions

### Function declarations

These are of the following form and are hoisted completely to the top. Now, we can understand why JavaScript enable us to invoke a function seemingly before declaring it.

**For Example**

```javascript
hoisted(); // Output: "This function has been hoisted."

function hoisted() {
  console.log('This function has been hoisted.');
};
```

### Function expressions

Function expressions, however are not hoisted.

**For Example**

```javascript
expression(); //Output: "TypeError: expression is not a function

var expression = function() {
  console.log('Will this work?');
};

expression(); //Output: Uncaught ReferenceError: expression is not defined

let expression = function() {
  console.log('Will this work?');
};
```

