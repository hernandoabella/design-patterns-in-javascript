### Memento

Memento restaura un objeto a su estado anterior.

El patrón memento es un patrón de diseño de software que brinda la capacidad de restaurar un objeto a su estado anterior. El patrón memento se implementa con tres objetos: el originador, un cuidador y un recuerdo.

### Ejemplo:

Estaremos tomando un ejemplo de una cuenta bancaria en la que almacenamos nuestro estado anterior y tendrá la funcionalidad de deshacer.

**Paso 1. Definición de la clase Memento:**

```
class Memento {
  constructor(balance) {
    this.balance = balance;
  }
}
```

En este paso, creamos la clase Memento, que se utilizará para almacenar el estado de la cuenta bancaria en un momento dado.

**Paso 2. Definición de la clase CuentaBanco:**

```
class CuentaBanco {
  constructor(balance = 0) {
    this.balance = balance;
  }

  deposito(cantidad) {
    this.balance += cantidad;
    return new Memento(this.balance);
  }

  restaurar(m) {
    this.balance = m.balance;
  }

  toString() {
    return `Balance: ${this.balance}`;
  }
}
```

Aquí creamos la clase CuentaBanco, que representa una cuenta bancaria con la capacidad de realizar depósitos, guardar estados en forma de Mementos y restaurar el estado anterior.

**Paso 3. Definición de la clase Cuidador:**

```
class Cuidador {
  constructor() {
    this.mementos = [];
  }

  agregarMemento(memento) {
    this.mementos.push(memento);
  }

  obtenerMemento(index) {
    return this.mementos[index];
  }
}
```

La clase Cuidador es responsable de almacenar los Mementos en una lista para que se puedan restaurar estados anteriores cuando sea necesario.

**Paso 4. Uso del patrón Memento**

```
// Crear una instancia de CuentaBanco
const cuentaBancaria = new CuentaBanco(100);
const cuidador = new Cuidador();

// Realizar depósitos y guardar estados en Mementos
cuidador.agregarMemento(cuentaBancaria.deposito(50));
console.log(cuentaBancaria.toString()); // Saldo: 150

cuidador.agregarMemento(cuentaBancaria.deposito(25));
console.log(cuentaBancaria.toString()); // Saldo: 175

// Restaurar estado anterior
cuentaBancaria.restaurar(cuidador.obtenerMemento(0));
console.log(cuentaBancaria.toString()); // Saldo: 150

cuentaBancaria.restaurar(cuidador.obtenerMemento(1));
console.log(cuentaBancaria.toString()); // Saldo: 175
```

En este paso, creamos una instancia de CuentaBanco y un Cuidador. Luego, realizamos depósitos en la cuenta bancaria y guardamos estados en forma de Mementos utilizando el Cuidador. Finalmente, restauramos estados anteriores de la cuenta bancaria usando los Mementos y verificamos los saldos resultantes.

**Código final:**

```
class Memento {
  constructor(balance) {
    this.balance = balance;
  }
}

class CuentaBanco {
  constructor(balance = 0) {
    this.balance = balance;
  }

  deposito(cantidad) {
    this.balance += cantidad;
    return new Memento(this.balance);
  }

  restaurar(m) {
    this.balance = m.balance;
  }

  toString() {
    return `Balance: ${this.balance}`;
  }
}

class Cuidador {
  constructor() {
    this.mementos = [];
  }

  agregarMemento(memento) {
    this.mementos.push(memento);
  }

  obtenerMemento(index) {
    return this.mementos[index];
  }
}

// Crear una instancia de CuentaBanco
const cuentaBancaria = new CuentaBanco(100);
const cuidador = new Cuidador();

// Realizar depósitos y guardar estados en Mementos
cuidador.agregarMemento(cuentaBancaria.deposito(50));
console.log(cuentaBancaria.toString()); // Saldo: 150

cuidador.agregarMemento(cuentaBancaria.deposito(25));
console.log(cuentaBancaria.toString()); // Saldo: 175

// Restaurar estado anterior
cuentaBancaria.restaurar(cuidador.obtenerMemento(0));
console.log(cuentaBancaria.toString()); // Saldo: 150

cuentaBancaria.restaurar(cuidador.obtenerMemento(1));
console.log(cuentaBancaria.toString()); // Saldo: 175

```
