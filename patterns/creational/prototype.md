### Prototype

Creates new objects based on existing objects.

The prototype pattern is a creational design pattern in software development. It is used when the type of objects to create is determined by a prototype instance, which is cloned to produce new objects.

**Example:**

We will use the example of a car.

**Step 1: Definition of the Car Class (Prototype)**

```
class Car {
  constructor(name, model) {
    this.name = name;
    this.model = model;
  }

  // ... (Class methods)
}
```

**Step 2: Method to set the car's name**

```
// Method to set the car's name
setCarName(name) {
  this.name = name;
  console.log(`Car name adjusted to: ${this.name}`);
}
```

**Step 3: Method to clone the car (create a copy)**

```
// Method to clone the car (create a copy)
clone() {
  // Create a new Car instance with the same attributes
  return new Car(this.name, this.model);
}
```

**Step 4: Using the Prototype Pattern**

```
// Using the Prototype Pattern
const originalCar = new Car('Audi', 'A3');

// Clone the original car to create a new instance
const clonedCar = originalCar.clone();
clonedCar.setCarName('BMW');
```

**Step 5: Verify that the cars are different**

```
// Verify that the cars are different
console.log('Original Car:', originalCar.name, originalCar.model);
console.log('Cloned Car:', clonedCar.name, clonedCar.model);
```

This code demonstrates how to use the Prototype Pattern to create a copy of an existing object (originalCar) and adjust its attributes (name) without affecting the original object. In the end, it verifies that the two cars are different, confirming that the clone worked correctly.

**Final Code:**

```
// Definition of the Car Class (Prototype)
class Car {
  constructor(name, model) {
    this.name = name;
    this.model = model;
  }

  // Method to set the car's name
  setCarName(name) {
    this.name = name;
    console.log(`Car name adjusted to: ${this.name}`);
  }

  // Method to clone the car (create a copy)
  clone() {
    // Create a new Car instance with the same attributes
    return new Car(this.name, this.model);
  }
}

// Using the Prototype Pattern
const originalCar = new Car('Audi', 'A3');

// Clone the original car to create a new instance
const clonedCar = originalCar.clone();
clonedCar.setCarName('BMW');

// Verify that the cars are different
console.log('Original Car:', originalCar.name, originalCar.model);
console.log('Cloned Car:', clonedCar.name, clonedCar.model);

// Expected Output:
// Car name adjusted to: BMW
// Original Car: Audi A3
// Cloned Car: BMW A3
```
