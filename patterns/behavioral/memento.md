### Memento

The Memento pattern allows restoring an object to its previous state.

The Memento pattern is a software design pattern that provides the capability to restore an object to a previous state. It is implemented using three objects: the originator, the caretaker, and the memento.

**Example:**

Let's take an example of a bank account in which we store our previous state and have the functionality to undo.

**Step 1. Definition of the Memento class:**

```
class Memento {
  constructor(balance) {
    this.balance = balance;
  }
}
```

In this step, we create the Memento class, which will be used to store the state of the bank account at a given moment.

**Step 2. Definition of the CuentaBanco class:**

```
class BankAccount {
  constructor(balance = 0) {
    this.balance = balance;
  }

  deposit(amount) {
    this.balance += amount;
    return new Memento(this.balance);
  }

  restore(memento) {
    this.balance = memento.balance;
  }

  toString() {
    return `Balance: ${this.balance}`;
  }
}

```

Here, we create the BankAccount class, which represents a bank account with the ability to make deposits, save states in the form of Mementos, and restore the previous state.


**Step 3. Definition of the Cuidador class:**

```
class Caretaker {
  constructor() {
    this.mementos = [];
  }

  addMemento(memento) {
    this.mementos.push(memento);
  }

  getMemento(index) {
    return this.mementos[index];
  }
}
```

The Cuidador class is responsible for storing the Mementos in a list so that previous states can be restored when needed.

**Step 4. Using the Memento pattern:**

```
// Create an instance of BankAccount
const bankAccount = new BankAccount(100);
const caretaker = new Caretaker();

// Make deposits and save states in Mementos
caretaker.addMemento(bankAccount.deposit(50));
console.log(bankAccount.toString()); // Balance: 150

caretaker.addMemento(bankAccount.deposit(25));
console.log(bankAccount.toString()); // Balance: 175

// Restore the previous state
bankAccount.restore(caretaker.getMemento(0));
console.log(bankAccount.toString()); // Balance: 150

bankAccount.restore(caretaker.getMemento(1));
console.log(bankAccount.toString()); // Balance: 175
```

In this step, we create an instance of CuentaBanco and a Cuidador. Then, we make deposits into the bank account and save states as Mementos using the Cuidador. Finally, we restore previous states of the bank account using the Mementos and verify the resulting balances.

**Final Code:**

```
class Memento {
  constructor(balance) {
    this.balance = balance;
  }
}

class BankAccount {
  constructor(balance = 0) {
    this.balance = balance;
  }

  deposit(amount) {
    this.balance += amount;
    return new Memento(this.balance);
  }

  restore(memento) {
    this.balance = memento.balance;
  }

  toString() {
    return `Balance: ${this.balance}`;
  }
}

class Caretaker {
  constructor() {
    this.mementos = [];
  }

  addMemento(memento) {
    this.mementos.push(memento);
  }

  getMemento(index) {
    return this.mementos[index];
  }
}

// Create an instance of BankAccount
const bankAccount = new BankAccount(100);
const caretaker = new Caretaker();

// Make deposits and save states in Mementos
caretaker.addMemento(bankAccount.deposit(50));
console.log(bankAccount.toString()); // Balance: 150

caretaker.addMemento(bankAccount.deposit(25));
console.log(bankAccount.toString()); // Balance: 175

// Restore the previous state
bankAccount.restore(caretaker.getMemento(0));
console.log(bankAccount.toString()); // Balance: 150

bankAccount.restore(caretaker.getMemento(1));
console.log(bankAccount.toString()); // Balance: 175


```
