### Memento

Memento restaura un objeto a su estado anterior.

El patrón memento es un patrón de diseño de software que brinda la capacidad de restaurar un objeto a su estado anterior. El patrón memento se implementa con tres objetos: el originador, un cuidador y un recuerdo.

### Ejemplo:

Estaremos tomando un ejemplo de una cuenta bancaria en la que almacenamos nuestro estado anterior y tendrá la funcionalidad de deshacer.

```
class Memento {
  constructor(balance) {
    this.balance = balance;
  }
}

// Agregando cuenta de banco
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