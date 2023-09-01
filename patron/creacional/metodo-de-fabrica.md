**Factory Method (método de fábrica)**

En diseño de software, el patrón de diseño Factory Method consiste en utilizar una clase constructora (al estilo del Abstract Factory) abstracta con unos cuantos métodos definidos y otro(s) abstracto(s): el dedicado a la construcción de objetos de un subtipo de un tipo determinado. Es una simplificación del Abstract Factory, en la que la clase abstracta tiene métodos concretos que usan algunos de los abstractos; según usemos una u otra hija de esta clase abstracta, tendremos uno u otro comportamiento.

**Ejemplo:**

Tomemos un ejemplo de un punto. Tenemos una clase de puntos y tenemos que crear un punto cartesiano y un punto polar. Definiremos una fábrica de Puntos que hará este trabajo.

```javascript
class Punto {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return `(${this.x}, ${this.y})`;
  }
}

class PuntoFactory {
  static crearPuntoCartesiano(x, y) {
    return new Punto(x, y);
  }

  static crearPuntoPolar(rho, theta) {
    return new Punto(rho * Math.cos(theta), rho * Math.sin(theta));
  }
}

// Ejemplo de uso
const puntoCartesiano = PuntoFactory.crearPuntoCartesiano(5, 6);
const puntoPolar = PuntoFactory.crearPuntoPolar(5, Math.PI / 2);

console.log("Punto Cartesiano:", puntoCartesiano.toString()); // Punto Cartesiano: (5, 6)
console.log("Punto Polar:", puntoPolar.toString()); // Punto Polar: (6.123233995736766e-17, 5)
