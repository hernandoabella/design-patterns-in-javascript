### Observer

Allows multiple observer objects to watch an event.

The Observer pattern is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and automatically notifies them of any state changes, usually by calling one of their methods.

**Example:**

Let's take an example of a person where if a person gets sick, it shows a notification.

**Step 1. Definition of classes and the Observer Pattern:** In this step, we define three key classes: Event, GetSick, and Person. The Event class represents an observable event and contains the logic for subscribing, unsubscribing, and notifying observers. The GetSick class is a specific event that contains information about the location where it occurs. The Person class is the observable subject that can "get sick" and notify observers when this happens.

```
// Event class representing an observable event
class Event {
  constructor() {
    this.handlers = new Map();
    this.counter = 0;
  }

  // Method to subscribe a handler to the event and return a unique identifier
  subscribe(handler) {
    this.handlers.set(++this.counter, handler);
    return this.counter;
  }

  // Method to unsubscribe from an event given an identifier
  unsubscribe(index) {
    this.handlers.delete(index);
  }

  // Method to notify all observers when the event occurs
  fire(sender, args) {
    this.handlers.forEach((handler, id) => handler(sender, args));
  }
}

// GetSick class representing a specific event
class GetSick {
  constructor(location) {
    this.location = location;
  }
}

// Person class that will be the observable subject
class Person {
  constructor(location) {
    this.location = location;
    this.getSick = new Event(); // Create a "get sick" event
  }

  // Method to simulate the person getting sick and notify observers
  catchCold() {
    this.getSick.fire(this, new GetSick(this.location));
  }
}
```

**Step 2. Using the Observer Pattern:** In this step, we create an instance of Person and then subscribe an observer to the "get sick" event using the subscribe method of the Event class. We then simulate the person getting sick twice by calling the catchCold method. After that, we unsubscribe the observer using the unsubscribe method. Finally, we call the catchCold method again, but the unsubscribed observer no longer receives notifications.

This pattern allows multiple observers to watch an event (in this case, getting sick) without the Person class needing to know the details of who the observers are or how they react to the event.

```
// Create an instance of the person
let person = new Person("Route ABC");

// Subscribe an observer to the "get sick" event
let sub = person.getSick.subscribe((subject, event) => {
  console.log(`A doctor has been called to ${event.location}`);
});

// The person gets sick twice
person.catchCold();
person.catchCold();

// Unsubscribe the observer
person.getSick.unsubscribe(sub);

// The person gets sick again, but the unsubscribed observer no longer receives the notification
person.catchCold();
```

**Final Code:**

```
// Definition of classes and the Observer Pattern

// Event class representing an observable event
class Event {
  constructor() {
    this.handlers = new Map();
    this.counter = 0;
  }

  // Method to subscribe a handler to the event and return a unique identifier
  subscribe(handler) {
    this.handlers.set(++this.counter, handler);
    return this.counter;
  }

  // Method to unsubscribe from an event given an identifier
  unsubscribe(index) {
    this.handlers.delete(index);
  }

  // Method to notify all observers when the event occurs
  fire(sender, args) {
    this.handlers.forEach((handler, id) => handler(sender, args));
  }
}

// GetSick class representing a specific event
class GetSick {
  constructor(location) {
    this.location = location;
  }
}

// Person class that will be the observable subject
class Person {
  constructor(location) {
    this.location = location;
    this.getSick = new Event(); // Create a "get sick" event
  }

  // Method to simulate the person getting sick and notify observers
  catchCold() {
    this.getSick.fire(this, new GetSick(this.location));
  }
}

// Using the Observer Pattern

// Create an instance of the person
let person = new Person("Route ABC");

// Subscribe an observer to the "get sick" event
let sub = person.getSick.subscribe((subject, event) => {
  console.log(`A doctor has been called to ${event.location}`);
});

// The person gets sick twice
person.catchCold();
person.catchCold();

// Unsubscribe the observer
person.getSick.unsubscribe(sub);

// The person gets sick again, but the unsubscribed observer no longer receives the notification
person.catchCold();

```
