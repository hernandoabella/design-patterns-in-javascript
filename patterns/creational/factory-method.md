### Factory Method

The Factory Method design pattern is a software design technique that relies on creating objects of a specific subtype through a common interface. This pattern is achieved by using an abstract creator class that contains both concrete and abstract methods. The concrete methods handle object creation, while the abstract methods are implemented by concrete subclasses. Depending on the subclass used, specific behavior is obtained.

**Example:**

To better understand the Factory Method, let's consider a concrete example related to creating points in a two-dimensional plane. Imagine that we are developing an application that needs to work with points in Cartesian and polar coordinates.

First, we create a class called Point that represents a point in the plane. This class has a constructor that takes the x and y coordinates and a toString() method that returns a readable representation of the point in the format (x, y).

**Step 1: Definition of the Point class representing a point in the plane:**

```
// Point class representing a point in the plane
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  // Method to obtain a readable representation of the point
  toString() {
    return `(${this.x}, ${this.y})`;
  }
}
```

In this step, we have created the Point class with a constructor that takes the x and y coordinates and a toString() method to obtain a readable representation of the point.

**Step 2: Implementation of the Factory Method in the PointFactory class:**

```
// PointFactory class implementing the Factory Method
class PointFactory {
  // Method to create a point in Cartesian coordinates
  static createCartesianPoint(x, y) {
    return new Point(x, y);
  }

  // Method to create a point in polar coordinates
  static createPolarPoint(rho, theta) {
    return new Point(rho * Math.cos(theta), rho * Math.sin(theta));
  }
}
```

In this step, we have created the PointFactory class that implements the Factory Method. This class contains two static methods: createCartesianPoint and createPolarPoint. The first one creates a point in Cartesian coordinates, and the second one creates a point in polar coordinates.

**Step 3: Example of using the Factory Method:**

```
// Example of using the Factory Method
const cartesianPoint = PointFactory.createCartesianPoint(5, 6);
const polarPoint = PointFactory.createPolarPoint(5, Math.PI / 2);
```

In this step, we have created two points using the PointFactory. One is created in Cartesian coordinates using createCartesianPoint, and the other is created in polar coordinates using createPolarPoint.

**Step 4: Printing the created points:**

```
// Printing the created points
console.log("Cartesian Point:", cartesianPoint.toString()); // Cartesian Point: (5, 6)
console.log("Polar Point:", polarPoint.toString()); // Polar Point: (6.123233995736766e-17, 5)
```

In this final step, we have printed the created points to verify the result.

**Final Code:**

```
// Point class representing a point in the plane
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  // Method to obtain a readable representation of the point
  toString() {
    return `(${this.x}, ${this.y})`;
  }
}

// PointFactory class implementing the Factory Method
class PointFactory {
  // Method to create a point in Cartesian coordinates
  static createCartesianPoint(x, y) {
    return new Point(x, y);
  }

  // Method to create a point in polar coordinates
  static createPolarPoint(rho, theta) {
    return new Point(rho * Math.cos(theta), rho * Math.sin(theta));
  }
}

// Example of using the Factory Method
const cartesianPoint = PointFactory.createCartesianPoint(5, 6);
const polarPoint = PointFactory.createPolarPoint(5, Math.PI / 2);

// Printing the created points
console.log("Cartesian Point:", cartesianPoint.toString()); // Cartesian Point: (5, 6)
console.log("Polar Point:", polarPoint.toString()); // Polar Point: (6.123233995736766e-17, 5)
```
