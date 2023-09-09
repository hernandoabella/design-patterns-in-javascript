### Responsibility Chain


Create a chain of objects. Starting from a point, it stops until a certain condition is met.

In object-oriented design, the Chain of Responsibility pattern is a design pattern consisting of a source of command objects and a series of processing objects.

**Example:**

Let's use an example of a game that has a creature. The creature will increase its defense and attack when it reaches a certain point. It will create a chain, and the attack and defense will increase and decrease.

**Paso 1. Definición de las clases clave y el patrón Cadena de Responsabilidad:** En este paso, definimos las clases principales, incluyendo Creatura y ModificadorCreatura, así como las clases de modificadores específicos.

```
class Creatura {
  constructor(nombre, ataque, defensa) {
    this.nombre = nombre;
    this.ataque = ataque;
    this.defensa = defensa;
  }

  toString() {
    return `${this.nombre} (${this.ataque} / ${this.defensa})`;
  }
}

class ModificadorCreatura {
  constructor(creatura) {
    this.creatura = creatura;
    this.siguiente = null;
  }

  agregar(modificador) {
    if (this.siguiente) this.siguiente.agregar(modificador);
    else this.siguiente = modificador;
  }

  manejar() {
    if (this.siguiente) this.siguiente.manejar();
  }
}
```

**Paso 2. Implementación de los modificadores específicos:** Creamos los modificadores específicos, como ModificadorSinBonificaciones, ModificadorDobleAtaque, y ModificadorAumentarDefensa.

```
class ModificadorSinBonificaciones extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }

  manejar() {
    console.log("¡No hay bonificaciones para ti!");
  }
}

class ModificadorDobleAtaque extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }

  manejar() {
    console.log(`Doblando ataque de ${this.creatura.nombre}`);
    this.creatura.ataque *= 2;
    super.manejar();
  }
}

class ModificadorAumentarDefensa extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }

  manejar() {
    if (this.creatura.ataque <= 2) {
      console.log(`Incrementando defensa de ${this.creatura.nombre}`);
      this.creatura.defensa++;
    }
    super.manejar();
  }
}
```

**Paso 3. Uso del patrón Cadena de Responsabilidad:** En este paso, creamos una instancia de Creatura, luego creamos una cadena de responsabilidad de modificadores y la aplicamos a la criatura.

```
let picachu = new Creatura("Picachu", 1, 1);
console.log(picachu.toString());

let raiz = new ModificadorCreatura(picachu);
raiz.agregar(new ModificadorSinBonificaciones(picachu));
raiz.agregar(new ModificadorAumentarDefensa(picachu));
raiz.manejar();

console.log(picachu.toString());
```

Este código final combina todos los pasos y muestra la salida esperada cuando se ejecuta.

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
