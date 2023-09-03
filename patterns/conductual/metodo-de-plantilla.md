### Método de plantilla

Define el esqueleto de un algoritmo como una clase abstracta, cómo debe realizarse.

Template Method (método de plantilla) es un método en una superclase, generalmente una superclase abstracta, y define el esqueleto de una operación en términos de una serie de pasos de alto nivel.

### Ejemplo:

Tomaremos un ejemplo de un juego de ajedrez,

```
class Juego {
  constructor(numeroJugadores) {
    this.numeroDeJugadores = numeroDeJugadores;
    this.jugadorActual = 0;
  }
  
  ejecutar() {
    this.iniciar();
    while(!this.hayaGanador) {
      this.tomarTurno();
    }
    console.log(`Jugador ${this.jugadorGanador} gana.`);
  }
  iniciar() {}
  get hayaJugador {}
  tomarTurno();
  get jugadorGanador() {}
}
```

Creando nuestra clase Ajedrez,

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
    return this.turno === this.turnosMaximos;
  }
  
  tomarTurno(){
    console.log(`Turno ${this.turno} tomado por jugador ${this.jugadorActual}`);
    this.jugadorActual = (this.jugadorActual + 1) % this.numeroDeJugadores;
  }
  
  get jugadorGanador() {
    return this.jugadorActual;
  }
  
}
```

Así usaremos esto:

```
let ajedrez = new Ajedrez();
ajedrez.ejecutar();
```