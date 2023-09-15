# JavaScript ES6

## Difference between "let" and 'var'

The 'var' variables have function or global scope.
The let keyword behaves similarly, but with some extra features. When you declare a variable with the let keyword inside a block, statement, or expression, its scope is limited to that block, statement, or expression.

For example:

```javascript
var numArray = []; 
for (var i = 0; i < 3; i++) { // here 'i' is declared globally as we have declared it ad var 
  numArray.push(i);
}
console.log(numArray); // [0,1,2]
console.log(i);        // 3 // We should not able to access the 'i' inside the 'for' but as it is declared 'var' we can accesss it globally 
```

Now if we declare the 'i' as 'let' inside the for loop, we will get the output as '2' in above example, as the variables declared as 'let' will have block level scope if we tried to access them outside that scope it will give error.

## "const"

variables declared using const are read-only. They are a constant value, which means that once a variable is assigned with const, it cannot be reassigned.
However, it is important to understand that objects (including arrays and functions) assigned to a variable using const are still mutable. Using the const declaration only prevents reassignment of the variable identifier.

```javascript
const s = [5, 6, 7];
s = [1, 2, 3];
s[2] = 45;
console.log(s); // prints [ 5, 6, 45 ]
```

## Object.freeze()

'const' declaration alone doesn't really protect your data from mutation. To ensure your data doesn't change, JavaScript provides a function Object.freeze to prevent data mutation.

```javascript
let obj = {
  name:"FreeCodeCamp",
  review:"Awesome"
};
Object.freeze(obj);
obj.review = "bad";
obj.newProp = "Test";
console.log(obj); 
```

## Arrow Functions, Rest Parameters and Spread Operator

### Arrow Function

If function has multiple lines, we can use it as follows:

```javascript
const myFunc = () => {
  const myVar = "value";
  return myVar;
}
```

Or we can use it for in single line if it contain only a return value:

```javascript
const myFunc = () => "value";
```

If an arrow function has a single parameter, the parentheses enclosing the parameter may be omitted.

```javascript
const doubler = item => item * 2;
```

It is possible to pass more than one argument into an arrow function.

```javascript
const multiplier = (item, multi) => item * multi;
multiplier(4, 2);
```

In order to help us create more flexible functions, ES6 introduces default parameters for functions.

```javascript
const greeting = (name = "Anonymous") => "Hello " + name;
console.log(greeting("John")); // returns Hello John
console.log(greeting()); // returns Hello
```

### Rest Parameters

ES6 introduces the rest parameter ES6 introduces the rest parameter These arguments are stored in an array that can be accessed later from inside the function similar to java's varargs

```javascript
function howMany(...args) {
  return "You have passed " + args.length + " arguments.";
}
console.log(howMany(0, 1, 2)); // 3
console.log(howMany("string", null, [1, 2, 3], { })); //4
```

### Spread Operator

Math.max() expects comma-separated arguments, but not an array. The spread operator makes this syntax much better to read and maintain.

```javascript
const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr); //maximus would have a value of 89.
const newArr = [...arr]   // copies the arr elements to newArr
```

...arr spreads the array. However, the spread operator only works in-place, like in an argument to a function or in an array literal. The following code will not work:

```javascript
const spreaded = ...arr;
```

## Destrctring Assignment

```javascript
const user = { name: 'John Doe', age: 34 };
const name = user.name;
const age = user.age;
```

name would have a value of the string John Doe, and age would have the number 34.

Here's an equivalent assignment statement using the ES6 destructuring syntax:

```javascript
const { name, age } = user;
```

Again, name would have a value of the string John Doe, and age would have the number 34.

If we want to assign new name to the each variable while destrucuring we can use it as following:

```javascript
const { name:userName, age:userAge } = user;
```

Using an object similar to previous examples:

```javascript
const user = {
  johnDoe: { 
    age: 34,
    email: 'johnDoe@freeCodeCamp.com'
  }
};
```

Here's how to extract the values of object properties and assign them to variables with the same name:

```javascript
const { johnDoe: { age, email }} = user;
```

And here's how you can assign an object properties' values to variables with different names:

```javascript
const { johnDoe: { age: userAge, email: userEmail }} = user;
```

One key difference between the spread operator and array destructuring is that the spread operator unpacks all contents of an array into a comma-separated list. Consequently, you cannot pick or choose which elements you want to assign to variables.

Destructuring an array lets us do exactly that:

```javascript
const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b); // 1 2
const [c,d,,e,,f] = [1,2,3,4,5,6]; // Another Use
console.log(c,d,e,f) // 1 2 4 6
```

Destructuring using the Rest elements :

```javascript
const [a,b,...arr] = [1,2,3,4,5,6,7];
console.log(a,b); // 1 2
console.log(arr); // [3,4,5,6,7]
```

In some cases, you can destructure the object in a function argument itself.

Consider the code below:

