### Responsibility Chain


Create a chain of objects. Starting from a point, it stops until a certain condition is met.

In object-oriented design, the Chain of Responsibility pattern is a design pattern consisting of a source of command objects and a series of processing objects.

**Example:**

Let's use an example of a game that has a creature. The creature will increase its defense and attack when it reaches a certain point. It will create a chain, and the attack and defense will increase and decrease.

**Step 1. Definition of Key Classes and the Chain of Responsibility Pattern:** In this step, we define the main classes, including Creature and CreatureModifier, as well as specific modifier classes.

```
class Creature {
  constructor(name, attack, defense) {
    this.name = name;
    this.attack = attack;
    this.defense = defense;
  }

  toString() {
    return `${this.name} (${this.attack} / ${this.defense})`;
  }
}

class CreatureModifier {
  constructor(creature) {
    this.creature = creature;
    this.next = null;
  }

  add(modifier) {
    if (this.next) this.next.add(modifier);
    else this.next = modifier;
  }

  handle() {
    if (this.next) this.next.handle();
  }
}
```

**Step 2. Implementation of Specific Modifiers:** We create specific modifiers such as NoBonusesModifier, DoubleAttackModifier, and IncreaseDefenseModifier.

```
class NoBonusesModifier extends CreatureModifier {
  constructor(creature) {
    super(creature);
  }

  handle() {
    console.log("No bonuses for you!");
  }
}

class DoubleAttackModifier extends CreatureModifier {
  constructor(creature) {
    super(creature);
  }

  handle() {
    console.log(`Doubling attack of ${this.creature.name}`);
    this.creature.attack *= 2;
    super.handle();
  }
}

class IncreaseDefenseModifier extends CreatureModifier {
  constructor(creature) {
    super(creature);
  }

  handle() {
    if (this.creature.attack <= 2) {
      console.log(`Increasing defense of ${this.creature.name}`);
      this.creature.defense++;
    }
    super.handle();
  }
}

```

**Step 3. Using the Chain of Responsibility Pattern:** In this step, we create an instance of Creature, then create a chain of responsibility of modifiers and apply it to the creature.

```
let pikachu = new Creature("Pikachu", 1, 1);
console.log(pikachu.toString());

let root = new CreatureModifier(pikachu);
root.add(new NoBonusesModifier(pikachu));
root.add(new IncreaseDefenseModifier(pikachu));
root.handle();

console.log(pikachu.toString());
```

This final code combines all the steps and shows the expected output when executed.

**Código final:**

```
class Creature {
  constructor(name, attack, defense) {
    this.name = name;
    this.attack = attack;
    this.defense = defense;
  }

  toString() {
    return `${this.name} (${this.attack} / ${this.defense})`;
  }
}

class CreatureModifier {
  constructor(creature) {
    this.creature = creature;
    this.next = null;
  }

  add(modifier) {
    if (this.next) this.next.add(modifier);
    else this.next = modifier;
  }

  handle() {
    if (this.next) this.next.handle();
  }
}

class NoBonusesModifier extends CreatureModifier {
  constructor(creature) {
    super(creature);
  }

  handle() {
    console.log("No bonuses for you!");
  }
}

class DoubleAttackModifier extends CreatureModifier {
  constructor(creature) {
    super(creature);
  }

  handle() {
    console.log(`Doubling attack of ${this.creature.name}`);
    this.creature.attack *= 2;
    super.handle();
  }
}

class IncreaseDefenseModifier extends CreatureModifier {
  constructor(creature) {
    super(creature);
  }

  handle() {
    if (this.creature.attack <= 2) {
      console.log(`Increasing defense of ${this.creature.name}`);
      this.creature.defense++;
    }
    super.handle();
  }
}

// Create a creature and show its initial state
let pikachu = new Creature("Pikachu", 1, 1);
console.log(pikachu.toString());

// Create a chain of responsibility and add modifiers
let root = new CreatureModifier(pikachu);
root.add(new NoBonusesModifier(pikachu));
root.add(new IncreaseDefenseModifier(pikachu));

// Apply the modifiers to the creature
root.handle();

// Show the final state of the creature after applying modifiers
console.log(pikachu.toString());

// Expected Output:
// Pikachu (1 / 1)
// Increasing defense of Pikachu
// Pikachu (1 / 2)
```
