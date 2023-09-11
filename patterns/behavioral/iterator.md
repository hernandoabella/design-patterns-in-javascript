### Iterador

Iterator accesses the elements of an object without exposing its underlying representation.

In object-oriented programming, the iterator pattern is a design pattern where an iterator is used to traverse a container and access the elements of the container.

Definition of the 'Thing' Class: First, we define a class called 'Thing' that has two properties 'a' and 'b.'

**Step 1:** Define the 'Thing' class and its 'a' and 'b' properties.
```
class Thing {
  constructor() {
    this.a = 11;
    this.b = 22;
  }
  // Rest of the code
}

```

**Step 2:** Implement the Symbol.iterator method to traverse the 'a' and 'b' properties of the 'Thing' class.

```
class Thing {
  // ...

  [Symbol.iterator]() {
    let i = 0;
    let self = this;
    return {
      next: function() {
        return {
          done: i > 1,
          value: self[i++ === 0 ? 'a' : 'b']
        };
      }
    };
  }

  // Rest of the code
}
```

**Step 3:** Implement the 'backwards' property to traverse the properties in reverse order.

```
class Thing {
  // ...

  get backwards() {
    let i = 0;
    let self = this;
    return {
      next: function() {
        return {
          done: i > 1,
          value: self[i++ === 0 ? 'b' : 'a']
        };
      },
      [Symbol.iterator]: function() { return this; }
    };
  }

  // Rest of the code
}
```

**Step 4:** Create an array 'values' with numeric elements.

```
let values = [100, 200, 300];
```

**Step 5:** Use a 'for...in' loop to iterate over the 'values' array.

```
for (let i in values) {
  console.log(`Element at position ${i} is ${values[i]}`);
}
```

**Step 6:** Use another 'for...in' loop to iterate over an object (not recommended).

```
for (let v in values) {
  console.log(`The value is ${v}`);
}

```

**Step 7:** Create an instance of the 'Thing' class called 'thing'.

```
let thing = new Thing();
```

**Step 8:** Use a 'for...of' loop to iterate over the properties of 'thing.'.

```
console.log("Iterating over 'a' and 'b':");
for (let element of thing) {
  console.log(`${element}`);
}
```

**Step 9:** Use another 'for...of' loop to iterate in reverse order.

```
console.log("Iterating in reverse order:");
for (let element of thing.backwards) {
  console.log(`${element}`);
}
```

**Final Code:**

We will take the example of an array where we print the values of an array and then, using an iterator, print its values in reverse.

```
// Define a class called 'Thing'
class Thing {
  constructor() {
    this.a = 11; // Property 'a' with value 11
    this.b = 22; // Property 'b' with value 22
  }

  // Define an iterator to traverse the elements 'a' and 'b' of this class
  [Symbol.iterator]() {
    let i = 0; // Initialize an index to keep control
    let self = this; // Capture a reference to the current instance ('this')
    return {
      next: function() {
        return {
          done: i > 1, // Indicates if everything has been traversed (when 'i' is greater than 1)
          value: self[i++ === 0 ? 'a' : 'b'] // Get the corresponding value ('a' or 'b')
        };
      }
    };
  }

  // Get an iterator to traverse the elements in reverse order
  get backwards() {
    let i = 0; // Initialize an index to keep control
    let self = this; // Capture a reference to the current instance ('this')
    return {
      next: function() {
        return {
          done: i > 1, // Indicates if everything has been traversed (when 'i' is greater than 1)
          value: self[i++ === 0 ? 'b' : 'a'] // Get the corresponding value ('b' or 'a')
        };
      },
      [Symbol.iterator]: function() { return this; } // Make the iterator iterable
    };
  }
}

let values = [100, 200, 300];

// Use a for...in loop to traverse an array (Note: not the recommended way for arrays)
for (let i in values) {
  console.log(`Element at position ${i} is ${values[i]}`);
}

// Use a for...in loop to traverse an object (Note: not the recommended way for objects)
for (let v in values) {
  console.log(`The value is ${v}`);
}

let thing = new Thing(); // Create an instance of the class 'Thing'

console.log("Iterating over 'a' and 'b':");
for (let element of thing) {
  console.log(`${element}`);
}

console.log("Iterating in reverse order:");
for (let element of thing.backwards) {
  console.log(`${element}`);
}

// Expected output:
// Element at position 0 is 100
// Element at position 1 is 200
// The value is 0
// The value is 1
// The value is 2
// Iterating over 'a' and 'b':
// 11
// 22
// Iterating in reverse order:
// 22
// 11

```
