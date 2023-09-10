### Bridge

The Bridge design pattern is used to separate the abstraction from the implementation, allowing both to evolve independently. In other words, the Bridge pattern is used when you want to avoid a tight connection between an abstract class and its concrete classes, enabling them to evolve independently without affecting each other.

**Example:**

In this example, we will create classes for rendering geometric shapes. We will use two renderer classes: VectorRenderer and RasterRenderer. Then, we will create an abstract class Shape and a Circle class that inherits from Shape. The key to the Bridge pattern is that Shape has a reference to a renderer and delegates the rendering task to the concrete renderer.

**Step 1. Definition of Renderer Classes:** In this step, we create the VectorRenderer and RasterRenderer classes, representing different rendering methods.

```
class VectorRenderer {
  renderCircle(radius) {
    console.log(`Drawing a circle of radius ${radius}`);
  }
}

class RasterRenderer {
  renderCircle(radius) {
    console.log(`Drawing pixels for circle of radius ${radius}`);
  }
}
```

**Step 2. Definition of Abstract Class Shape:** In this step, we create the abstract class Shape that will act as our abstraction. This class has a renderer attribute that is a reference to the renderer we will use to draw the shape.

```
class Shape {
  constructor(renderer) {
    this.renderer = renderer;
  }
}
```

**Step 3. Definition of Circle Class:** In this step, we create the Circle class that inherits from Shape. The Circle class has a radius attribute representing the circle's radius.

```
class Circle extends Shape {
  constructor(renderer, radius) {
    super(renderer);
    this.radius = radius;
  }
}
```

**Step 4. Implementation of the draw Method:** In the Circle class, we implement the draw method. This method delegates the rendering task to the concrete renderer (VectorRenderer or RasterRenderer) through the this.renderer reference.

```
draw() {
  this.renderer.renderCircle(this.radius);
}
```

**Step 5. Creating Instances of Renderers and Circle:** In this step, we create instances of the renderer classes VectorRenderer and RasterRenderer. Then, we create an instance of Circle named circle and provide it with the vector renderer and a radius of 5.

```
let raster = new RasterRenderer();
let vector = new VectorRenderer();
let circle = new Circle(vector, 5);
```

**Step 6. Drawing the Circle and Changing Its Size:** We call the draw method on the circle instance, resulting in the printing of the corresponding message for the vector renderer. Then, we change the size of the circle by calling the resize method, doubling its radius.

```
circle.draw();
circle.resize(2);
```

**Step 7. Drawing the Circle After Size Change:** We call the draw method again on the circle instance, resulting in the updated message after the size change.

```
circle.draw();
```

**Final Code:**

```
// Definition of Renderer Classes
class VectorRenderer {
  renderCircle(radius) {
    console.log(`Drawing a circle of radius ${radius}`);
  }
}

class RasterRenderer {
  renderCircle(radius) {
    console.log(`Drawing pixels for circle of radius ${radius}`);
  }
}

// Definition of the Abstract Class `Shape`
class Shape {
  constructor(renderer) {
    this.renderer = renderer;
  }
}

// Definition of the `Circle` Class
class Circle extends Shape {
  constructor(renderer, radius) {
    super(renderer);
    this.radius = radius;
  }

  // Implementation of the `draw` Method
  draw() {
    this.renderer.renderCircle(this.radius);
  }

  resize(factor) {
    this.radius *= factor;
  }
}

// Creating Instances of Renderers and Circle
let raster = new RasterRenderer();
let vector = new VectorRenderer();
let circle = new Circle(vector, 5);

// Drawing the Circle and Changing Its Size
circle.draw();
circle.resize(2);

// Drawing the Circle After Size Change
circle.draw();

// Expected Output:
// Drawing a circle of radius 5
// Drawing a circle of radius 10
```
