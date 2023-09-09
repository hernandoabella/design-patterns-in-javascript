### Mediador

El patrón mediador agrega un objeto de terceros para controlar la interacción entre dos objetos. Permite un acoplamiento flexible entre clases al ser la única clase que tiene un conocimiento detallado de sus métodos.

El patrón mediador define un objeto que encapsula cómo interactúa un conjunto de objetos. Este patrón se considera un patrón de comportamiento debido a la forma en que puede alterar el comportamiento de ejecución del programa. En la programación orientada a objetos, los programas a menudo constan de muchas clases.

Usaremos un ejemplo de una persona que usa una sala de chat. Aquí, una sala de chat actúa como mediador entre dos personas que se comunican entre sí.

**Ejemplo:**

**Paso 1:** Definición de la clase Persona, que representa a las personas en la sala de chat:

```
class Persona {
  constructor(nombre, salaChat) {
    this.nombre = nombre;         // Nombre de la persona
    this.salaChat = salaChat;     // Sala de chat a la que pertenece
  }

  // Método para enviar un mensaje en la sala de chat
  decir(mensaje) {
    this.salaChat.enviarMensaje(this, mensaje);
  }

  // Método para recibir un mensaje
  recibir(mensaje) {
    console.log(`${this.nombre} recibe: ${mensaje}`);
  }
}

```

**Paso 2:** Definición de la clase SalaChat, que actúa como mediador:

```
class SalaChat {
  constructor() {
    this.personas = [];  // Almacena las personas en la sala de chat
  }

  // Método para agregar una persona a la sala de chat
  unirPersona(persona) {
    this.personas.push(persona);  // Agrega la persona a la lista
    persona.salaChat = this;      // Establece la sala de chat de la persona como esta sala
  }

  // Método para enviar un mensaje a todas las personas en la sala
  enviarMensaje(emisor, mensaje) {
    for (const persona of this.personas) {
      if (persona !== emisor) {
        persona.recibir(`${emisor.nombre}: ${mensaje}`);
      }
    }
  }
}

```

**Paso 3:** Creación de una sala de chat (SalaChat):

```
const sala = new SalaChat();

```

**Paso 4:** Creación de personas y unión a la sala de chat:

```
const john = new Persona("John", sala);
const tony = new Persona("Tony", sala);

sala.unirPersona(john);
sala.unirPersona(tony);

```

**Paso 5:** John envía un mensaje en la sala de chat:

```
john.decir("¡Hola a todos!");
```

**Paso 6:** Creación de una nueva persona y unión a la sala de chat:

```
const doe = new Persona("Doe", sala);
sala.unirPersona(doe);

```

**Paso 7:** Doe envía un mensaje en la sala de chat:

```
doe.decir("¡Hola a todos!");
```

Cada vez que alguien envía un mensaje, la sala de chat se encarga de distribuir ese mensaje a todas las demás personas en la sala.

**Código final:**

```
// Definición de la clase Persona, que representa a las personas en la sala de chat
class Persona {
  constructor(nombre, salaChat) {
    this.nombre = nombre;         // Nombre de la persona
    this.salaChat = salaChat;     // Sala de chat a la que pertenece
  }

  // Método para enviar un mensaje en la sala de chat
  decir(mensaje) {
    this.salaChat.enviarMensaje(this, mensaje);
  }

  // Método para recibir un mensaje
  recibir(mensaje) {
    console.log(`${this.nombre} recibe: ${mensaje}`);
  }
}

// Definición de la clase SalaChat, que actúa como mediador
class SalaChat {
  constructor() {
    this.personas = [];  // Almacena las personas en la sala de chat
  }

  // Método para agregar una persona a la sala de chat
  unirPersona(persona) {
    this.personas.push(persona);  // Agrega la persona a la lista
    persona.salaChat = this;      // Establece la sala de chat de la persona como esta sala
  }

  // Método para enviar un mensaje a todas las personas en la sala
  enviarMensaje(emisor, mensaje) {
    for (const persona of this.personas) {
      if (persona !== emisor) {
        persona.recibir(`${emisor.nombre}: ${mensaje}`);
      }
    }
  }
}

// Creación de una sala de chat
const sala = new SalaChat();

// Creación de personas y unión a la sala de chat
const john = new Persona("John", sala);
const tony = new Persona("Tony", sala);

sala.unirPersona(john);
sala.unirPersona(tony);

// John envía un mensaje en la sala de chat
john.decir("¡Hola a todos!");

// Creación de una nueva persona y unión a la sala de chat
const doe = new Persona("Doe", sala);
sala.unirPersona(doe);

// Doe envía un mensaje en la sala de chat
doe.decir("¡Hola a todos!");

```
