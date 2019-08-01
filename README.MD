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

> Note: It's easy to remember the argument rule like so; Apply starts with an 'a' and so does array. Call starts with a 'c' and so does commas ;)

