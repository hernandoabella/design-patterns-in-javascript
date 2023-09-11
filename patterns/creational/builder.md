### Constructor

Builds complex objects from simple objects.

The constructor pattern is a design pattern designed to provide a flexible solution to various object creation problems in object-oriented programming.

**Example:**

Let's use an example of a Person class to store information about a person.

**Step 1. Definition of the Person Class:** In this step, we define the Person class, which is the class we want to build in a structured way. The Person class has several properties like addressStreet, postalCode, city, companyName, position, and annualIncome, which store information about a person. It also has a toString() method that returns a readable string representation of the person's information.

```
class Person {
  constructor() {
    this.addressStreet = this.postalCode = this.city = "";
    this.companyName = this.position = "";
    this.annualIncome = 0;
  }

  toString() {
    return (
      `Person lives at
      ${this.addressStreet}, ${this.city}, ${this.postalCode}
      and works at ${this.companyName} as
      ${this.position} earning ${this.annualIncome}`
    );
  }
}
```

In this step, we have created the Person class with a constructor that initializes the properties and a toString() method to obtain a readable representation of the person.


**Step 2. Creating Constructors:** In this step, we create three related constructors: PersonBuilder, WorkPersonBuilder, and AddressPersonBuilder.

PersonBuilder: This is the main constructor used to build Person objects. It has two methods, lives and works, to specify the person's address and job. The build() method finalizes the construction and returns the built Person object.

WorkPersonBuilder: Extends PersonBuilder and is used to specify the person's job. It has methods like at, asA, and earning to define the company name, position, and annual income of the person.

AddressPersonBuilder: Also extends PersonBuilder and is used to specify the person's address. It has methods like at, withPostcode, and in to define the address, postal code, and city.

```
class PersonBuilder {
  constructor(person = new Person()) {
    this.person = person;
  }

  get lives() {
    return new AddressPersonBuilder(this.person);
  }

  get works() {
    return new WorkPersonBuilder(this.person);
  }

  build() {
    return this.person;
  }
}

class WorkPersonBuilder extends PersonBuilder {
  constructor(person) {
    super(person);
  }

  at(companyName) {
    this.person.companyName = companyName;
    return this;
  }

  asA(position) {
    this.person.position = position;
    return this;
  }

  earning(annualIncome) {
    this.person.annualIncome = annualIncome;
    return this;
  }
}

class AddressPersonBuilder extends PersonBuilder {
  constructor(person) {
    super(person);
  }

  at(addressStreet) {
    this.person.addressStreet = addressStreet;
    return this;
  }

  withPostcode(postalCode) {
    this.person.postalCode = postalCode;
    return this;
  }

  in(city) {
    this.person.city = city;
    return this;
  }
}

```

**Step 3. Using the Constructor:** In this step, we create an instance of PersonBuilder called personBuilder. Then, we use a method chain to build a Person instance in a structured way.

```
let personBuilder = new PersonBuilder();
let person = personBuilder.lives
  .at("123 Main Street")
  .in("New York")
  .withPostcode("10001")
  .works.at("ABC Inc.")
  .asA("Engineer")
  .earning(80000)
  .build();
```

**Step 4. Result and Output:** Finally, we can print the information of the built person using the toString() method of the Person class.

```
console.log(person.toString());
```

The expected output will be a string representation of the person's information, including details of address and job:

Person lives at
123 Main Street, New York, 10001
and works at ABC Inc. as
Engineer earning 80000

**Final Code:**

```
// Definition of the Person class to store personal and job-related information
class Person {
  constructor() {
    this.addressStreet = this.postalCode = this.city = "";
    this.companyName = this.position = "";
    this.annualIncome = 0;
  }

  toString() {
    return (
      `Person lives at
      ${this.addressStreet}, ${this.city}, ${this.postalCode}
      and works at ${this.companyName} as
      ${this.position} earning ${this.annualIncome}`
    );
  }
}

// Base class PersonBuilder to build Person objects
class PersonBuilder {
  constructor(person = new Person()) {
    this.person = person;
  }

  get lives() {
    return new AddressPersonBuilder(this.person);
  }

  get works() {
    return new WorkPersonBuilder(this.person);
  }

  build() {
    return this.person;
  }
}

// Constructor for Person's job details
class WorkPersonBuilder extends PersonBuilder {
  constructor(person) {
    super(person);
  }

  at(companyName) {
    this.person.companyName = companyName;
    return this;
  }

  asA(position) {
    this.person.position = position;
    return this;
  }

  earning(annualIncome) {
    this.person.annualIncome = annualIncome;
    return this;
  }
}

// Constructor for Person's address details
class AddressPersonBuilder extends PersonBuilder {
  constructor(person) {
    super(person);
  }

  at(addressStreet) {
    this.person.addressStreet = addressStreet;
    return this;
  }

  withPostcode(postalCode) {
    this.person.postalCode = postalCode;
    return this;
  }

  in(city) {
    this.person.city = city;
    return this;
  }
}

// Using the constructor pattern to create a Person object in a structured way
let personBuilder = new PersonBuilder();
let person = personBuilder.lives
  .at("123 Main Street")
  .in("New York")
  .withPostcode("10001")
  .works.at("ABC Inc.")
  .asA("Engineer")
  .earning(80000)
  .build();

// Printing the details of the created Person
console.log(person.toString());

/*
Expected Output:
Person lives at
123 Main Street, New York, 10001
and works at ABC Inc. as
Engineer earning 80000
*/
```
