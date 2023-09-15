# Objects

## Dot Notation

```javascript
let duck = {
  name: "Aflac",
  numLegs: 2
};
console.log(duck.name); // prints 'Alfac'
```

Dot notation is used on the object name, duck, followed by the name of the property, name, to access the value of Aflac.

## Methods inside object

Objects can have a special type of property, called a method.

Methods are properties that are functions. This adds different behavior to an object. Here is the duck example with a method:

```javascript
let duck = {
  name: "Aflac",
  numLegs: 2,
  sayName: function() {return "The name of this duck is " + duck.name + ".";}
};
duck.sayName();
```

The example adds the sayName method, which is a function that returns a sentence giving the name of the duck. Notice that the method accessed the name property in the return statement using duck.name. The next challenge will cover another way to do this.

## Constructors

Define a Constructor Function
Constructors are functions that create new objects. They define properties and behaviors that will belong to the new object. Think of them as a blueprint for the creation of new objects.

Here is an example of a constructor:

```javascript
function Bird() {
  this.name = "Albert";
  this.color = "blue";
  this.numLegs = 2;
}
```

This constructor defines a Bird object with properties name, color, and numLegs set to Albert, blue, and 2, respectively. Constructors follow a few conventions:

1. Constructors are defined with a capitalized name to distinguish them from other functions that are not constructors.
2. Constructors use the keyword this to set properties of the object they will create. Inside the constructor, this refers to the new object it will create.
3. Constructors define properties and behaviors instead of returning a value as other functions might.

## Create new objects using the 'new' keyword

```javascript
function Bird() {
  this.name = "Albert";
  this.color  = "blue";
  this.numLegs = 2;
}
let blueBird = new Bird();
```

Anytime a constructor function creates a new object, that object is said to be an instance of its constructor. JavaScript gives a convenient way to verify this with the instanceof operator. instanceof allows you to compare an object to a constructor, returning true or false based on whether or not that object was created with the constructor. Here's an example:

```javascript
let Bird = function(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}
let crow = new Bird("Alexis", "black");
let duck = new Bird("Donald","white")
crow instanceof Bird;       // true
```

## ownProperties

name, color and numLegs are called own properties, because they are defined directly on the instance object. That means that duck and crow each has its own separate copy of these properties
We can access this own properties in following way

```javascript
let ownProps = [];
for (let property in duck) {
  if(duck.hasOwnProperty(property)) {
    ownProps.push(property);
  }
}
console.log(ownProps) // [ name, color, numLegs ]
```

## prototypeProperties

Since numLegs will probably have the same value for all instances of Bird, you essentially have a duplicated variable numLegs inside each Bird instance.

A better way is to use the prototype of Bird. Properties in the prototype are shared among ALL instances of Bird
We can define a prototype property as follows:

```javascript
let Bird = function Bird(name, color) {
  this.name = name;
  this.color = color;
}

Bird.prototype.numLegs = 2; // defining prototype property and its value

let canary = new Bird("Millan","brown")

console.log(canary)         // { "Millan" , "brown" }
console.log(canary.numLegs) // access numLegs using dot annotation
```

It will be not visible if we display a object directly using the console.log(object)

but if we use the dot notation to access the property.

## Constructor property for object

constructor property is a reference to the constructor function that created the instance.

The advantage of the constructor property is that it's possible to check for this property to find out what kind of object it is

constructor property is a reference to the constructor function that created the instance

```javascript
function Dog(name,color) {
  this.name = name;
  this.color = color;
}
let inu = new Dog("akamaru","white");
console.log(inu.constructor)  // [Function: Dog]
```

## specifying multiple prototype properties using single object

we can specify different prototype properties in single object as follows:

```javascript
Bird.prototype = {
  numLegs: 2, 
  eat: function() {
    console.log("nom nom nom");
  },
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```

## constructor property inside prototype

When we assign prototype property using a object we override the constructor property of the created object

```javascript
function Dog(name,color) {
  this.name = name;
  this.color = color;
};

let inu0 = new Dog("Night","black"); // the constructor will be Dog as prototype properties are not yet set

Dog.prototype = {     // set the prototype properties using object
  numLegs : 4,
  breed : "Konoha inu"
};

let inu = new Dog("akamaru","white"); // create a object using new

console.log(inu.constructor === Dog, inu.constructor === Object , inu instanceof Dog); // false, true, true
console.log(inu0.constructor === Dog , inu0.constructor === Object , inu0 instanceof Dog); // true false false
```

We can fix this by using the constructor property inside the prototype object we are using to specify the properties

```javascript
function Dog(name,color) {
  this.name = name;
  this.color = color;
};

let inu0 = new Dog("Night","black"); 

Dog.prototype = {    
  constructor: Dog,     // specify the constructor
  numLegs : 4,
  breed : "Konoha inu"
};

let inu = new Dog("akamaru","white");

console.log(inu.constructor === Dog , inu.constructor === Object , inu instanceof Dog); // true, false, true
console.log(inu0.constructor === Dog , inu0.constructor === Object , inu0 instanceof Dog); // true false false
```

## isPrototypeOf()

Here the Bird constructor creates the duck object:

```javascript
function Bird(name) {
  this.name = name;
}

let duck = new Bird("Donald");
```

duck inherits its prototype from the Bird constructor function. You can show this relationship with the isPrototypeOf method:

```javascript
Bird.prototype.isPrototypeOf(duck); // true
```

## Prototype chaining

Because a prototype is an object, a prototype can have its own prototype. In this case, the prototype of Bird.prototype is Object.prototype:

```javascript
function Bird(name) {
  this.name = name;
}

console.log(typeof Bird.prototype);
Object.prototype.isPrototypeOf(Bird.prototype);
```

Chaining:

```javascript
let duck = new Bird("Donald");
duck.hasOwnProperty("name");

```

The hasOwnProperty method is defined in Object.prototype, which can be accessed by Bird.prototype, which can then be accessed by duck. This is an example of the prototype chain.

## Object inheriting the other prototype of other properties

We can inherit properties of one object to the other by using the prototype for that object.

```javascript
function Animal() { }
Animal.prototype = {    // create a prototype for animal
  constructor: Animal,
  eat: () => console.log("NOM NO< NO<")
}

function Dog() { }

Dog.prototype = Object.create(Animal.prototype);

let inu = new Dog();
inu.eat();
```

## Overriding the inherited methods

We can override the inherited method using defining it again

```javascript
function Animal() { }
Animal.prototype.eat = function() {
  return "nom nom nom";
};
function Bird() { }

Bird.prototype = Object.create(Animal.prototype);

Bird.prototype.eat = function() {
  return "peck peck peck";
};
```

## Make the constructor variables as private

```javascript
function Bird() {
  let hatchedEgg = 10;  // let prohibits the access to method and can only accessed using gerHatchedEggCount()

  this.getHatchedEggCount = function() { 
    return hatchedEgg;
  };
}
let ducky = new Bird();
ducky.getHatchedEggCount();
```

## Anonymous Function

A common pattern in JavaScript is to execute a function as soon as it is declared:

```javascript
(function () {
  console.log("Chirp, chirp!");
})(); // Chirp, chirp!
```

This is an anonymous function expression that executes right away, and outputs Chirp, chirp! immediately.

Note that the function has no name and is not stored in a variable. The two parentheses () at the end of the function expression cause it to be immediately executed or invoked. This pattern is known as an immediately invoked function expression or IIFE.
