---
title: 'New JS Features'
date: 2021-01-16T21:18:05+05:30
draft: false
---

## Default Paramters in Function

**The old way**

```javascript

// The old way

function multiply(a, b) {
	b = typeof b !== 'undefined' ? b : 1;
	return a * b;
}

multiply(7); // 7
multiply(7, 3); // 21

// The new way

function multiply(a, b = 1) {
	return a * b;
}

multiply(7); // 7
multiply(7, 3); // 21

const greet = function (person, greet = "Hi") {
  console.log(`${greet} ${person}`)
}
greet("Umar");
greet("Umar", "Hello");
```

> The order of the argument matters in function

**For Example**

```javascript

// Here x will be assigned 7, and y will be default as there is no value used for y.

function multiply(x, y = 1) {
  return x * y;
}
multiply(7); // 7

// We can't make the first thing default and then have non default paramter for second/ afterwards argument.

function multiply(x = 1, y) {
  return x * y;
}

multiply(7) // NaN
```

## spread - (...)

Spread syntax allows an iterable such as an arrays to be expanded in places where zero or more arguments(for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.

### spread for function calls

Expand an iterable (array, string, etc.) into a list of arguments.

**Example**

```javascript
const nums = [9, 3, 2, 8];

Math.max(nums); // NaN

// Use spread

Math.max(...nums); // 9

// Same as calling
// Math.max(9, 3, 2, 8)

function printAllArguments(a, b, c, d) {
  console.log(a, b, c, d);
}

const colors = ['red', 'green', 'blue', 'orange']

printAllArguments(colors); // [ 'red', 'green', 'blue', 'orange' ] undefined undefined undefined

printAllArguments(...colors); // 'red' 'green' 'blue' 'orange'

let str = "CHANGE";

let str = "RAIN";

printAllArguments(...str); // 'R' 'A' 'I' 'N'
```

### spread for array literals

Creat a new array using an existing array. Spreads the elements from one array to a new array.

```javascript
const nums1 = [1, 2, 3];
const nums2 = [4, 5, 6];

const array1 = [ ...nums1, ...nums2];
array1; // [ 1, 2, 3, 4, 5, 6 ]

const array2 = ['a', 'b', ...nums1];
array2; // [ 'a', 'b', 1, 2, 3 ]

const array3 = [ ...nums1, ...nums2, 7, 8, 9];
array3; [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]

// spread can used to make a copy of an array.

const array3copy = [...array3]

array3copy; // [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]

// Note - It does not extend to nested arrays or we had objects inside of the array.

// spread can used to used to convert a string into an array.

let string = "abcdefg";

const array = [...string];

array; // [ 'a', 'b', 'c', 'd', 'e', 'f', 'g' ]

[...'abc', ...'def', 'Hello'];

// returns [ 'a', 'b', 'c', 'd', 'e', 'f', 'Hello' ]
```

### spread in Object Literals

Copies properties from one object to another object literal.

**Example**

```javascript
const feline = { legs: 4, family: 'Felidae' };
const canine = { family: 'Caninae', furry: true };

const dog = { ...canine, isPet: true }
dog // { family: 'Caninae', furry: true, isPet: true }

const lion = { ...feline, genus: 'Panthera' };
lion // { legs: 4, family: 'Felidae', genus: 'Panthera' }

const catDog = { ...feline, ...canine };
catDog // { legs: 4, family: 'Caninae', furry: true }

// In an object, if there are two properties with same key, they overide each other. The last property will override the previos property.

// We can also clone an object, but it just level deep like in the case of arrays.

const CatDogClone = { ...CatDog }; 

// { legs: 4, family: 'Caninae', furry: true }
```

> Note - We can only spread an object in another object.

```javascript
const feline = { legs: 4, family: 'Felidae' };
const canine = { family: 'Caninae', furry: true };

const test = [...dog] // TypeError: Object is not an iterable.
```

**We can spread an array in object literal**

```javascript
{ ...[1, 2, 3, 4, 5] } // {0: 1, 1: 2, 2: 3, 3: 4, 4: 5}
{ ...'abcdefg' } // {0: "a", 1: "b", 2: "c", 3: "d", 4: "e", 5: "f", 6: "g"}

// Note: We get key based of indicies.
```

**We can create array literals that also contain object literal, where we use spread in different context**

```javascript
const object = { a: 1 }

const random = [...'hello', {...object}]
random; //  'h', 'e', 'l', 'l', 'o', { a: 1 } ]

// Object can be spread in an object.
```
## Rest

It's look like spread, but it's not. It is used when we want to make function that accept an unlimited number of arguments or a variable number of arguments.

### The Argument Object (old)

* Available inside every function.
* It's an array like object
  * Has a length property.
  * Does not have array method like push/pop
* Contains all arguments passed to the function
* Not available inside of arrow functions

**Example 1**

```javascript
function sum() {
  let total = 0;
  for(let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

sum(1, 2, 3, 4)

// or 

function sum() {
  const argsArray = [...arguments];
  return argsArray.reduce((total, currentValue) => {
    return total + currentValue;
  })
}

sum(1, 2, 3, 4)
```

### rest params (new)

Collects all remaining arguments into an actual array.

**Example 1**

```javascript
function sum(...nums) {
  let total = 0;
  for(let num of nums) total += num
  return total
}

sum(1, 2, 3, 4, 5); // 15

// or

function sum(...nums) {
  return nums.reduce((total, currentValue) => total + currentValue)
}

sum(1, 2, 3, 4, 5)
```

**Example 2**

```javascript
function fullName(first, last, ...titles) {
  console.log('first', first)
  console.log('last', last)
  console.log('titles', titles)
}

fullName('tom', 'jones', 'III', 'order of phoenix')

// Collect remaing arguments which are not written. However argument object contained every argument including first and last. Rest is collecting the unclaimed arguments
```

**We can use rest in arrow function.**

```javascript
const sum = (...nums) => nums.reduce((total, currentValue) => total + currentValue)

sum(1, 2, 3, 4, 5, 10) // 25
```
