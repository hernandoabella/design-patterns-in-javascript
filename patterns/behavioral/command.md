### Command (Comando)

En la programación orientada a objetos, el patrón de comando es un patrón de diseño de comportamiento en el que se utiliza un objeto para encapsular toda la información necesaria para realizar una acción o desencadenar un evento en un momento posterior. Esta información incluye el nombre del método, el objeto que posee el método y los valores de los parámetros del método.

**Ejemplo:**

Estaremos tomando un ejemplo sencillo de una cuenta bancaria en la que damos una orden si tenemos que depositar o retirar una determinada cantidad de dinero.

**Paso 1. Definición de la clase CuentaBanco:** En este paso, definimos la clase CuentaBanco, que representa una cuenta bancaria con métodos para depositar, retirar y obtener el saldo.

```
class CuentaBanco {
  constructor(balance = 0) {
    this.balance = balance;
  }
  
  deposito(cantidad) {
    this.balance += cantidad;
    console.log(`${cantidad} depositado en el saldo total ${this.balance}`);
  }
  
  retirar(cantidad) {
    if (this.balance - cantidad >= CuentaBanco.limiteDescubierto) {
      this.balance -= cantidad;
      console.log(`Se retiraron ${cantidad} del saldo total.`);
    } else {
      console.log(`Fondos insuficientes para retirar ${cantidad}`);
    }
  }
  
  toString() {
    return `Saldo: ${this.balance}`;
  }
}

CuentaBanco.limiteDescubierto = -500;
```

**Paso 2. Creación de comandos:** En este paso, creamos una enumeración Accion para representar las acciones de depósito y retiro, y luego definimos la clase ComandoCuentaBanco que encapsula una acción junto con su cantidad.

```
let Accion = Object.freeze({
  deposito: 1,
  retirar: 2,
});

class ComandoCuentaBanco {
  constructor(cuenta, accion, cantidad) {
    this.cuenta = cuenta;
    this.accion = accion;
    this.cantidad = cantidad;
  }
  
  llamar() {
    switch (this.accion) {
      case Accion.deposito:
        this.cuenta.deposito(this.cantidad);
        break;
      case Accion.retirar:
        this.cuenta.retirar(this.cantidad);
        break;
    }
  }
  
  undo() {
    switch (this.accion) {
      case Accion.deposito:
        this.cuenta.retirar(this.cantidad); // Revertir un depósito es retirar
        break;
      case Accion.retirar:
        this.cuenta.deposito(this.cantidad); // Revertir un retiro es depositar
        break;
    }
  }
}
```

**Paso 3. Uso del patrón Command:** En este paso, creamos una instancia de CuentaBanco y un comando para depositar y luego deshacer ese depósito.

```
let cuentaBancaria = new CuentaBanco(100);
let cmd = new ComandoCuentaBanco(cuentaBancaria, Accion.deposito, 50);

cmd.llamar(); // Realizar un depósito de 50
console.log(cuentaBancaria.toString()); // Saldo: 150

cmd.undo(); // Deshacer el depósito de 50
console.log(cuentaBancaria.toString()); // Saldo: 100\
```

Este código muestra cómo el patrón Command permite encapsular solicitudes como objetos, lo que facilita la ejecución y reversión de acciones.

**Código final:** 

```
class CuentaBanco {
  constructor(balance = 0) {
    this.balance = balance;
  }
  
  deposito(cantidad) {
    this.balance += cantidad;
    console.log(`${cantidad} depositado en el saldo total ${this.balance}`);
  }
  
  retirar(cantidad) {
    if (this.balance - cantidad >= CuentaBanco.limiteDescubierto) {
      this.balance -= cantidad;
      console.log(`Se retiraron ${cantidad} del saldo total.`);
    } else {
      console.log(`Fondos insuficientes para retirar ${cantidad}`);
    }
  }
  
  toString() {
    return `Saldo: ${this.balance}`;
  }
}

CuentaBanco.limiteDescubierto = -500;

let Accion = Object.freeze({
  deposito: 1,
  retirar: 2,
});

class ComandoCuentaBanco {
  constructor(cuenta, accion, cantidad) {
    this.cuenta = cuenta;
    this.accion = accion;
    this.cantidad = cantidad;
  }
  
  llamar() {
    switch (this.accion) {
      case Accion.deposito:
        this.cuenta.deposito(this.cantidad);
        break;
      case Accion.retirar:
        this.cuenta.retirar(this.cantidad);
        break;
    }
  }
  
  undo() {
    switch (this.accion) {
      case Accion.deposito:
        this.cuenta.retirar(this.cantidad); // Revertir un depósito es retirar
        break;
      case Accion.retirar:
        this.cuenta.deposito(this.cantidad); // Revertir un retiro es depositar
        break;
    }
  }
}

let cuentaBancaria = new CuentaBanco(100);
let cmd = new ComandoCuentaBanco(cuentaBancaria, Accion.deposito, 50);

cmd.llamar(); // Realizar un depósito de 50
console.log(cuentaBancaria.toString()); // Saldo: 150

cmd.undo(); // Deshacer el depósito de 50
console.log(cuentaBancaria.toString()); // Saldo: 100

```