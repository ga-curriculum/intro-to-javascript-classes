# ![Intro to JavaScript Classes - Prototype Methods](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able utilize prototype methods in JavaScript classes.

## Prototype and static methods in classes

Two types of methods can be added to a class - [Prototype methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#methods) and [Static methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#static_methods_and_fields).

1. **Prototype methods** are available on an instance of the class (object) - this is why they are called `instance methods` in other OOP languages. `forEach` is an example of a prototype method:

```javascript
const nums = [1, 2, 3, 4, 5];
nums.forEach(num => console.log(num));
```

Prototype methods are common, but another less common type of method can be defined.

2. **Static methods** are called on the class itself and are not available on instances. These are typically used to implement behavior that doesn't pertain to a specific instance.

[Array.isArray](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray) is an example of a static method:

```js
const nums = [1, 2, 3, 4, 5];
console.log(Array.isArray(nums)); // true
```

## Defining prototype methods in a class

Let's add a prototype method called `start` to our `Car` class:

```javascript
class Car {
  // The constructor will always be called
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
    this.isRunning = false;
  }
  start() {
    this.isRunning = true;
    console.log('Running!');
  }
};
```

> 🧠 Class methods are not separated by a comma or any other character.

Notice the usage of the `this` keyword in our `start` method. It is being used outside of the constructor in this scenario.

In our `start` method, the `this` keyword refers to the current object instance. When defining methods in a class, we don't know the names of the future instances. Because we don't know the name of the object being created ahead of time, we cannot specify its name within the `start` method. Even if we knew the object's name, it wouldn't be very useful because our `start` method would only work with that single object! `this` allows the method to function correctly in the context of a specific object instance.

If we define an object directly, we can reference the object by its name within its methods:

```javascript
const hybridCar = {
  isRunning: false,
  start: function() {
    // Referencing the object by its name:
    hybridCar.isRunning = true;
    console.log('Running!');
  },
};
```

Here, we use `hybridCar.isRunning` because we're certain of the object's name. However, in class based instances, the object's name isn't predetermined, so we use `this` to dynamically reference whichever instance is calling the method. `this` will always point to the current object.

#### 🎓 You Do

Add another instance method.

1. Define a `stop` method in the `Car` class.

2. The `stop` method should set the `isRunning` property to `false` and log `"Stopped!"` to the console.

### Overriding methods

Thanks to another OOP principle called [inheritance](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)), **subclasses** inherit methods from their parent classes.

JavaScript implements inheritance differently from traditional OOP languages like Java or Python, in that JavaScript's implementation is prototype-based.

We won't go into prototypes during this lesson because, thanks to the new class syntax we're currently learning about, knowing about prototypes isn't as important anymore.

In JavaScript, the `Object` class is at the top of the class hierarchy, and thus nearly all objects inherit its methods, such as [toString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString):

```js
console.log(mySubaru.toString()) // something like: [object Object]
```

However, it's possible to override inherited methods by redefining that method.

For example, we can override/replace `Object`'s implementation of `toString` by defining it in the `Car` class:

```js
class Car {
  // the constructor will always be called
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
    this.isRunning = false;
  }
  start() {
    this.isRunning = true;
    console.log('Running!');
  }
  toString() {
    return `This car is a ${this.color} ${this.make} ${this.model}.`;
  }
};
```

Now when we call the `toString()` method on `mySubaru`, we should see the defined output:

```js
console.log(mySubaru.toString()); // "This car is a blue Subaru Crosstrek"
```

So far, you've learned how to define a class that creates objects with properties and add prototype methods. This represents about 80% of what there is to know about classes - congrats! Sounds like a great time for you to try your hand at this!

## 🎓 You Do

Define another class.

1. Pick something like our car example above that would make sense to instantiate. You can pick anything you'd like, but we'll use `Airplane` as an example. Remember that the class name should be uppercase and singular.
2. Code the class' `constructor` method so that it creates at least two properties.
3. Add at least two methods to the class. At least one of the methods you write should interact with one or multiple of the properties you created above. As you write your methods you might think of more properties you could add to the constructor - if you do, add them!
4. Create a couple of new instances of the class you've built.