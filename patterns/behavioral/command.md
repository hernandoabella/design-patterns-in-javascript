### Command

In object-oriented programming, the Command pattern is a behavioral design pattern in which an object is used to encapsulate all the information needed to perform an action or trigger an event at a later time. This information includes the method's name, the object that owns the method, and the method's parameter values.

**Example:**

We'll take a simple example of a bank account where we issue an order to deposit or withdraw a certain amount of money.

**Step 1. Definition of the `BankAccount` class:** In this step, we define the `BankAccount` class, which represents a bank account with methods for depositing, withdrawing, and getting the balance.

```
class BankAccount {
  constructor(balance = 0) {
    this.balance = balance;
  }
  
  deposit(amount) {
    this.balance += amount;
    console.log(`${amount} deposited into the total balance ${this.balance}`);
  }
  
  withdraw(amount) {
    if (this.balance - amount >= BankAccount.overdraftLimit) {
      this.balance -= amount;
      console.log(`${amount} withdrawn from the total balance.`);
    } else {
      console.log(`Insufficient funds to withdraw ${amount}`);
    }
  }
  
  toString() {
    return `Balance: ${this.balance}`;
  }
}

BankAccount.overdraftLimit = -500;
```

**Step 2. Creating Commands:** In this step, we create an enumeration Action to represent deposit and withdraw actions, and then define the BankAccountCommand class that encapsulates an action along with its amount.

```
let Action = Object.freeze({
  deposit: 1,
  withdraw: 2,
});

class BankAccountCommand {
  constructor(account, action, amount) {
    this.account = account;
    this.action = action;
    this.amount = amount;
  }
  
  execute() {
    switch (this.action) {
      case Action.deposit:
        this.account.deposit(this.amount);
        break;
      case Action.withdraw:
        this.account.withdraw(this.amount);
        break;
    }
  }
  
  undo() {
    switch (this.action) {
      case Action.deposit:
        this.account.withdraw(this.amount); // Reversing a deposit is a withdrawal
        break;
      case Action.withdraw:
        this.account.deposit(this.amount); // Reversing a withdrawal is a deposit
        break;
    }
  }
}

```

**Step 3. Using the Command Pattern:** In this step, we create an instance of BankAccount and a command to deposit and then undo that deposit.

```
let bankAccount = new BankAccount(100);
let cmd = new BankAccountCommand(bankAccount, Action.deposit, 50);

cmd.execute(); // Perform a deposit of 50
console.log(bankAccount.toString()); // Balance: 150

cmd.undo(); // Undo the deposit of 50
console.log(bankAccount.toString()); // Balance: 100
```

This code demonstrates how the Command pattern allows encapsulating requests as objects, making it easy to execute and undo actions.

**Final Code:** 

```
class BankAccount {
  constructor(balance = 0) {
    this.balance = balance;
  }
  
  deposit(amount) {
    this.balance += amount;
    console.log(`${amount} deposited into the total balance ${this.balance}`);
  }
  
  withdraw(amount) {
    if (this.balance - amount >= BankAccount.overdraftLimit) {
      this.balance -= amount;
      console.log(`${amount} withdrawn from the total balance.`);
    } else {
      console.log(`Insufficient funds to withdraw ${amount}`);
    }
  }
  
  toString() {
    return `Balance: ${this.balance}`;
  }
}

BankAccount.overdraftLimit = -500;

let Action = Object.freeze({
  deposit: 1,
  withdraw: 2,
});

class BankAccountCommand {
  constructor(account, action, amount) {
    this.account = account;
    this.action = action;
    this.amount = amount;
  }
  
  execute() {
    switch (this.action) {
      case Action.deposit:
        this.account.deposit(this.amount);
        break;
      case Action.withdraw:
        this.account.withdraw(this.amount);
        break;
    }
  }
  
  undo() {
    switch (this.action) {
      case Action.deposit:
        this.account.withdraw(this.amount); // Reversing a deposit is a withdrawal
        break;
      case Action.withdraw:
        this.account.deposit(this.amount); // Reversing a withdrawal is a deposit
        break;
    }
  }
}

let bankAccount = new BankAccount(100);
let cmd = new BankAccountCommand(bankAccount, Action.deposit, 50);

cmd.execute(); // Perform a deposit of 50
console.log(bankAccount.toString()); // Balance: 150

cmd.undo(); // Undo the deposit of 50
console.log(bankAccount.toString()); // Balance: 100
```