### Visitor

Add operations to objects without having to modify them.

The visitor design pattern is a way to separate an algorithm from an object structure it operates on. A practical result of this separation is the ability to add new operations to existing object structures without modifying those structures.

**Example:**

Let's take an example of the NumericExpression class that gives us the result of the given expression.

**1. NumericExpression Class:** This class represents a simple numeric expression with a value.

```
class NumericExpression {
  constructor(value) {
    this.value = value;
  }

  print(buffer) {
    buffer.push(this.value.toString());
  }
}
```

**2. SumExpression Class:** This class represents a sum expression that takes two numeric expressions (left and right) and adds them.

```
class SumExpression {
  constructor(left, right) {
    this.left = left;
    this.right = right;
  }

  print(buffer) {
    buffer.push('(');
    this.left.print(buffer);
    buffer.push('+');
    this.right.print(buffer);
    buffer.push(')');
  }
}
```

**3. Using the Visitor Pattern:** Next, you create a composite expression that represents "5 + (1 + 9)" using instances of the NumericExpression and SumExpression classes.

```
let e = new SumExpression(
    new NumericExpression(5),
    new SumExpression(
        new NumericExpression(1),
        new NumericExpression(9)
    )
);
```

Printing the Expression: Finally, you use the print() method to get a readable representation of the expression and store it in a buffer.

```
let buffer = [];
e.print(buffer);
console.log(buffer.join('')); // Output: (5+(1+9))
```

This example illustrates how the visitor design pattern allows you to add the printing operation to complex objects without having to modify their internal structure. This makes the code more flexible and extensible for future operations without affecting existing classes.

**Final Code:**

```
class NumericExpression {
  constructor(value) {
    this.value = value;
  }

  print(buffer) {
    buffer.push(this.value.toString());
  }
}

class SumExpression {
  constructor(left, right) {
    this.left = left;
    this.right = right;
  }

  print(buffer) {
    buffer.push('(');
    this.left.print(buffer);
    buffer.push('+');
    this.right.print(buffer);
    buffer.push(')');
  }
}

// Creating a composite expression: 5 + (1 + 9)
let e = new SumExpression(
    new NumericExpression(5),
    new SumExpression(
        new NumericExpression(1),
        new NumericExpression(9)
    )
);

let buffer = [];
e.print(buffer);

console.log(buffer.join('')); // Expected Output: (5+(1+9))
```

The expected output is (5+(1+9)), which is the representation of the "5 + (1 + 9)" expression after printing it using the visitor pattern. This code demonstrates how the visitor pattern allows adding the printing operation to complex objects without modifying their internal structure.
