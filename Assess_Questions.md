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