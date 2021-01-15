---
title: 'Array Callback Methods'
date: 2021-01-12T02:33:05+05:30
draft: false
---

Arrays come with many built-in methods that accepts callback functions.

* [forEach](#foreach)
* [map](#map)
* [filter](#filter)
* [find](#find)
* [reduce](#reduce)
* [some](#some)
* [every](#every)

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

**Example 4**

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

> Map doesn't mutate the array.

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

**Example 6**

```javascript
const nums = [1, 2, 3, 4, 5, 6, 7, 8];

const parityList = nums.map(num => num % 2 === 0 ? 'Even' : 'Odd')

parityList; // [Odd, Even, Odd, Even, Odd, Even, Odd, Even]

// Other way

const parityList = nums.map(function(num){
	if(n %  2 === 0) return 'Even';
	return 'Odd';
})
```

## find

Returns the value of the first element in the array that satisfies the provided testing functions.

**Example 1**

```javascript
const movies = [
  "The Fantastic Mr. Fox",
  "Mr. and Mrs. Smith",
  "Mrs. Doubtfire",
  "Mr. Deeds"
]

let movie = movies.find(function(movie){
  return movie.includes("Mrs.");
})
movie // Mr. and Mrs. Smith

let movie2 = movies.find(movie => movie.indexOf('Mrs') === 0 )
movie2 // 'Mrs. Doubtfire'
```

**Example 2**

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

const book = books.find(book => book.rating >= 4.3 )
book;

const neilbook = books.find(book => book.authors.includes('Neil Gaiman'))

neilbook;
```

## filter

Creates a new array with all the elements that pass the test implemented by the provided function.

> Filter doesn't mutate the array.

**Example 1**

```javascript
const nums = [9, 8, 7, 6, 5, 4, 3, 2, 1];
const odds = nums.filter(num => num % 2 === 1)
odds; // [ 9, 7, 5, 3, 1 ]
```

**Example 2**

```javascript
const nums = [9, 8, 7, 6, 5, 4, 3, 2, 1];
const smallNums = nums.filter(num => num < 5)
smallNums // [ 4, 3, 2, 1 ]
```

**Example 3**

```javascript
const books = [
  {
    title: 'Good Omens',
    authors: ['Terry Pratchett', 'Neil Gaiman'],
    rating: 4.25,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'Changing My Mind',
    authors: ['Zadie Smith'],
    rating: 3.83,
    genres: ['nonfiction', 'essays']
  },
  {
    title: 'Bone: The Complete Edition',
    authors: ['Jeff Smith'],
    rating: 4.42,
    genres: ['fiction', 'graphic novel', 'fantasy']
  },
  {
    title: 'America Gods',
    authors: ['Neil Goiman'],
    rating: 4.11,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'A Gentleman in Moscow',
    authors: ['Amor Towels'],
    rating: 4.36,
    genres: ['fiction', 'historical fiction']
  },
  {
    title: 'The Name of the Wind',
    authors: ['Patrick Rothfuss'],
    rating: 4.54,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'The OverStory',
    authors: ['Richard Powers'],
    rating: 4.19,
    genres: ['fiction', 'short stories']
  },
  {
    title: 'The Way of Kings',
    authors: ['Brandon Sanderson'],
    rating: 4.65,
    genres: ['fantasy', 'epic']
  },
  {
    title: 'Lord of the files',
    authors: ['Wiliam Golding'],
    rating: 3.67,
    genres: ['fiction']
  }
]

const goodBooks = books.filter(book => book.rating >= 4.3 )
goodBooks;

const fantasyBooks = books.filter(book => book.genres.includes('fantasy'))
fantasyBooks

const shortStories = books.filter(book => book.genres.includes('short stories') || book.genres.includes('essays'))
shortStories

let query = 'The';
const results = books.filter(book => {
  return book.title.toLowerCase().includes(query.toLowerCase())
})
results

// or

let query = 'The';
const results = books.filter(book => {
  let title = book.title.toLowerCase();
  return title.includes(query.toLowerCase())
})
results
```

## every

Tests whether all elements in the array pass the provided function. It returns a boolean value.

**Example**

```javascript
const words = ['dog', 'dig', 'log', 'bag', 'wag'];

words.every(word => {
  return word.length === 3;
}) 

// returns true

const allEndInG = words.every(word => word[0] === 'd'); //false

words.every(word => {
  return word[word.length-1] === 'g';
})

// returns true

const check = books.every(book => {
  return book.rating > 3.5
})

//returns true
```

## some

Similar to every, but returns true if ANY of the array elements pass the test function.

**Example**

```javascript
const words = ['dog', 'jello', 'log', 'cupcake', 'bag', 'wag'];

// Are there any words longer than 4 characters?

const check = words.some(word => {
  return word.length > 4;
})

check // true

// Do any words starts with 'Z'?

const check = words.some(word => {
  return word[0] === 'z'
})

check // false

// Do any words contain cake

const check = words.some(word => {
  return word.includes('cake')
})

check // true

const check = books.some(book => {
  return book.authors.length === 2
})

//returns true
```

## reduce

It takes an array of values and it reduces them down to a single value.

**Example**

```javascript
const nums = [3, 5, 7., 9, 11];

const total = nums.reduce((accumulator, currentValue) => {
  return accumulator + currentValue;
})

total; // 35
```

| Callback    | accumulator | currentValue | returnValue |
| first call  |       3     |       5      |       8     |
| second call |       8     |       7      |      15     |
| third call  |      15     |       9      |      24     |
| fourth call |      24     |      11      |      35     |