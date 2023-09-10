### Flyweight

The Flyweight pattern is used to minimize memory usage when creating similar objects by sharing as much data as possible among them. This means that instead of creating multiple instances of objects with identical data, a shared instance is used to represent that common data. This significantly reduces the amount of memory used, especially when working with large quantities of similar objects.

**Example:**

**Step 1: Definition of User and User2 Classes:**: In this step, we define two classes: User and User2. The first represents a simple user with a full name, while the second implements the Flyweight pattern to reduce memory usage by sharing similar full names.

```
// Definition of the User class
class User {
  constructor(fullName) {
    this.fullName = fullName;
  }
}

// Definition of the User2 class that implements the Flyweight pattern
class User2 {
  constructor(fullName) {
    let getOrAdd = function(s) {
      let idx = User2.strings.indexOf(s);
      if (idx !== -1) return idx;
      else {
        User2.strings.push(s);
        return User2.strings.length - 1;
      }
    };
    this.names = fullName.split(' ').map(getOrAdd);
  }
}

User2.strings = [];
```

**Step 2: Auxiliary Functions:** In this step, we create two auxiliary functions: getRandomInteger to obtain random integers and getRandomText to generate random text strings.

```
// Auxiliary functions
function getRandomInteger(max) {
  return Math.floor(Math.random() * Math.floor(max));
}

function getRandomText() {
  let result = [];
  for (let x = 0; x < 10; ++x)
    result.push(String.fromCharCode(65 + getRandomInteger(26)));
  return result.join('');
}
```

**Step 3: Creating Random Names:** In this step, we create two arrays, names and lastNames, which contain randomly generated names and last names that will be used to create users.

```
// Creating Random Names
let names = lastNames = [];
for (let i = 0; i < 100; ++i) {
  names.push(getRandomText());
  lastNames.push(getRandomText());
}
```

**Step 4: Creating Users:** In this step, we create two arrays, users and users2, which will contain the created users. We iterate through the names and last names arrays to create 10,000 users both without the Flyweight pattern and with it.

```
let users = [];
let users2 = [];

// Creating Users
for (let name of names) {
  for (let lastName of lastNames) {
    users.push(new User(`${name} ${lastName}`));
    users2.push(new User2(`${name} ${lastName}`));
  }
}
```

**Step 5: Memory Usage Comparison:** In this step, we compare the memory usage between users without the Flyweight pattern and users with it using JSON.stringify. We print the results to the console.

```
// Memory Usage Comparison
console.log(`10,000 users occupy approximately ${JSON.stringify(users).length} characters`);
let users2Length = [users2, User2.strings].map(x => JSON.stringify(x).length).reduce((x, y) => x + y);
console.log(`10,000 users with Flyweight occupy ~${users2Length} characters`);
```

**Final Code:**

```
// Definition of the User class
class User {
  constructor(fullName) {
    this.fullName = fullName;
  }
}

// Definition of the User2 class that implements the Flyweight pattern
class User2 {
  constructor(fullName) {
    let getOrAdd = function(s) {
      let idx = User2.strings.indexOf(s);
      if (idx !== -1) return idx;
      else {
        User2.strings.push(s);
        return User2.strings.length - 1;
      }
    };
    this.names = fullName.split(' ').map(getOrAdd);
  }
}

User2.strings = [];

// Auxiliary functions
function getRandomInteger(max) {
  return Math.floor(Math.random() * Math.floor(max));
}

function getRandomText() {
  let result = [];
  for (let x = 0; x < 10; ++x)
    result.push(String.fromCharCode(65 + getRandomInteger(26)));
  return result.join('');
}

// Creating Random Names
let names = lastNames = [];
for (let i = 0; i < 100; ++i) {
  names.push(getRandomText());
  lastNames.push(getRandomText());
}

let users = [];
let users2 = [];

// Creating Users
for (let name of names) {
  for (let lastName of lastNames) {
    users.push(new User(`${name} ${lastName}`));
    users2.push(new User2(`${name} ${lastName}`));
  }
}

// Memory Usage Comparison
console.log(`10,000 users occupy approximately ${JSON.stringify(users).length} characters`); // 10,000 users occupy approximately 1720001 characters
let users2Length = [users2, User2.strings].map(x => JSON.stringify(x).length).reduce((x, y) => x + y);
console.log(`10,000 users with Flyweight occupy ~${users2Length} characters`); // 10,000 users with Flyweight occupy ~838602 characters
```
