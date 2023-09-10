### Proxy

The Proxy pattern allows one class to represent the functionality of another class, acting as an intermediary or "proxy" between the client and the real object. This can be useful for controlling access to the real object, performing additional operations before or after accessing the real object, or even replacing the real object entirely.

**Example:**

Let's imagine an example of a Proxy object called "Percentage" used to represent percentages. This Proxy allows manipulating percentage values and performing mathematical operations on them.

```
class Percentage {
  constructor(percentage) {
    this.percentage = percentage;
  }

  toString() {
    return `${this.percentage}%`;
  }

  valueOf() {
    return this.percentage / 100;
  }
}

// Let's use the Percentage Proxy object
let percentageFive = new Percentage(5);
console.log(percentageFive.toString()); // Output: "5%"
console.log(`5% of 50 is ${50 * percentageFive}`); // Output: "5% of 50 is 2.5"
```

In this example, the "Percentage" acts as a proxy that allows representing percentage values and performing calculations with them. The Percentage Proxy makes it easy to manipulate percentage values and use them in mathematical operations.
