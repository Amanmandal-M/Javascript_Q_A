<h1 align="center">JavaScript Questions with answers</h1>

<br>

##  What is Prototypical Inheritance ?

<br>

Prototypical inheritance is a form of object inheritance in JavaScript that relies on the concept of prototypes. In JavaScript, every object has an internal property called `[[Prototype]]` (also known as `__proto__`), which references another object. When you access a property or method on an object, and it doesn't exist on the object itself, JavaScript will look for it in the object's `[[Prototype]]` or its prototype chain.

Prototypical inheritance works by establishing a chain of objects where each object serves as the prototype for the next one. If an object doesn't have a property or method, JavaScript will automatically look for it in its prototype, and this process continues until the property or method is found or until the end of the prototype chain is reached.

In JavaScript, prototypical inheritance is implemented using constructor functions and their prototypes. When you create an object using a constructor function, the newly created object inherits properties and methods from the prototype object associated with that constructor function. This allows you to define shared behavior and characteristics for a group of objects.

<br>

<strong>Here's a simple example to demonstrate prototypical inheritance:</strong>


```
// Parent object constructor function
function Shape() {
}

// Method defined on the prototype of Shape
Shape.prototype.getArea = function() {
  console.log('This is the base shape.');
};

// Child object constructor function
function Circle(radius) {
  this.radius = radius;
}

// Set up the prototype chain
Circle.prototype = Object.create(Shape.prototype);
Circle.prototype.constructor = Circle;

// Method defined on the prototype of Circle
Circle.prototype.getRadius = function() {
  console.log('Radius:', this.radius);
};

// Create an instance of Circle
var myCircle = new Circle(5);

// Access properties and methods
myCircle.getArea();    // Output: This is the base shape.
myCircle.getRadius();  // Output: Radius: 5

```


<strong>Explaination : </strong>

In this example, the `Shape` constructor function defines the `getArea` method on its prototype. The `Circle` constructor function inherits from `Shape` by setting `Circle.prototype` to a new object created with `Object.create(Shape.prototype)`. This establishes the prototypical inheritance relationship, where the `Circle` prototype has access to the methods defined in the `Shape` prototype. The `Circle` prototype then defines its own method, `getRadius`. Finally, an instance of `Circle` is created and its properties and methods are accessed.

Through prototypical inheritance, the `myCircle` object inherits the `getArea` method from the `Shape` prototype and the `getRadius` method from the `Circle` prototype.


<strong>Diagram Explaination :</strong>


```
          +-------------------+
          |      Shape        |
          +-------------------+
          |   getArea()       |
          +-------------------+
                  ^
                  |
          +-------------------+
          |      Circle       |
          +-------------------+
          |   getRadius()     |
          +-------------------+
                  ^
                  |
          +-------------------+
          |     myCircle      |
          +-------------------+
          |     radius: 5     |
          +-------------------+
```

In this diagram, we have three objects: `Shape`, `Circle`, and `myCircle`. The `Shape` object serves as the prototype for the `Circle` object, and the `Circle` object serves as the prototype for the `myCircle` object. The `Shape` object has a method called `getArea()`, which is inherited by the `Circle` object. The `Circle` object also has its own method called `getRadius()`, which is inherited by the `myCircle` object. The `myCircle` object has its own property called `radius`.

This diagram illustrates the prototypical inheritance relationship, where objects inherit properties and methods from their prototypes.

<br>

## Why it gives you `false` as a boolean `[]===[]` ?

<br>

In JavaScript, `[]` is an empty array, and `[] === []` compares two separate empty array objects for equality. However, the comparison will return `false` because each array object is a unique instance in memory, even if they have the same contents.

To understand why `[] === []` returns `false`, consider the following:

- An array is an object in JavaScript.
- When you create a new array with the `[]` syntax, you are creating a new object in memory.
- If you create two separate empty arrays using `[]`, you will get two unique objects in memory, even if they look identical.
- The `===` operator checks for strict equality, meaning that it compares the values and types of the two operands.
- When you compare two objects with `===`, `it checks whether they are the same instance in memory, not whether their contents are the same.`

Therefore, `[] === []` compares two separate empty array objects for equality, and since they are two unique objects in memory, the comparison returns false.

<br>

## What is call , apply and bind in javascript ?

<br>

In JavaScript, call, apply, and bind are methods that can be used to manipulate the this value and invoke functions with a specific context.

- <strong><i>call :</i></strong> The `call` method allows you to invoke a function with a specified `this` value and arguments passed individually. The syntax is: `functionName.call(thisValue, arg1, arg2, ...)`. It sets the `this` value inside the function to the provided `thisValue` and allows you to pass arguments one by one.

- <strong><i>apply :</i></strong> Similar to `call`, the `apply` method allows you to invoke a function with a specified `this` value and arguments passed as an array or array-like object. The syntax is: `functionName.apply(thisValue, [arg1, arg2, ...])`. It sets the this value inside the function to the provided `thisValue` and allows you to pass arguments as an array or array-like object.

- <strong><i>bind :</i></strong> The `bind` method returns a new function with a bound `this` value and, optionally, pre-set arguments. The syntax is: `functionName.bind(thisValue, arg1, arg2, ...)`. It creates a new function where `this` is permanently bound to the provided `thisValue`, and you can also pass initial arguments that are pre-set for the function.

Here's an example to illustrate the usage of these methods :

```
var person = {
  name: 'John',
  sayHello: function() {
    console.log('Hello, ' + this.name);
  }
};

var sayHi = function(greeting) {
  console.log(greeting + ', ' + this.name);
};

person.sayHello();              // Output: Hello, John
sayHi.call(person, 'Hi');       // Output: Hi, John
sayHi.apply(person, ['Hola']);  // Output: Hola, John

var sayHola = sayHi.bind(person, 'Hola');
sayHola();                      // Output: Hola, John
```

In this example, we have an object `person` with a method `sayHello`. We also have a standalone function `sayHi`. By using `call` and `apply`, we can invoke `sayHi` with the `person` object as the `this` value and pass arguments. With `bind`, we create a new function `sayHola` with the `this` value bound to `person` and the initial argument `'Hola'`.

<br>

## What is Array.prototype.filter() in javascript ?

<br>

In JavaScript, `Array.prototype.filter()` is a built-in method that allows you to create a new array by filtering out elements from an existing array based on a specified condition. It provides a concise way to iterate over an array and selectively include elements that satisfy a given criteria.

The `filter()` method takes a callback function as its argument, which is executed for each element in the array. The callback function should return a Boolean value (`true` or `false`) to indicate whether the element should be included in the resulting filtered array.

The syntax for using `Array.prototype.filter()` is as follows:

```
const newArray = array.filter(callback(element, index, array));
```

- <strong><i>array :</i></strong> The original array that you want to filter.
- <strong><i>callback :</i></strong> A function that defines the filtering condition. It can take three arguments:
  - <b>element</b>: The current element being processed in the array.
  - <b>index (optional)</b>: The index of the current element.
  - <b>array (optional)</b>: The array on which the `filter()` method was called.

The `filter()` method returns a new array containing only the elements from the original array that passed the filtering condition.

Here's an example that demonstrates how to use `Array.prototype.filter()` to filter out even numbers from an array:

```
const numbers = [1, 2, 3, 4, 5, 6];
const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers); // Output: [2, 4, 6]
```

In this example, the `filter()` method is used to create a new array `evenNumbers` by filtering out the elements that are not even. The callback function `(number => number % 2 === 0)` checks if each number in the array is divisible by 2 (i.e., an even number), and only the even numbers are included in the resulting `evenNumbers` array.