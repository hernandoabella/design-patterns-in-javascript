### Observador

Permite que varios objetos observadores vean un evento.

El patrón de observador es un patrón de diseño de software en el que un objeto, llamado sujeto, mantiene una lista de sus dependientes, llamados observadores, y les notifica automáticamente cualquier cambio de estado, generalmente llamando a uno de sus métodos.

**Ejemplo:**

Tomaremos un ejemplo de una persona en la que si una persona se enferma, mostrará una notificación.

**Paso 1. Definición de las clases y el patrón Observador:**

En este paso, definimos tres clases clave: Evento, Enfermarse, y Persona. La clase Evento representa un evento observable y contiene la lógica para suscribirse, darse de baja y notificar a los observadores. La clase Enfermarse es un evento específico que contiene información sobre la dirección donde ocurre. La clase Persona es el sujeto observable que puede "enfermarse" y notificar a los observadores cuando esto sucede.

```
// Clase Evento que representa un evento observable
class Evento {
  constructor() {
    this.manejadores = new Map();
    this.contador = 0;
  }

  // Método para suscribir un manejador al evento y devuelve un identificador único
  suscribir(manejador) {
    this.manejadores.set(++this.contador, manejador);
    return this.contador;
  }

  // Método para darse de baja de un evento dado un identificador
  darseDeBaja(idx) {
    this.manejadores.delete(idx);
  }

  // Método para notificar a todos los observadores cuando ocurre el evento
  fuego(enviador, argumentos) {
    this.manejadores.forEach((manejador, id) => manejador(enviador, argumentos));
  }
}

// Clase Enfermarse que representa un evento específico
class Enfermarse {
  constructor(direccion) {
    this.direccion = direccion;
  }
}

// Clase Persona que será el sujeto observable
class Persona {
  constructor(direccion) {
    this.direccion = direccion;
    this.enfermarse = new Evento(); // Creamos un evento "enfermarse"
  }

  // Método para simular que la persona se enferma y notificar a los observadores
  agarrarResfriado() {
    this.enfermarse.fuego(this, new Enfermarse(this.direccion));
  }
}
```


**Paso 2. Uso del patrón Observador:**

En este paso, creamos una instancia de Persona y luego suscribimos un observador al evento enfermarse utilizando el método suscribir de la clase Evento. Luego, simulamos que la persona se enferma dos veces llamando al método agarrarResfriado. Después, damos de baja al observador utilizando el método darseDeBaja. Finalmente, llamamos nuevamente al método agarrarResfriado, pero el observador dado de baja ya no recibe notificaciones.

Este patrón permite que varios observadores vean un evento (en este caso, enfermarse) sin que la clase Persona tenga que conocer los detalles de quiénes son los observadores ni cómo reaccionan ante el evento.

```
// Creamos una instancia de la persona
let persona = new Persona("Ruta ABC");

// Suscribimos un observador al evento "enfermarse"
let sub = persona.enfermarse.suscribir((sujeto, evento) => {
  console.log(`Un doctor ha sido llamado a ${evento.direccion}`);
});

// La persona se enferma dos veces
persona.agarrarResfriado();
persona.agarrarResfriado();

// Damos de baja al observador
persona.enfermarse.darseDeBaja(sub);

// La persona se enferma nuevamente, pero el observador dado de baja no recibe la notificación
persona.agarrarResfriado();
```


**Código final:**

```
// Definición de las clases y el patrón Observador

// Clase Evento que representa un evento observable
class Evento {
  constructor() {
    this.manejadores = new Map();
    this.contador = 0;
  }

  // Método para suscribir un manejador al evento y devuelve un identificador único
  suscribir(manejador) {
    this.manejadores.set(++this.contador, manejador);
    return this.contador;
  }

  // Método para darse de baja de un evento dado un identificador
  darseDeBaja(idx) {
    this.manejadores.delete(idx);
  }

  // Método para notificar a todos los observadores cuando ocurre el evento
  fuego(enviador, argumentos) {
    this.manejadores.forEach((manejador, id) => manejador(enviador, argumentos));
  }
}

// Clase Enfermarse que representa un evento específico
class Enfermarse {
  constructor(direccion) {
    this.direccion = direccion;
  }
}

// Clase Persona que será el sujeto observable
class Persona {
  constructor(direccion) {
    this.direccion = direccion;
    this.enfermarse = new Evento(); // Creamos un evento "enfermarse"
  }

  // Método para simular que la persona se enferma y notificar a los observadores
  agarrarResfriado() {
    this.enfermarse.fuego(this, new Enfermarse(this.direccion));
  }
}

// Uso del patrón Observador

// Creamos una instancia de la persona
let persona = new Persona("Ruta ABC");

// Suscribimos un observador al evento "enfermarse"
let sub = persona.enfermarse.suscribir((sujeto, evento) => {
  console.log(`Un doctor ha sido llamado a ${evento.direccion}`);
});

// La persona se enferma dos veces
persona.agarrarResfriado();
persona.agarrarResfriado();

// Damos de baja al observador
persona.enfermarse.darseDeBaja(sub);

// La persona se enferma nuevamente, pero el observador dado de baja no recibe la notificación
persona.agarrarResfriado();

// Salida esperada:
// Un doctor ha sido llamado a Ruta ABC
// Un doctor ha sido llamado a Ruta ABC

```