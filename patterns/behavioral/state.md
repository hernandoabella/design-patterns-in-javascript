### State

Modifies the behavior of an object when its internal state changes.

The State pattern is a behavioral software design pattern that allows an object to alter its behavior when its internal state changes. This pattern is closely related to the concept of finite state machines.

**Example:**

Let's take an example of a light switch in which turning the switch on or off changes its state.

This is an example of the "State" design pattern, which allows an object to change its behavior when its internal state changes. Here is the code with comments explaining each step:

**Step 1:** We create two state classes, OnState and OffState, which inherit from the base State class. Each state class defines how the switch should behave when it is in that particular state.

```
class OnState extends State {
  constructor() {
    super();
    console.log("Lights are on");
  }
  
  turnOff(sw) {
    console.log("Turning off the lights...");
    sw.state = new OffState();
  }
}

class OffState extends State {
  constructor() {
    super();
    console.log("Lights are off...");
  }
  
  turnOn(sw) {
    console.log("Turning on the lights...");
    sw.state = new OnState();
  }
}

```

**Step 2:** We create the Switch class, which contains an internal state and turnOn() and turnOff() methods to change the state. We initialize the switch with the off state.

```
class Switch {
  constructor() {
    this.state = new OffState();
  }
  
  turnOn() {
    this.state.turnOn(this);
  }
  
  turnOff() {
    this.state.turnOff(this);
  }
}


```

**Step 3:** We create the abstract base class State, which defines the turnOn() and turnOff() methods. Concrete state classes must implement these methods.

```
class State {
  constructor() {
    if (this.constructor === State) throw new Error("Abstract!");
  }
  
  turnOn(sw) {
    console.log("The light is on.");
  }
  
  turnOff(sw) {
    console.log("The light is off.");
  }
}

```

**Step 4:** We create an instance of the Switch class and test its methods to change the state of the lights. First, we turn the lights on and then we turn them off.

```
let lightSwitch = new Switch();
lightSwitch.turnOn();
lightSwitch.turnOff();
```

This example demonstrates how the "State" design pattern allows an object, in this case, a light switch, to change its behavior based on its internal state (on or off). Each state has its own behaviors defined in the concrete state classes.

**Final Code:**

```
// Create two state classes

class OnState extends State {
  constructor() {
    super();
    console.log("Lights are on");
  }
  
  turnOff(sw) {
    console.log("Turning off the lights...");
    sw.state = new OffState();
  }
}

class OffState extends State {
  constructor() {
    super();
    console.log("Lights are off...");
  }
  
  turnOn(sw) {
    console.log("Turning on the lights...");
    sw.state = new OnState();
  }
}

// Create the Switch class

class Switch {
  constructor() {
    this.state = new OffState(); // Initialize with the off state
  }
  
  turnOn() {
    this.state.turnOn(this); // Call the turn-on method of the current state
  }
  
  turnOff() {
    this.state.turnOff(this); // Call the turn-off method of the current state
  }
}

// Create the abstract base class State

class State {
  constructor() {
    if (this.constructor === State) throw new Error("Abstract!"); // Prevent direct instantiation
  }
  
  turnOn(sw) {
    console.log("The light is on.");
  }
  
  turnOff(sw) {
    console.log("The light is off.");
  }
}

// Create an instance of the Switch class and test its methods

let lightSwitch = new Switch();
lightSwitch.turnOn(); // Turn on the lights
lightSwitch.turnOff(); // Turn off the lights
```