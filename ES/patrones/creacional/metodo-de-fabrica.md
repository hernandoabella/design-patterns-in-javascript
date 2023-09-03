### Factory Method (Método de Fábrica)

El patrón de diseño Factory Method es una técnica en el diseño de software que se basa en la creación de objetos de un subtipo específico a través de una interfaz común. Este patrón se logra mediante el uso de una clase constructora abstracta que contiene métodos concretos y métodos abstractos. Los métodos concretos se encargan de la creación de objetos, mientras que los métodos abstractos son implementados por subclases concretas. Dependiendo de la subclase utilizada, se obtiene un comportamiento específico.

**Ejemplo:**

Para comprender mejor el Factory Method, consideremos un ejemplo concreto relacionado con la creación de puntos en un plano bidimensional. Imaginemos que estamos desarrollando una aplicación que necesita trabajar con puntos en coordenadas cartesianas y polares.

Primero, creamos una clase llamada Punto que representa un punto en el plano. Esta clase tiene un constructor que toma las coordenadas x e y, y un método toString() que devuelve una representación legible del punto en formato (x, y).

**Paso 1. Definición de la clase Punto que representa un punto en el plano:**

```
// Clase Punto que representa un punto en el plano
class Punto {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  // Método para obtener una representación legible del punto
  toString() {
    return `(${this.x}, ${this.y})`;
  }
}

```

En este paso, hemos creado la clase Punto con un constructor que toma las coordenadas x e y y un método toString() para obtener una representación legible del punto.

**Paso 2. Implementación del Factory Method en la clase PuntoFactory:**

```
// Clase PuntoFactory que implementa el Factory Method
class PuntoFactory {
  // Método para crear un punto en coordenadas cartesianas
  static crearPuntoCartesiano(x, y) {
    return new Punto(x, y);
  }

  // Método para crear un punto en coordenadas polares
  static crearPuntoPolar(rho, theta) {
    return new Punto(rho * Math.cos(theta), rho * Math.sin(theta));
  }
}

```

En este paso, hemos creado la clase PuntoFactory que implementa el Factory Method. Esta clase contiene dos métodos estáticos: crearPuntoCartesiano y crearPuntoPolar. El primero crea un punto en coordenadas cartesianas y el segundo crea un punto en coordenadas polares.

**Paso 3. Ejemplo de uso del Factory Method:**

```
// Ejemplo de uso del Factory Method
const puntoCartesiano = PuntoFactory.crearPuntoCartesiano(5, 6);
const puntoPolar = PuntoFactory.crearPuntoPolar(5, Math.PI / 2);
```

En este paso, hemos creado dos puntos utilizando la PuntoFactory. Uno se crea en coordenadas cartesianas con crearPuntoCartesiano, y el otro se crea en coordenadas polares con crearPuntoPolar.

**Paso 4. Impresión de los puntos creados:**

```
// Impresión de los puntos creados
console.log("Punto Cartesiano:", puntoCartesiano.toString()); // Punto Cartesiano: (5, 6)
console.log("Punto Polar:", puntoPolar.toString()); // Punto Polar: (6.123233995736766e-17, 5)

```

En este último paso, hemos impreso los puntos creados para verificar el resultado.

**Código final:**

```
// Clase Punto que representa un punto en el plano
class Punto {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  // Método para obtener una representación legible del punto
  toString() {
    return `(${this.x}, ${this.y})`;
  }
}

// Clase PuntoFactory que implementa el Factory Method
class PuntoFactory {
  // Método para crear un punto en coordenadas cartesianas
  static crearPuntoCartesiano(x, y) {
    return new Punto(x, y);
  }

  // Método para crear un punto en coordenadas polares
  static crearPuntoPolar(rho, theta) {
    return new Punto(rho * Math.cos(theta), rho * Math.sin(theta));
  }
}

// Ejemplo de uso del Factory Method
const puntoCartesiano = PuntoFactory.crearPuntoCartesiano(5, 6);
const puntoPolar = PuntoFactory.crearPuntoPolar(5, Math.PI / 2);

// Impresión de los puntos creados
console.log("Punto Cartesiano:", puntoCartesiano.toString()); // Punto Cartesiano: (5, 6)
console.log("Punto Polar:", puntoPolar.toString()); // Punto Polar: (6.123233995736766e-17, 5)
```