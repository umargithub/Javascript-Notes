---
title: 'Destructiring'
date: 2021-01-17T05:26:05+05:30
draft: false
---

A short clean syntax to 'unpack':
* Values from arrays
* Properties from objects
Into  distinct variables.

## Array Destructuring

```javascript
const raceResults = ['Eluid Kipchoge', 'Feyisa Lelisa', 'Galen Rupp', 'Ghirmay Ghebreslassie', 'Alphonce Simbu', 'Jared Ward'];

const [gold, silver, bronze] = raceResults;

gold; // 'Eluid Kipchoge'
silver; // 'Feyisa Lelisa'
bronze; // 'Galen Rupp'

const [fastest, ...everyoneElse] = raceResults;
fastest; // 'Eluid Kipchoge'
everyoneElse; // [ 'Feyisa Lelisa', 'Galen Rupp', 'Ghirmay Ghebreslassie', 'Alphonce Simbu', 'Jared Ward' ]
```

We can skip element by using commas. Let's say I want the first and the fourth results, then we can do this

```javascript
const raceResults = ['Eluid Kipchoge', 'Feyisa Lelisa', 'Galen Rupp', 'Ghirmay Ghebreslassie', 'Alphonce Simbu', 'Jared Ward'];

const [first, , , fourth] = raceResults;

first; // 'Eluid Kipchoge'
fourth; // 'Ghirmay Ghebreslassie'

const [winner, , ...others] = raceResults; // skips second element

winner; // 'Eluid Kipchoge'
others; // ['Galen Rupp', 'Ghirmay Ghebreslassie', 'Alphonce Simbu', 'Jared Ward'];
```

## Object Destructuring

```javascript
const runner = {
  first: "Eluid",
  last: "Kipchoge",
  country: "Kenya",
  title: "Elder of the Order of the Golden Heart of Kenya"
}

const { first, last, country } = runner

first; // 'Eluid'
last; // 'Kipchoge'
country // 'Kenya'
```

Note: The variable name must be existing key names in the object, but we can give them new names.

```javascript
const runner = {
  first: "Eluid",
  last: "Kipchoge",
  country: "Kenya",
  title: "Elder of the Order of the Golden Heart of Kenya"
}

const { country: nation, title: honorific } = runner
nation; // 'Kenya'
honorific; // 'Elder of the Order of the Golden Heart of Kenya'

const { country: nation, title: honorific, ...others } = runner

nation; // 'Kenya'
honorific; // 'Elder of the Order of the Golden Heart of Kenya'
others; // { first: 'Eluid', last: 'Kipchoge' }
```

## Nested Destructuring

```javascript
const results = [{
    first: "Eluid",
    last: "Kipchoge",
    country: "Kenya"
  },
  {
    first: "Feyisa",
    last: "Lilesa",
    country: "Ethiopia"
  },
  {
    first: "Galen",
    last: "Rupp",
    country: "United States"
  }              
] 

const [, {country}] = results;
country; // 'Ethiopia'

const [{first: goldWinner}, {country}] = results;
goldWinner; // 'Eluid'
country; // 'Ethiopia'

// Better to break into single elements and then use destructuring for nested cases.

const [, silverMedal] = results;
const {country} = silverMedal;
country; // 'Ethiopia'
```

## Param Destructuring

```javascript
const fullName = ({first, last}) => {
  return `${first} ${last}`
}

const runner = {
  first: "Eluid",
  last: "Kipchoge",
  country: "Kenya"
}

fullName(runner); // 'Eluid Kipchoge'

const response = [
  'HTTP/1.1',
  '200 OK',
  'application/json'
]

function parseResponse([protocal, statusCode, contentType]) {
  console.log(`Status: ${statusCode}`);
}

parseResponse(response); // 'Status: 200 OK'
```