```javascript
const profileUpdate = (profileData) => {
  const { name, age } = profileData;
  console.log(name,age) //  Jhon Doe 35
}
profileUpdate ({name:"Jhon Doe", age: 35});
```

This effectively destructures the object sent into the function. This can also be done in-place:

```javascript
const profileUpdate = ({ name, age}) => {
  console.log(name,age) // Jhon Doe 35
}
```

## Template Literals

```javascript
const person = {
  name: "Zodiac Hasbro",
  age: 56
};

const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting); // First Line of Output: 
```

The console will display the strings Hello, my name is Zodiac Hasbro! and I am 56 years old..

The example uses backticks (`), not quotes (' or "), to wrap the string. Secondly, notice that the string is multi-line, both in the code and the output. This saves inserting \n within strings. The ${variable} syntax used above is a placeholder. Basically, you won't have to use concatenation with the + operator anymore. To add variables to strings, you just drop the variable in a template string and wrap it with ${ and }. Similarly, you can include other expressions in your string literal, for example ${a + b}. This new way of creating strings gives you more flexibility to create robust strings.

Object Literals Declaration
Consider the following code:

```javascript
const getPerson = (name, age) => ({
  name: x,
  age: y
});

const getPersonUpdated = (name,age) => ({ name, age });
```

The above code eleminates the redunduncy to write 'name:name'.

### New Function Declaration

When defining functions within objects in ES5, we have to use the keyword function as follows:

```javascript
// ES5
const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};
// ES6 
const person = {
  name: "Taylor",
  sayHello() {    // No need of colon and literal function
    return `Hello! My name is ${this.name}.`;
  }
};
```

## The class keyword

ES6 provides a new syntax to create objects, using the class keyword.

class declaration has a constructor method that is invoked with the new keyword. If the constructor method is not explicitly defined, then it is implicitly defined with no arguments.

```javascript
class SpaceShuttle {
  constructor(targetPlanet) {   // Explicit constructor

    this.targetPlanet = targetPlanet;
  }
  takeOff() {
    console.log("To " + this.targetPlanet + "!");
  }
}

// Implicit constructor 
class Rocket {
  launch() {
    console.log("To the moon!");
  }
}

const zeus = new SpaceShuttle('Jupiter');
// prints To Jupiter! in console
zeus.takeOff();

const atlas = new Rocket();
// prints To the moon! in console
atlas.launch();
```

### Getter and Setter

Getter functions are meant to simply return value of an object's private variable
Setter functions are meant to modify (set) the value of an object's private variable

```javascript
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer() {
    return this._author;
  }
  // setter
  set writer(updatedAuthor) {
    this._author = updatedAuthor;
  }
}
const novel = new Book('anonymous');
console.log(novel.writer);  // anonymous
novel.writer = 'newAuthor';
console.log(novel.writer);  // newAuthor
```

## Module in JS

JavaScript started with a small role to play on an otherwise mostly HTML web. Today, it’s huge, and some websites are built almost entirely with JavaScript. In order to make JavaScript more modular, clean, and maintainable; ES6 introduced a way to easily share code among JavaScript files. This involves exporting parts of a file for use in one or more other files, and importing the parts you need, where you need them. In order to take advantage of this functionality, you need to create a script in your HTML document with a type of module. Here’s an example:

``` javascript
<script type="module" src="filename.js"></script>
```

### export the fnctions from js file

If you want to use a function in several different JavaScript files. In order to share it with these other files, you first need to export it.

```javascript
export const add = (x, y) => {
  return x + y;
}
// We can also do the same by following: 
const add = (x, y) => {
  return x + y;
}
export { add };
// For more than one functions to export:
export { add,subtract }
```

### import the fnctions from js file

To import the functions from other files we have to use following syntax:

```javascript
import { add, subtract } from './math_functions.js';
console.log(add(10,15));
```

To import all functions from the file as a module we can use:

```javascript
import * as myMathModule from "./math_functions.js";
console.log(myMathModule.add(10,15));
console.log(myMathModule.subtract(10,15));
```

## export default

We use this syntax if only one value is being exported from a file. It is also used to create a fallback value for a file or module

```javascript
export default function add(x, y) { // named default functon
  return x + y;
}

