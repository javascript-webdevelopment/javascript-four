# Javascript Four

Todays lecture we will talk about Classes, Context, and some more depth of Arrow Functions.

## Context

Outside of Javascript, context means the surrounding information that gives a better understanding and more clarity to a situation. This also applies the same way to Javascript.

Since objects are the building blocks of Javascript, there is a special object we can use to access the context of our code that is being executed. The object is referred to as `this`.

### This

The value of `this` is decided upon how our code is being executed.

### Default Context

The default value of `this` refers to the global object. In a browser environment, `this` would be the `window` object.

```javascript
const myCar = 'Tesla';

function displayMyCar(){
    // reference the global object with `this`
    alert(this.myCar);
};

displayMyCar();
```

### Implicit Context

Implicit Context is where the value of `this` is the parent object of where the function exists. In the example above, the function exists in the global object, so the context of the `displayMyCar` function would be referring to the window object. However, the default value of the context will be implictely changed based on where the function exists. Meaning, if we have a function inside of an object, the default context for that function would be the object it lives in.

> It's easy to think that the value of `this` will be whatever is left of the `.`

```javascript
const newCar = {
    make: 'Tesla',
    model: 'Model X',
    year: 2019,
    showOff: function(){
        alert(`I drive a ${this.make}`);
    }
};

newCar.showOff();
```

Notice how `showOff` lives on the `newCar` object so the context of the showOff function will be newCar.

### Explicit Context

Explicit Context is where we explicitely tell a function what it's context is. We can do that by using the three different built in function methods `call`, `apply`, and `bing`.

#### Call

`.call()` is a built method that we can use on Function objects. This will allow us to pass in the object as an argument that we want the context of `this` to refer to. The following arguments will be additional values that we can use. These will need to be comma seperated.

```javascript
// people object with a method
const people = {
    sayName: function(car, year){
        alert(`My name is ${this.firstName} ${this.lastName} and I drive a ${car} made in ${year}`);
    };
};

// two new person objects
const personOne = {
    firstName: 'Tayte',
    lastName: 'Stokes'
};

const personTwo = {
    firstName: 'Matt',
    lastName: 'Bodily'
};

// call the people method sayName on two different objects
people.sayName.call(personeOne, 'tesla', 2020);
people.sayName.call(personTwo, 'masaratti', 2020);
```

#### Apply

`.apply()` works exactly like how call works, but the only difference is that apply only takes in two arguments so we will pass in new arguments as an array not comma seperated values.

```javascript
// people object with a method
const people = {
    sayName: function(car, year){
        alert(`My name is ${this.firstName} ${this.lastName} and I drive a ${car} made in ${year}`);
    };
};

// two new person objects
const personOne = {
    firstName: 'Tayte',
    lastName: 'Stokes'
};

const personTwo = {
    firstName: 'Matt',
    lastName: 'Bodily'
};

// apply the people method sayName on two different objects
people.sayName.apply(personeOne, 'tesla', 2020);
people.sayName.apply(personTwo, ['masaratti', 2020]);
```

> Note: It's easy to remember the argument rule like so; Apply starts with an 'a' and so does array. Call starts with a 'c' and so does comma ;)

#### Bind

`.bind()` works very similar to call except it defers the function invokation, meaning it will return an entirely new function.

```javascript
// sayName function
function(car, year){
    alert(`My name is ${this.firstName} ${this.lastName} and I drive a ${car} made in ${year}`);
};

// two new person objects
const personOne = {
    firstName: 'Tayte',
    lastName: 'Stokes',
};

const personTwo = {
    firstName: 'Matt',
    lastName: 'Bodily'
};

// create new functions using the sayName functionality and the object to bind it to
const personOneBrag = sayName.bind(personOne, 'Tesla', 2020);
const personTwoBrag = sayName.bind(personTwo, 'Mazaratti', 2020);

// now we need to manually invoke the newly bound functions
personOneBrag();
personTwoBrag();
```

## Classes

Classes are a newer syntax that we can use as a blueprint to create objects. 

We will use the `class` keyword to declare a new class. It's important to note that classes will start will capital letter.

```javascript
class Car {
    
}
```

We can create an `instance` or the object from this class by creating a variable and calling upon the class using the `new` keyword.

`new` is the keyword we use to invoke a class.

```javascript
class Car {
    
}

const myCar = new Car();

console.log(myCar) //result: this will be the new car object from the class invokation
```

### Constructor Function

We can have our class execpt arguments by using a `constructor` function. This function is where we will receive arguments and can then add them as a property to the object that class returns by using the `this`. 

```javascript
class Car {
    // define params to receive args in the class
    constructor(make, model, year){
        // then add them as props to the object that will be return
        this.make = make;
        this.model = model;
        this.year = year;
    }
}

const myCar = new Car('Tesla', 'Model X', 2020);
```

### ProtoType Functions

Prototype functions are functions that are built into a certain object type or class. We can create a prototype function on our class so that every object that is created from the class will have access to the function.

```javascript
class Car {
    constructor(make, model, year){
        this.make = make;
        this.model = model;
        this.year = year;
    }

    // prototypes go here, outside of the constructor
    // we should avoid using the function keyword and arrow functions
    honk(){
        alert(`Your ${this.make} honked!`);
    }
}

const myCar = new Car('Tesla', 'Model X', 2020);
```

### Extending Classes

We can have a class extend from another class to inherit the properties and protoypes from another class without having to re-write the logic.

We use the keyword `extends` to delcare our new class is extending another class.

```javascript
class Animal {
  constructor(name, type){
      this.name = name;
      this.type = type;
  }

  // prototype functions
  talk(saying){
    console.log(`${this.name} says: ${saying}`)
  }
}

// make another class that extends Animal
class Fish extends Animal {
  
};

const fishy = new Fish();
```

### Super

`super` is the keyword we can use when extending a class to invoke the construcor method from the class that is being extended. When we invoke `super` we will pass the arguments to the parent classes constructor method.

```javascript
class Animal {
  constructor(name, type){
      this.name = name;
      this.type = type;
  }

  talk(saying){
    console.log(`${this.name} says: ${saying}`)
  }
}

class Fish extends Animal {
    // constrcutor for the fish class to accept arguments
    constructor(name){
        // invoke super to call the parent classes constructor
        super(name, 'Fish');
    }
};

const fishy = new Fish('fishy');

// we can now use the talk prototype method from the Animal class on the fishy instance
fishy.talk('bubble bubble');
```

## Arrow Functions

Arrow functions are the newest way in Javascript to create a function.

```javascript
// This function:
function notArrowFunction(str) {
  return str
};

// is the same as this arrow function:
let arrowFunction1 = (str) => {
  return str
};

// which is also the same as this arrow function:
let arrowFunction2 = str => {
  return str
};

// which is also the same as this arrow function:
let arrowFunction3 = str => str;
```

Notice how we now use the `=>` rather than the `function` keyword. We also do not have to use parenthesis if we only are expecting a single argument. This is awesome because it allows for really short syntax that's easy to read.

Arrow function also work extremely well as a `callback` function.

```javascript
const myArray = [1,2,3,4,5];

// keep note of the anonymous arrow function being used as the callback
const evensArray = myArray.filter((element) => {
    return element % 2 === 0;
});
```