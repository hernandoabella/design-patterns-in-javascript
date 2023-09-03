### Método de plantilla

Define el esqueleto de un algoritmo como una clase abstracta, cómo debe realizarse.

Template Method (método de plantilla) es un método en una superclase, generalmente una superclase abstracta, y define el esqueleto de una operación en términos de una serie de pasos de alto nivel.

**Ejemplo:**

Tomaremos un ejemplo de un juego de ajedrez.

El patrón Template Method (Método de Plantilla) es un patrón de diseño que define el esqueleto de un algoritmo en una superclase, pero permite que las subclases implementen ciertos pasos del algoritmo sin cambiar su estructura general. Aquí está el código paso a paso:

**Paso 1:** Creamos la clase base Juego que servirá como el esqueleto del juego y define el flujo general del juego.

```
class Juego {
  constructor(numeroJugadores) {
    this.numeroDeJugadores = numeroJugadores;
    this.jugadorActual = 0;
  }
  
  ejecutar() {
    this.iniciar();
    while (!this.hayaGanador) {
      this.tomarTurno();
    }
    console.log(`Jugador ${this.jugadorGanador} gana.`);
  }
  
  iniciar() {}
  get hayaGanador() {}
  tomarTurno() {}
  get jugadorGanador() {}
}
```

**Paso 2:** Creamos la clase Ajedrez que hereda de Juego y personaliza los detalles específicos del juego de ajedrez, como el número de jugadores y el número máximo de turnos.

```
class Ajedrez extends Juego {
  constructor() {
    super(2);
    this.turnosMaximos = 10;
    this.turno = 1;
  }
  
  iniciar() {
    console.log(`Iniciando un juego de ajedrez con ${this.numeroDeJugadores} jugadores.`);
  }
  
  get hayaGanador() {
    return this.turno > this.turnosMaximos;
  }
  
  tomarTurno() {
    console.log(`Turno ${this.turno} tomado por jugador ${this.jugadorActual}`);
    this.jugadorActual = (this.jugadorActual + 1) % this.numeroDeJugadores;
    this.turno++;
  }
  
  get jugadorGanador() {
    return this.jugadorActual;
  }
}
```

**Paso 3:** Creamos una instancia de la clase Ajedrez y ejecutamos el juego llamando al método ejecutar.

```
let ajedrez = new Ajedrez();
ajedrez.ejecutar();
```

Este ejemplo muestra cómo se utiliza el patrón de método de plantilla para definir el flujo general del juego en la clase base Juego y cómo se personalizan los detalles específicos del juego en la clase Ajedrez.


**Código final:**

```
class Juego {
  constructor(numeroJugadores) {
    this.numeroDeJugadores = numeroJugadores;
    this.jugadorActual = 0;
  }
  
  ejecutar() {
    this.iniciar();
    while (!this.hayaGanador) {
      this.tomarTurno();
    }
    console.log(`Jugador ${this.jugadorGanador} gana.`);
  }
  
  iniciar() {}
  get hayaGanador() {}
  tomarTurno() {}
  get jugadorGanador() {}
}

class Ajedrez extends Juego {
  constructor() {
    super(2);
    this.turnosMaximos = 10;
    this.turno = 1;
  }
  
  iniciar() {
    console.log(`Iniciando un juego de ajedrez con ${this.numeroDeJugadores} jugadores.`);
  }
  
  get hayaGanador() {
    return this.turno > this.turnosMaximos;
  }
  
  tomarTurno() {
    console.log(`Turno ${this.turno} tomado por jugador ${this.jugadorActual}`);
    this.jugadorActual = (this.jugadorActual + 1) % this.numeroDeJugadores;
    this.turno++;
  }
  
  get jugadorGanador() {
    return this.jugadorActual;
  }
}

let ajedrez = new Ajedrez();
ajedrez.ejecutar();

// Salida esperada:

// Iniciando un juego de ajedrez con 2 jugadores.
// Turno 1 tomado por jugador 0
// Turno 2 tomado por jugador 1
// Turno 3 tomado por jugador 0
// Turno 4 tomado por jugador 1
// Turno 5 tomado por jugador 0
// Turno 6 tomado por jugador 1
// Turno 7 tomado por jugador 0
// Turno 8 tomado por jugador 1
// Turno 9 tomado por jugador 0
// Turno 10 tomado por jugador 1
// Jugador 1 gana.

```