export default function(x, y) { // annonymous default function
  return x + y;
}
```

Since export default is used to declare a fallback value for a module or file, you can only have one value be a default export in each module or file.

### Importing default function

we can import the default function as:

```javascript
import subtract from './math_functions.js' 
```

here main difference is that we have to import the functions without using curly braces '{}'

## Promise in JS

Create a JavaScript Promise
A promise in JavaScript is exactly what it sounds like - you use it to make a promise to do something, usually asynchronously. When the task completes, you either fulfill your promise or fail to do so. Promise is a constructor function, so you need to use the new keyword to create one. It takes a function, as its argument, with two parameters - resolve and reject. These are methods used to determine the outcome of the promise. The syntax looks like this:

``` javascript
const myPromise = new Promise((resolve, reject) => {
  // implementation
});
```

Promise have three states - pending, fulfilled, and rejected
The resolve and reject parameters given to the promise argument are used to do this. resolve is used when you want your promise to succeed, and reject is used when you want it to fail

```javascript
const myPromise = new Promise((resolve, reject) => {
  if(condition here) {
    resolve("Promise was fulfilled");
  } else {
    reject("Promise was rejected");
  }
});
```

To hanndle a server request we may use promise as it can be asynchronous and so we can use promise in such case. Now if we want to do something after the promise is completed then we can do it using 'then'.
The then method is executed immediately after your promise is fulfilled with resolve

```javascript
myPromise.then(result => {
  // we can print the result here  
});
```

we can handle a rejected promise using the catch block

```javascript
myPromise.catch(error => {
  // print the things returned by reject method
});
```

## '==' vs '==='

The '==' and '===' operators check for equality (the triple === tests for strict equality, meaning both value and type are the same).

```javascript
let a = 5
let b = '5' 
console.log(a == b);  // true
console.log(a === b); // false
```

## Array Operations

### push() & unshift()

push adds the elements to the end of array and unshif adds the elements at the front of array

### pop() & shift()

pop removes and returns the last element in the array and shift() removes and returns first element in the array

```javascript
a = []
a.unshift("First",2); // a = [ First , 2 ]
a.push(3,"Last");       // a = [ 3 , Last ]
a.shift()               // [ 2, 3, 'Last' ]  
a.pop()                 // [ 2 , 3 ]
```

### splice()

splice() allows us to remove any number of consecutive elements from anywhere in an array.
splice(begin,no_elements_to_be_deleted)
splice(beginindex,no_elements_to_be_deleted, elements_to_be_added)

```javascript
let a = [1,2,3,4,5,6,7,8,9]
a.splice(3,2); // removes and returns 3,4 from array 
// a = [1,2,5,6,7,8,9]
a.splice(0,2,3,4) // 1,2 
is returned and removed and 3,4,5 is added
```

### slice()

slice() copies or extracts a given number of elements to a new array. slice() takes only 2 parameters — the first is the index at which to begin extraction, and the second is the index at which to stop extraction (extraction will occur up to, but not including the element at this index)

```javascript
a = [0,1,2,3,4,5,6]
a = a.slice(0,2); // a = [0,1]
```

### indexOf(element_to_be_checked)

indexOf(), that allows us to quickly and easily check for the presence of an element on an array. indexOf() takes an element as a parameter, and when called, it returns the position, or index, of that element, or -1 if the element does not exist on the array

```javascript
let fruits = ['apples', 'pears', 'oranges', 'peaches', 'pears'];
fruits.indexOf('dates');  // -1
fruits.indexOf('oranges');  // 2
```

## Objects and related terminologies

```javascript
const tekkenCharacter = {
  player: 'Hwoarang',
  fightingStyle: 'Tae Kwon Doe',
  human: true
};
```

The above code defines a Tekken video game character object called tekkenCharacter. It has three properties, each of which map to a specific value. If you want to add an additional property, such as "origin", it can be done by assigning origin to the object:

```javascript
tekkenCharacter.origin = 'South Korea';
```

This uses dot notation. If you were to observe the tekkenCharacter object, it will now include the origin property. Hwoarang also had distinct orange hair. You can add this property with bracket notation by doing:

```javascript
tekkenCharacter['hair color'] = 'dyed orange';
```

Bracket notation is required if your property has a space in it or if you want to use a variable to name the property

If we want to remove the 'player' key, we can remove it by using the delete keyword like this

```javascript
let obj = {
  'apple': 95,
  'custard-apple':26,
  'pineapple':85,
  'kiwi':100
}
delete obj.apple; // removes the apple in obj
```

### 'in' and 'has'

### Object.keys(obj)

Object.keys(obj) is used to get all the keys for the object passed in the method

```javascript
let obj = {
  'apple': 95,
  'custard-apple':26,
  'pineapple':85,
  'kiwi':100
}
console.log(Object.keys(obj));  // ['apple','custard-apple','pineapple','kiwi']
```

## Promise

A promise is a contract which has three states pending, resolve or reject. It is used in the context of the API calls where the data to be acquired is not yet been provided by the API.
Once the response from the API is returned then the promise is either rejected or resolved

```js
const buyFlightTicket = () => {
    return new Promise( (resolve, reject) => {
        setTimeout( () => {// wating for 3 seconds
            const error = false; // checking error
            if( error ) { 
                reject("Sorry your payment was not successful")
            } else {
                resolve("Thank you, your payment was successful");
            }
        }, 3000)
    })
}

buyFlightTicket()
.then( (success) => console.log(success)) // to run the code after successful completion of request
.catch( (error) => console.log(error) ); // If error then catch block is run
```
