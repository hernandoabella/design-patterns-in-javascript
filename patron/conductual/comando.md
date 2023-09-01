### Command (Comando)

En la programación orientada a objetos, el patrón de comando es un patrón de diseño de comportamiento en el que se utiliza un objeto para encapsular toda la información necesaria para realizar una acción o desencadenar un evento en un momento posterior. Esta información incluye el nombre del método, el objeto que posee el método y los valores de los parámetros del método.

### Ejemplo:

Estaremos tomando un ejemplo sencillo de una cuenta bancaria en la que damos una orden si tenemos que depositar o retirar una determinada cantidad de dinero.

```
class CuentaBanco {
  constructor(balance = 0) {
    this.balance = balance;
  }
  
  deposito(cantidad) {
    this.balance += cantidad;
    console.log(`${cantidad} depositado al balance total ${total.balance}`);
  }
  
  retirar(cantidad) {
    if(this.balance - cantidad >= CuentaBanco.limiteDescubierto) {
      this.balance -= cantidad;
      console.log('retirar');
    }
  }
  
  toString() {
    return `Balance ${this.balance}`;
  }
}

CuentaBanco.limiteDescubierto = -500;
```

Creando nuestros comandos,

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
    switch(this.accion) {
      case Accion.deposito:
        this.cuenta.deposito(this.cantidad);
        break;
      case Accion.retirar(this.cantidad);
        break;
    }
  }
  
  undo() {
    switch(this.accion) {
      case Accion.deposito:
        this.cuenta.deposito(this.cantidad);
        break;
      case Accion.retirar:
        this.cuenta.deposito(this.cantidad);
        break;
    }
  }
}
```

Así es como usaremos esto,


```
let cuentaBancaria = new CuentaBanco(100);
let cmd = new ComandoCuentaBanco(cuentaBancaria, Accion.deposito, 50);

cmd.llamar();
console.log(cuentaBancaria.toString());

cmd.undo();
console.log(cuentaBancaria.toString());
```