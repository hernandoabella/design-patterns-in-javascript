# Creational Design Patterns

Creational design patterns focus on how objects are created, providing solutions for instantiating objects appropriately for the situation. They address design and complexity problems that can arise when creating objects in the most basic form. These patterns solve these problems by controlling the object creation in some way.

Below are the most common creational design patterns in JavaScript:

## 1. Factory Method

The **Factory Method** provides an interface for creating objects, allowing subclasses to alter the type of objects that will be created. It's useful when flexible and adaptable creation logic is needed.

- [Learn more about the Factory Method](/patterns/creational/factory-method.md)

## 2. Abstract Factory

The **Abstract Factory** pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes. This promotes the creation of consistent and compatible objects.

- [Learn more about the Abstract Factory](/patterns/creational/abstract-factory.md)

## 3. Builder

The **Builder** pattern is used to construct an object step by step. It allows the creation of complex objects by specifying their type and content incrementally.

- [Learn more about the Builder](/patterns/creational/builder.md)

## 4. Prototype

The **Prototype** focuses on creating new objects by copying an existing object, called a prototype. It's useful when creating an object is more efficient by duplicating an existing object rather than building it from scratch.

- [Learn more about the Prototype](/patterns/creational/prototype.md)

## 5. Singleton

The **Singleton** pattern ensures that a class has a single instance and provides a global point of access to that instance. It is used when a single instance of a class needs to coordinate actions throughout the system.

- [Learn more about the Singleton](/patterns/creational/singleton.md)

These creational patterns are valuable tools for addressing object creation problems efficiently and structuredly in JavaScript projects. Each one has its specific purpose and application, making them essential resources in software design.
