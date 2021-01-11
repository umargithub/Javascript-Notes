---
title: 'Array Callback Methods'
date: 2021-01-12T02:33:05+05:30
draft: false
---

Arrays come with many built-in methods that accepts callback functions.

* [forEach](#foreach)
* [map](#map)
* filter
* find
* reduce
* some
* every 

## forEach

* Accepts a callback function.
* Calls the function once per element in the array.

> forEach doesn't mutate the array.

**Example 1**

```javascript
const nums = [9, 8, 7, 6, 5, 4, 3, 2, 1];

nums.forEach(function(n){
  console.log(n * n);
  // prints 81, 64, 49, 36, 25, 16, 9, 4, 1
})
```

**Example 2**

```javascript
const nums = [9, 8, 7, 6, 5, 4, 3, 2, 1];

nums.forEach(function(el){
  if(el % 2 === 0) {
    console.log(el);
    // prints 8, 6, 4, 2
  }
})
```

**Example 3**

```javascript
const nums = [9, 8, 7, 6, 5, 4, 3, 2, 1];

function printTriple(n) {
	console.log(n * 3);
	// prints 27, 24, 21, 18, 15, 12, 9, 6, 3
}

nums.forEach(printTriple)
```

**Example - 4**

```javascript
const books = [
  {
    title: 'Good Omens',
    authors: ['Terry Pratchett', 'Neil Gaiman'],
    rating: 4.25
  },
  {
    title: 'Bone: The Complete Edition',
    authors: ['Jeff Smith'],
    rating: 4.42
  },
  {
    title: 'America Gods',
    authors: ['Neil Goiman'],
    rating: 4.41
  },
  {
    title: 'A Gentleman in Moscow',
    authors: ['Amor Towels'],
    rating: 4.36
  }
]

books.forEach(function(book){
  console.log(book.title);
  // prints 
  // Good Omens
  // Bone: The Complete Edition
  // America Gods
  // A Gentleman in Moscow
})

// Alternative way to do

// Using for of Loop

for(let book of books) {
  console.log(book.title)
}

// Using for Loop

for(let i = 0; i < books.length; i++) {
  console.log(books[i].title);
}

```

**We can also access index using forEach method**

**Example 5**

```javascript
const nums = [9, 8, 7, 6, 5, 4, 3, 2, 1];

nums.forEach(function(num, idx){
  console.log(idx, num);
})

// Prints
// 0 9
// 1 8
// 2 7
// 3 6
// 4 5
// 5 4
// 6 3
// 7 2
// 8 1
```

## map

Map is used to create a new array from an existing array.

**Example 1**

```javascript
const texts = ['rofl', 'lol', 'omg', 'ttyl'];
const caps  = texts.map(function(text){
  return text.toUpperCase();
})
texts; // [ 'rofl', 'lol', 'omg', 'ttyl' ]
caps; // [ 'ROFL', 'LOL', 'OMG', 'TTYL' ]
```

**Example 2**

```javascript
const numbers = [20, 21, 22, 23, 24, 25, 26, 27];

const doubles = numbers.map(function(num){
	return num * 2;
})

numbers; // 20, 21, 22, 23, 24, 25, 26, 27
doubles; // 40, 42, 44, 46, 48, 50, 52, 54
```
**Example 3**

```javascript
const numbers = [20, 21, 22, 23, 24, 25, 26, 27];

const map = numbers.map(function(num){
  return {
    num: num,
    isEven: num % 2 === 0
  }
})

map;

// returns
// [
//   { num: 20, isEven: true },
//   { num: 21, isEven: false },
//   { num: 22, isEven: true },
//   { num: 23, isEven: false },
//   { num: 24, isEven: true },
//   { num: 25, isEven: false },
//   { num: 26, isEven: true },
//   { num: 27, isEven: false }
// ]
```

**Example 4**

```javascript
const words = ['asap', 'byob', 'rsvp', 'diy'];

const abbrevs = words.map(function(word){
  return word.toUpperCase().split('').join('.');
})

abbrevs // [ 'A.S.A.P', 'B.Y.O.B', 'R.S.V.P', 'D.I.Y' ]
```

**Example 5**

```javascript
const books = [
  {
    title: 'Good Omens',
    authors: ['Terry Pratchett', 'Neil Gaiman'],
    rating: 4.25
  },
  {
    title: 'Bone: The Complete Edition',
    authors: ['Jeff Smith'],
    rating: 4.42
  },
  {
    title: 'America Gods',
    authors: ['Neil Goiman'],
    rating: 4.41
  },
  {
    title: 'A Gentleman in Moscow',
    authors: ['Amor Towels'],
    rating: 4.36
  }
]

const bookTitle = books.map(function(book){
  return book.title;
})

bookTitle;

// Returns ['Good Omens', 'Bone: The Complete Edition', 'America Gods', 'A Gentleman in Moscow']
```

> Map doesn't mutate the array.