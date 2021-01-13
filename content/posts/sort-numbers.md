---
title: 'Sorting Numbers'
date: 2021-01-14T02:33:05+05:30
draft: false
---

```javascript
const prices = [400.50, 3000, 99.99, 35.99, 12.00, 9500];

prices.sort();

// [ 12, 3000, 35.99, 400.5, 9500, 99.99 ]
```

The default sort in Javascript does not work for numbers. All the numbers are converted to strings and and sorted as strings and that leads to incorrect order.

## Sorting for Numbers

```javascript 
arr.sort(compareFunc(a,b))
```

> sort mutates the array.

**If compareFunc(a, b) returns less than 0**

* Sort a before b

**If compareFunc(a, b) returns 0**

* Leave a and b unchanged with respect to each other

**If compareFunc(a, b) returns greater than 0**

* Sort b before a

**Example 1**

```Javascript
const prices = [400.50, 3000, 99.99, 35.99, 12.00, 9500];

// array.slice() makes a new copy of the array.

const ascSort = prices.slice().sort((a, b) => {
  return a - b
})

ascSort; // [ 12, 35.99, 99.99, 400.5, 3000, 9500 ]

const descSort = prices.slice().sort((a, b) => {
  return b - a
})

descSort; // [ 9500, 3000, 400.5, 99.99, 35.99, 12 ]
```

**Example 2**

```Javascript
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

const ascRating = books.sort((a, b) => {
  return a.rating - b.rating;
})

ascRating;

const descRating = books.sort((a, b) => {
  return b.rating - a.rating;
})

descRating;
```