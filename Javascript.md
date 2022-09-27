[**↺**BACK](./README.md)
# JavaScript Guideline


Below is a list of things that all JavaScript developers should know and try to adhere too.

  - [General](#general)
  - [Comparison Operators & Equality](#comparison-operators--equality)
  - [Functions](#functions)
  - [Arrow Functions](#arrow-functions)
  - [Iterators and Generators](#iterators-and-generators)
  - [Accessors](#accessors)
  - [Object Shorthand](#object-shorthand)
  - [Performance](#performance)
  - [Comments](#comments)
  - [Linting](#linting)
  - [Testing](#testing)
  - [References](#references)

## General
 - Use shorthand in place of constructors.  
  
 ***Avoid***
 ```js
 const items = new Array()
 // []
 const itemName = new String()
 // String {""}
 const item = new Object()
 // {}
 const createItem = new Function('data', 'return {id: data.ID, name: data.Label }')
 // ƒ anonymous(data) {
 // return {id: data.ID, name: data.Label }
 // }
 ```
 **Do**
 ```js
 const items = []
 // []
 const itemName = ''
 // ""
 const item = {}
 // {}
 const createItem = (data) => { 
   // do stuff
   return {
     id: data.ID,
     name: data.Label
   }
 }
// (data) => { 
//    // do stuff
//    return {
//      id: data.ID,
//      name: data.Label
//    }
//  }
 ```
>**Why** Because the result is not allways as aspected and shorthand is easyer to read and write.

## Comparison Operators & Equality
 - Use === and !== over == and !=. 
 - Conditional statements follow these simple rules:
   - Objects evaluate to true
   - Undefined evaluates to false
   - Null evaluates to false
   - Booleans evaluate to the value of the boolean
   - Numbers evaluate to false if +0, -0, or NaN, otherwise true
   - Strings evaluate to false if an empty string '', otherwise true
- Use explicit comparisons for strings and numbers.

***Avoid***
```js
if (isValid === true) {
  // ...
}
if (name) {
  // ...
}
if (collection.length) {
  // ...
}
```
 **Do**
 ```js
if (isValid) {
  // ...
}
if (name !== '') {
  // ...
}
if (collection.length > 0) {
  // ...
}
```
- Use simple ternarie expresions.

***Avoid***
```js
const foo = maybe1 > maybe2
  ? "bar"
  : value1 > value2 ? "baz" : null
```
**Do**
```js
// split into 2
const maybeNull = value1 > value2 ? 'baz' : null
const foo = maybe1 > maybe2 ? 'bar' : maybeNull
```
>**Why** To keep the code clean, easy to read and maintain.

## Functions
  - Use named function expressions instead of function declarations.
```js
const short = function longUniqueMoreDescriptiveLexicalFoo() {
  // ...
};
```
  - Use spread operator rest syntax instead of arguments.
```js
function concatenateAll(...args) {
  return args.join('')
}
```
  - Use default parameter syntax and put them last.
```js
function handleThings(opts = {}) {
  // ...
}
```

## Arrow Functions
 - Use arrow functions when you need them to be anonymous, like with [higher-order functions](#iterators).
 - Use the implicit return.
 ```js
 let a = [1, 2, 3]

 a.map((x) => x * x)

 a.map((x, idx) => ({
   id: idx,
   name: `Name ${x}`
 }))

 a.map((httpMethod) => (
   Object.prototype.hasOwnProperty.call(
     httpMagicObjectWithAVeryLongName,
     httpMethod,
   )
 ))
 ```
>**Why?** It shows clearly where the function starts and ends. 
 - Use parentheses around arguments.
 ```js
 let a = ['a', 'b', 'c']

 a.find((x) => x === 'a')

 a.map((x, idx) => ({
   index: idx,
   label: `The ${x}`
 }))
 ```
>**Why?** Minimizes difficulty when adding or removing arguments.

## Iterators and Generators
 - Use Array methods instead of loops like `for-in` or `for-of`.
    - <a name="iterators"></a>Array.map() / every() / filter() / find() / findIndex() / reduce() / some()
    - Object.keys() / values() / entries() to produce arrays
```js
let sum = 0;
numbers.forEach((num) => {
  sum += num
});

const sum = numbers.reduce((total, num) => total + num, 0)

const increasedByOne = numbers.map((num) => num + 1)
```
>**Why?** Dealing with pure functions that return values is easier to reason about than side effects.
 - *Don’t* use generators for now, `function* () {}`.
>**Why?** They don’t transpile well to ES5.

## Object Shorthand
- Use it for object method.
```js
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value
  },
}
```
- Use it for property value.
```js
const lukeSkywalker = 'Luke Skywalker'

const obj = {
  lukeSkywalker
}

const anakinSkywalker = 'Anakin Skywalker'

const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4,
}
```

## Comments
 - Use // for single line comments.

 **Avoid**
```js
const active = true  // is current tab

function getType() {
  console.log('fetching type...')
  // set the default type to 'no type'
  const type = this.type || 'no type'

  return type
}
```
**Do**
```js
// is current tab
const active = true

function getType() {
  console.log('fetching type...')

  // set the default type to 'no type'
  const type = this.type || 'no type'

  return type
}

function getType() {
  // set the default type to 'no type'
  const type = this.type || 'no type'

  return type
}
```

  
## Linting
Use `eslint` with default [standardJS](https://github.com/standard/standard/blob/master/RULES.md) minimum.

## Testing
Use `jest` for unit testing and if possible implement TDD.

## References
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript#airbnb-javascript-style-guide-)
- [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [MDN JavaScript guidelines](https://developer.mozilla.org/en-US/docs/MDN/Contribute/Guidelines/Code_guidelines/JavaScript)

[**⇪**TOP](#javascript-guideline)