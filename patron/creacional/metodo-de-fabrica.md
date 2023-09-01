### Factory Method (método de fábrica)

En diseño de software, el patrón de diseño Factory Method consiste en utilizar una clase constructora (al estilo del Abstract Factory) abstracta con unos cuantos métodos definidos y otro(s) abstracto(s): el dedicado a la construcción de objetos de un subtipo de un tipo determinado. Es una simplificación del Abstract Factory, en la que la clase abstracta tiene métodos concretos que usan algunos de los abstractos; según usemos una u otra hija de esta clase abstracta, tendremos uno u otro comportamiento.

### Ejemplo:

Tomemos un ejemplo de un punto. Tenemos una clase de puntos y tenemos que crear un punto cartesiano y un punto polar. Definiremos una fábrica de Puntos que hará este trabajo.

```
SistemaCoordenadas = {
  CARTESIANO: 0,
  POLARES: 1,
}

class Punto{
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  
  static get factory() {
    return new PuntoFactory();
  }
}
```

Ahora crearemos una clase PuntoFactory y usaremos nuestra fábrica ahora,

```
class PuntoFactory {

  static nuevoPuntoCartesiano(x, y) {
    return new Punto(x, y);
  }
  
  static nuevoPuntoPolar(rho, theta) {
    return new Punto(rho * Math.cos(theta), rho * Math.sin(theta));
  }
}

// Así es como usaremos esta clase

let punto = PuntoFactory.nuevoPuntoPolar(5, Math.Pi/2);
let punto2 = PuntoFactory.nuevoPuntoCartesiano(5, 6);
console.log(punto);
console.log(punto2);
```