---
title: 'Object Methods and the This Keyword'
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

// With shorthand properties

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

math.add(2, 4); // 6
```

## this keyword

this is a keyword. It is a reference to the current execution scope. It is going to give you an object back. 

> This is an object and it refers to the current execution scope

**The value of this inside a regular function refers to window object. Window is global scope in the browser. When we define a function using function declaration or expression, it is added like a property/method to window object.**

```javascript
function sayHi() {
  console.log("Hi");
  console.log(this);
}

sayHi(); // "HI"
window.sayHi(); // "Hi"
```

var is added to window object. let and const are not added to window object or global scope.

```javascript
var color = "teal";
window.color; // 'teal'

let color = "blue";
window.color; // it's not there
```

**this in Objects**

**Use the keyword this to access other properties on the same object**

```javascript
const person = {
  first: 'Cherilyn',
  last: 'Sarkisian',
  nickName: 'Cher',
  fullName(){
    console.log(this);
  }
}

person.fullName();

// returns

// {
//   first: 'Cherilyn',
//   last: 'Sarkisian',
//   nickName: 'Cher',
//   fullName: ƒ fullName()
// }

// Here the value of this is object itself.

const person = {
  first: 'Cherilyn',
  last: 'Sarkisian',
  nickName: 'Cher',
  fullName(){
    console.log(`${this.first} ${this.last} aka ${this.nickName}`);
  }
}

person.fullName(); // 'Cherilyn Sarkisian aka Cher'

// We can also use destructuring to make it clean.

const person = {
  first: 'Cherilyn',
  last: 'Sarkisian',
  nickName: 'Cher',
  fullName(){
    const {first, last, nickName} = this;
    console.log(`${first} ${last} aka ${nickName}`);
  }
}

person.fullName();

const person = {
  first: 'Cherilyn',
  last: 'Sarkisian',
  nickName: 'Cher',
  fullName(){
    const {first, last, nickName} = this;
    return `${first} ${last} aka ${nickName}`;
  }, 
  printBio(){
    const fullName = this.fullName();
    console.log(`${fullName} is a person.`)
  }
}

person.printBio(); // 'Cherilyn Sarkisian aka Cher is a person.'
```

## this invocation context

**The value of this depends on the invocation context of the function it is used in**

We have seen two different values for this so far. We saw that when we declared just a regular old function, this refers to the window object. When we use this inside of a method, it's a way of accessing the parent objects.

But that's not always the case. The value of this depends on the invocation context of the function that it is used in. What that means is the value will change depending on how the function is actually executed, not just where we write it.


But if we use this inside a method, it doesn't guarantee to reference the object. It depends on how we are calling.

```javascript
const person = {
  first: 'Cherilyn',
  last: 'Sarkisian',
  fullName(){
    const {first, last, nickName} = this;
    return `${first} ${last}`;
  }, 
}

person.fullName(); // This is what setting the value of this, the way that we are actually executing or invoking this function.

// Let's make a reference of the fullName function

const fullName = person.fullName;

// We are just pointing the variable to fullName to the function. It's (fullName function) a property on the person object.


const person = {
  first: 'Cherilyn',
  last: 'Sarkisian',
  fullName(){
    console.log(this)
    const {first, last, nickName} = this;
    return `${first} ${last}`;
  }, 
}

const fullName = person.fullName;
fullName(); // undefined undefined.

// this will return window object. This is because of the way we are executing the function.

// if we insted execute it the way we have been doing like below 

person.fullName(); // 'Cherilyn Sarkisian'

// Now this will return { first: 'Cherilyn', last: 'Sarkisian', fullName: ƒ fullName() }
```

## Key difference between arrow function amd regular function.

The value of this is not changed in the arrow function. this is reference to global scope to the window. That's why we don't use arrow function as methods. A lot of methods we write, we want to have access to the parent object or the containing object to do things like reference properties.

```javascript
const person = {
  first: 'Cherilyn',
  last: 'Sarkisian',
  fullName: () => {
    console.log(this)
    const {first, last, nickName} = this;
    return `${first} ${last}`;
  }, 
}

person.fullName(); // udefined undefined

// this will return window object.
```

But there is a reason that arrow functions don't get their own this, if you only use regular standard traditional functions (like fullName), sometime you can run into issues. Let see an example where that can happen.

```javascript
const annoyer = {
  phrases: ["literally", "cray cray", "I can't even", "Totes!", "YOLO", "Can't Stop", "Won't stop"],
  pickPhrase() {
    let index = Math.floor(Math.random() * this.phrases.length);
    return this.phrases[index];
  },
  start() {
    console.log(this.pickPhrase()) // Here Working
    setInterval(function(){
        console.log(this) // returns window object
        console.log(this.pickPhrase()) // this.pickPhrase is not a function
    }, 3000);
  }
}

const result = annoyer.start()
result; 
```

**Why is this before setInterval function set to object, but inside setInterval it's set to the window**

***Remember this changes depending on how it's called. We are executing start function ourselves as an object or as a method. But the anynomus function is not being executed by us insted by setInterval. Because the way this is called, it is set to window object just like if we had a regular function and if we don't execute a function as method on an object, this is set to be global scope to the window.***

**In the past, before arrow function were a thing, if we wanted to make this work or want to have a reference to the object in the setInterval function, we could create a variable and store the reference.**

```javascript
const annoyer = {
  phrases: ["literally", "cray cray", "I can't even", "Totes!", "YOLO", "Can't Stop", "Won't stop"],
  pickPhrase() {
    let index = Math.floor(Math.random() * this.phrases.length);
    return this.phrases[index];
  },
  start() {
    let that = this;
    setInterval(function(){
        console.log(that) // returns object
        console.log(that.pickPhrase()) // will generate a random phrase 
    }, 3000);
  }
}

const result = annoyer.start()
result  
```
**This is not ideal solution. We can do it by using arrow function, it's actually easier. if we insted use an arrow function there, we can avoid the problem entirely.**

**Remember that arrow function do not get their own this. The *this* in an arrow function does change from the *this* of it's parent or of nearest**

```javascript
const annoyer = {
  phrases: ["literally", "cray cray", "I can't even", "Totes!", "YOLO", "Can't Stop", "Won't stop"],
  pickPhrase() {
    let index = Math.floor(Math.random() * this.phrases.length);
    return this.phrases[index];
  },
  start() {
    setInterval(() => {
        console.log(this) // returns object
        console.log(this.pickPhrase()) // will generate a random phrase 
    }, 3000);
  }
}

const result = annoyer.start()
result   
```

> Sometime arrow function is a good choice becuase we don't want a new *this* but the other side of the coin is that they suck regular method on an object becuase you don't get access to *this* referencing the object, as they references the window. So arrow function is good in a situation like we have for setInterval function, because will use this from start function. But it's not good to if we had tried to write start function with arrow function instead of regular function. 

```javascript
const annoyer = {
  phrases: ["literally", "cray cray", "I can't even", "Totes!", "YOLO", "Can't Stop", "Won't stop"],
  pickPhrase() {
    let index = Math.floor(Math.random() * this.phrases.length);
    return this.phrases[index];
  },
  start() {
    this.timerId = setInterval(() => {
        console.log(this.pickPhrase())
    }, 3000);
  }, 
  stop() {
    clearInterval(this.timerId)
  }
}

annoyer.start();
annoyer.stop();
```