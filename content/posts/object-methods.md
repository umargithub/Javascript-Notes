---
title: 'Object Methods and the 'This' Keyword'
date: 2021-01-18T01:30:05+05:30
draft: false
---

## Shorthand Properties

```javascript
const getStats = (arr) => {
  const max = Math.max(...arr);
  const min = Math.min(...arr);
  const sum = arr.reduce((total, currentValue) => total+ currentValue)
  const avg = sum/arr.length;
  return {
    max: max,
    min: min,
    sum: sum,
    avg: avg
  }
}

const reviews = [4.5, 5.0, 3.44, 2.8, 3.5, 4.0, 3.5];

const stats = getStats(reviews);
stats;

// Withshorthand properties

const getStats = (arr) => {
  const max = Math.max(...arr);
  const min = Math.min(...arr);
  const sum = arr.reduce((total, currentValue) => total+ currentValue)
  const avg = sum/arr.length;
  return {
    max,
    min,
    sum,
    avg
  }
}

const reviews = [4.5, 5.0, 3.44, 2.8, 3.5, 4.0, 3.5];

const stats = getStats(reviews);
stats;

const reviews = [4.5, 5.0, 3.44, 2.8, 3.5, 4.0, 3.5];
const max = Math.max(...reviews);
const min = Math.min(...reviews);
const sum = reviews.reduce((total, currentValue) => total+ currentValue)
const avg = sum/reviews.length;

const stats = {min, max, sum, avg}
stats; // { min: 2.8, max: 5, sum: 26.74, avg: 3.82 }
```

## Computed Properties

We can use a variable as a key name in an object literal property.

```javascript
const role = "host"; 
const person = "Jools Holland";
const role2 = "Director";
const person2 = "James Cameron";

const team = {};
team[role] = person // here variable is evaluated
team[role2] = person2;

team; // { host: 'Jools Holland', Director: 'James Cameron' }

const team = {
  [role]: person,
  [role2]: person2
}

team; // { host: 'Jools Holland', Director: 'James Cameron' }
```

```javascript
// This function adds a new propety to an object

function addProperty(obj, key, value) {
  obj[key] = value;
}

const person = {
  name: "Tim",
  age: 29,
}

addProperty(person, "country", "US");

person; // { name: 'Tim', age: 29, country: 'US' }

function addProperty(obj, key, value) {
  const copy = {...obj}
  copy[key] = value;
  return copy
}

const person = {
  name: "Tim",
  age: 29,
}

const results=  addProperty(person, "country", "US"); 
results // { name: 'Tim', age: 29, country: 'US' }

// But using computed properties

function addProperty(obj, key, value) {
  const copy = {...obj, [key]:value}
  return copy
}

const person = {
  name: "Tim",
  age: 29,
}

addProperty(person, "country", "US"); // { name: 'Tim', age: 29, country: 'US' }

// Using arrow function implicit return

const addProperty = (obj, key, value) => (
  {...obj, [key]:value }
)

const person = {
  name: "Tim",
  age: 29,
}

addProperty(person, "country", "US"); // { name: 'Tim', age: 29, country: 'US' }
```

## Methods

We can add functions as properties on objects. We call them methods.

```javascript
const math = {
  multiply: function(x, y) {
    return x * y;
  },
  divide: function(x, y) {
    return x / y;
  },
  square: function(x) {
    return x * x;
  }
};

math.multiply(3, 5); // 15
math.divide(20, 10); // 2
math.square(2); // 4
```

## Method Shorthand Syntax

```javascript
const math = {
  add(x, y) {
    return x + y;
  }, 
  multiply(x, y) {
    return x * y;
  }
}

math.add(2, 4); // 
```
