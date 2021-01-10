---
title: 'Hoisting'
date: 2021-01-10T22:38:05+05:30
draft: false
---

## What is Hoisting

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.

Inevitably, this means that no matter where functions and variables are declared, they are moved to the top of their scope regardless of whether their scope is global or local.

**For Example**

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

### But why undefined?

When JavaScript engine finds a var variable declaration during the compile phase, it will add that variable to the lexical environment and initialize it with undefined and later during the execution when it reaches the line where the actual assignment is done in the code, it will assign that value to the variable.

### So are let and const variables not hoisted?

All declarations (function, var, let, const and class) are hoisted in JavaScript, while the var declarations are initialized with undefined, but let and const declarations remain uninitialized.

They will only get initialized when their lexical binding (assignment) is evaluated during runtime by the JavaScript engine. This means you can’t access the variable before the engine evaluates its value at the place it was declared in the source code. This is what we call “Temporal Dead Zone”, A time span between variable creation and its initialization where they can’t be accessed.

### let

Variables defined with let and const are hoisted to the top of the block, but not initialized.

**For Example**

```javascript
console.log(hoist); // Output: ReferenceError: hoist is not defined ...
let hoist = 'The variable has been hoisted.';
```

> This ensures that we always declare our variables first.

If the JavaScript engine still can’t find the value of let or const variables at the line where they were declared, it will assign them the value of undefined or return an error (in case of const).

**For Example**

```javascript
let hoist;

console.log(hoist); // Output: undefined
hoist = 'Hoisted'
```

### const

With const, just as with let, the variable is hoisted to the top of the block but not initialized.

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

Only function declarations are hoisted in JavaScript, function expressions are not hoisted. For example: this code won’t work.

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

