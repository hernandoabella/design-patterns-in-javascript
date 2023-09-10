### Decorator

The decorator pattern allows dynamically adding or overriding behaviors to an individual object without affecting other objects of the same class. It is especially useful when you want to extend the capabilities of an object without creating subclasses.

**Example:**

**1. Class Definitions:** In this example, we create the Form class as the base and Circle as a concrete shape we want to decorate. We also create a class called ColoredShape that acts as a decorator to add colors to shapes.

```
class Form {
  constructor(color) {
    this.color = color;
  }
}

class Circle extends Form {
  constructor(radius = 0) {
    super();
    this.radius = radius;
  }

  resize(factor) {
    this.radius *= factor;
  }

  toString() {
    return `A circle of radius ${this.radius}`;
  }
}

class ColoredShape extends Form {
  constructor(shape, color) {
    super();
    this.shape = shape;
    this.color = color;
  }

  toString() {
    return `${this.shape.toString()}, colored ${this.color}`;
  }
}
```

**2. Using the Decorator:** We create an instance of a base circle and then decorate that circle with a red color using the ColoredShape class.

```
// Create a base circle
let circle = new Circle(2);
console.log(circle.toString()); // Output: A circle of radius 2

// Decorate the circle with red color
let redCircle = new ColoredShape(circle, "red");
console.log(redCircle.toString()); // Output: A circle of radius 2, colored red
```

**Final Code:**

```
// Base class for all shapes
class Form {
  constructor(color) {
    this.color = color;
  }
}

// Concrete class for a circle that inherits from Form
class Circle extends Form {
  constructor(radius = 0) {
    super();
    this.radius = radius;
  }

  resize(factor) {
    this.radius *= factor;
  }

  toString() {
    return `A circle of radius ${this.radius}`;
  }
}

// Decorator class that adds color to an existing shape
class ColoredShape extends Form {
  constructor(shape, color) {
    super();
    this.shape = shape;
    this.color = color;
  }

  toString() {
    return `${this.shape.toString()}, colored ${this.color}`;
  }
}

// Create a base circle
let circle = new Circle(2);
console.log(circle.toString()); // Output: A circle of radius 2

// Decorate the circle with red color
let redCircle = new ColoredShape(circle, "red");
console.log(redCircle.toString()); // Output: A circle of radius 2, colored red

```
