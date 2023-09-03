### Composite

The Composite pattern is used to compose objects into tree structures to represent object hierarchies. This allows individual objects and compositions of objects to be treated in the same way, simplifying their manipulation.

**Example:**

**1. Class Definitions:** In this example, we create two classes: Employee to represent individual employees and EmployeeGroup to represent groups of employees.

```
class Employee {
  constructor(name, role) {
    this.name = name;
    this.role = role;
  }

  print() {
    console.log("Name: " + this.name + ", Role: " + this.role);
  }
}

class EmployeeGroup {
  constructor(name, composite = []) {
    this.name = name;
    this.composite = composite;
  }

  print() {
    console.log("Group: " + this.name);
    this.composite.forEach(emp => {
      emp.print();
    })
  }
}
```

**2. Creating Employees and Groups:** We create instances of individual employees and then group them into an EmployeeGroup.

```
// Creating individual employees
let hernando = new Employee("Hernando", "Developer");
let albert = new Employee("Albert", "Developer");

// Creating an employee group and adding individual employees
let developerGroup = new EmployeeGroup("Developers", [hernando, albert]);
```

**3. Printing the Hierarchical Structure:** We use the print() method to display the hierarchical structure, which includes both individual employees and employee groups.

```
// Print the hierarchical structure
developerGroup.print();
```

**Final Code:**

```
class Employee {
  constructor(name, role) {
    this.name = name;
    this.role = role;
  }

  print() {
    console.log(`Name: ${this.name}, Role: ${this.role}`);
  }
}

class EmployeeGroup {
  constructor(name, composite = []) {
    this.name = name;
    this.composite = composite;
  }

  print() {
    console.log(`Group: ${this.name}`);
    this.composite.forEach(emp => {
      emp.print();
    })
  }
}

// Creating individual employees
let hernando = new Employee("Hernando", "Developer");
let albert = new Employee("Albert", "Developer");

// Creating an employee group and adding individual employees
let developerGroup = new EmployeeGroup("Developers", [hernando, albert]);

// Print the hierarchical structure
developerGroup.print();
// Expected Output:
// Group: Developers
// Name: Hernando, Role: Developer
// Name: Albert, Role: Developer
```
