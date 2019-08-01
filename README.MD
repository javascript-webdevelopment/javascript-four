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
}

newCar.showOff();
```

Notice how `showOff` lives on the `newCar` object so the context of the showOff function will be newCar.

### Explicit Context