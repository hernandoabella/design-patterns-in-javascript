### Mediator

The mediator pattern adds a third-party object to control the interaction between two objects. It allows for flexible coupling between classes since it is the only class with detailed knowledge of its methods.

The mediator pattern defines an object that encapsulates how a set of objects interact. This pattern is considered a behavioral pattern due to the way it can alter the program's execution behavior. In object-oriented programming, programs often consist of many classes.

We will use an example of a person using a chat room. Here, a chat room acts as a mediator between two people communicating with each other.

**Example:**

**Step 1:** Definition of the Person class, which represents people in the chat room:

```
class Person {
  constructor(name, chatRoom) {
    this.name = name;         // Person's name
    this.chatRoom = chatRoom; // Chat room they belong to
  }

  // Method to send a message in the chat room
  say(message) {
    this.chatRoom.sendMessage(this, message);
  }

  // Method to receive a message
  receive(message) {
    console.log(`${this.name} receives: ${message}`);
  }
}

```

**Step 2:** Definition of the ChatRoom class, which acts as a mediator:

```
class ChatRoom {
  constructor() {
    this.people = []; // Stores people in the chat room
  }

  // Method to add a person to the chat room
  joinPerson(person) {
    this.people.push(person); // Add the person to the list
    person.chatRoom = this;  // Set the person's chat room as this room
  }

  // Method to send a message to all people in the room
  sendMessage(sender, message) {
    for (const person of this.people) {
      if (person !== sender) {
        person.receive(`${sender.name}: ${message}`);
      }
    }
  }
}
```

**Step 3:** Creation of a chat room (ChatRoom):

```
const chatRoom = new ChatRoom();
```

**Step 4:** Creation of people and joining them to the chat room:

```
const john = new Person("John", chatRoom);
const tony = new Person("Tony", chatRoom);

chatRoom.joinPerson(john);
chatRoom.joinPerson(tony);
```

**Step 5:** John sends a message in the chat room:

```
john.say("Hello, everyone!");
```

**Step 6:** Creation of a new person and joining them to the chat room:

```
const doe = new Person("Doe", chatRoom);
chatRoom.joinPerson(doe);
```

**Step 7:** Doe sends a message in the chat room:

```
doe.say("Hi, everyone!");
```

Whenever someone sends a message, the chat room takes care of distributing that message to all the other people in the room.

**Final Code:**

```
// Definition of the Person class, which represents people in the chat room
class Person {
  constructor(name, chatRoom) {
    this.name = name;         // Person's name
    this.chatRoom = chatRoom; // Chat room they belong to
  }

  // Method to send a message in the chat room
  say(message) {
    this.chatRoom.sendMessage(this, message);
  }

  // Method to receive a message
  receive(message) {
    console.log(`${this.name} receives: ${message}`);
  }
}

// Definition of the ChatRoom class, which acts as a mediator
class ChatRoom {
  constructor() {
    this.people = []; // Stores people in the chat room
  }

  // Method to add a person to the chat room
  joinPerson(person) {
    this.people.push(person); // Add the person to the list
    person.chatRoom = this;  // Set the person's chat room as this room
  }

  // Method to send a message to all people in the room
  sendMessage(sender, message) {
    for (const person of this.people) {
      if (person !== sender) {
        person.receive(`${sender.name}: ${message}`);
      }
    }
  }
}

// Creation of a chat room
const chatRoom = new ChatRoom();

// Creation of people and joining them to the chat room
const john = new Person("John", chatRoom);
const tony = new Person("Tony", chatRoom);

chatRoom.joinPerson(john);
chatRoom.joinPerson(tony);

// John sends a message in the chat room
john.say("Hello, everyone!");

// Creation of a new person and joining them to the chat room
const doe = new Person("Doe", chatRoom);
chatRoom.joinPerson(doe);

// Doe sends a message in the chat room
doe.say("Hi, everyone!");
```
