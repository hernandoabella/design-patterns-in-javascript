### Adapter 🔌

The adapter pattern enables classes with incompatible interfaces to collaborate by adapting their own interface to fit around the existing class. This is particularly useful when we need objects with different interfaces to work together without altering their source code.

**Example:** 

**1. Definition of Incompatible Interfaces:** In this example, we have two calculator interfaces: Calculator1 (old) and Calculator2 (new).

```
class Calculator1 {
  constructor() {
    this.operations = function(value1, value2, operation) {
      // Implementation of the old calculator
      switch(operation) {
        case 'sum':
          return value1 + value2;
        case 'subtract':
          return value1 - value2;
      }
    };
  }
}

class Calculator2 {
  constructor() {
    this.add = function(value1, value2) {
      // Implementation of the new calculator
      return value1 + value2;
    };
    
    this.subtract = function(value1, value2) {
      // Implementation of the new calculator
      return value1 - value2;
    };
  }
}
```

**2. Creating an Adapter:** We create a CalcAdapter class that will act as an adapter between the two calculator interfaces. The adapter wraps the new interface (Calculator2) and provides methods for the required operations.

```
class CalcAdapter {
  constructor() {
    const cal2 = new Calculator2();
    this.operations = function(value1, value2, operation) {
      switch(operation) {
        case 'sum':
          return cal2.add(value1, value2);
        case 'subtract':
          return cal2.subtract(value1, value2);
      }
    };
  }
}
```

**3. Using the Adapter:** Now, we can use the CalcAdapter to perform operations on the new interface (Calculator2) without modifying its code. This makes transitioning from the old calculator to the new one easier.

```
// Create an instance of the adapter
const calcAdapter = new CalcAdapter();

// Use the adapter to perform a subtraction operation
console.log(calcAdapter.operations(10, 55, 'subtract'));
```

**Final Code:**

```
// Definition of the Old Calculator Class
class OldCalculator {
  constructor() {
    this.operations = function(value1, value2, operation) {
      switch(operation) {
        case 'add':
          return value1 + value2;
        case 'subtract':
          return value1 - value2;
      }
    };
  }
}

// Definition of the New Calculator Class
class NewCalculator {
  constructor() {
    this.add = function(value1, value2) {
      return value1 + value2;
    };
    
    this.subtract = function(value1, value2) {
      return value1 - value2;
    };
  }
}

// Definition of the Adapter Class
class CalculatorAdapter {
  constructor() {
    // Create an instance of the New Calculator
    const newCalculator = new NewCalculator();
    
    // Define the operations method that will use the New Calculator
    this.operations = function(value1, value2, operation) {
      switch(operation) {
        case 'add':
          return newCalculator.add(value1, value2);
        case 'subtract':
          return newCalculator.subtract(value1, value2);
      }
    };
  }
}

// Create an instance of the Calculator Adapter
const calculatorAdapter = new CalculatorAdapter();

// Use the Calculator Adapter to perform a subtraction operation
console.log(calculatorAdapter.operations(10, 55, 'subtract')); // -45
console.log(calculatorAdapter.operations(10, 55, 'add')); // 65
```
