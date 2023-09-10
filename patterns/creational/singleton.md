### Singleton:

Ensures that there is only one object created for a particular class.

In software engineering, the singleton pattern is a software design pattern that restricts the instantiation of a class to a "single" instance. This is useful when you need exactly one object to coordinate actions throughout the system.

**Example:**

**Step 1: Singleton Class Definition:**

```
class Singleton {
  constructor() {
    // ...
  }
  // ...
}
```

**Step 2: Check if an instance of the class already exists:**

```
const instance = this.constructor.instance;
if (instance) {
  return instance;
}
```

In this step, within the constructor of the Singleton class, we check if an instance of the class already exists using this.constructor.instance. If an instance exists, we return that instance instead of creating a new one.

**Step 3: Create instances of the Singleton class:**

```
let s1 = new Singleton();
let s2 = new Singleton();
```

In this step, we create two instances, s1 and s2, of the Singleton class.

**Step 4: Check if s1 and s2 are the same instance:**

```
console.log('Are they the same? ' + (s1 === s2));
```

Here, we check if s1 and s2 are the same instance using (s1 === s2) and display the result in the console.

**Step 5: Call the say() method:** In this final step, we call the say() method of the s1 instance, which will print "Saying..." to the console.

```
s1.say();
```

**Final Code:**

In this last step, we call the say() method of the s1 instance, which will print "Saying..." to the console.

```
// Singleton class definition
class Singleton {
  constructor() {
    // Check if an instance of the class already exists
    const instance = this.constructor.instance;
    if (instance) {
      // If it exists, return the existing instance
      return instance;
    }

    // If no instance exists, store this as the unique instance
    this.constructor.instance = this;
  }

  // Method to display a message
  say() {
    console.log('Saying...');
  }
}

// Create instances of the Singleton class
let s1 = new Singleton();
let s2 = new Singleton();

// Check if s1 and s2 are the same instance
console.log('Are they the same? ' + (s1 === s2));

// Call the say() method of the s1 instance
s1.say();

// Expected Output:
// Are they the same? true
// Saying...
```
