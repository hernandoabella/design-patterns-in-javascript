### Mediador

El patrón mediador agrega un objeto de terceros para controlar la interacción entre dos objetos. Permite un acoplamiento flexible entre clases al ser la única clase que tiene un conocimiento detallado de sus métodos.

El patrón mediador define un objeto que encapsula cómo interactúa un conjunto de objetos. Este patrón se considera un patrón de comportamiento debido a la forma en que puede alterar el comportamiento de ejecución del programa. En la programación orientada a objetos, los programas a menudo constan de muchas clases.

Usaremos un ejemplo de una persona que usa una sala de chat. Aquí, una sala de chat actúa como mediador entre dos personas que se comunican entre sí.

```
class Persona {
  constructor(nombre) {
    this.nombre = nombre;
    this.registroChat = [];
  }
  
  recibir(enviador, mensaje) {
    let s = `${enviador}: ${mensaje}`;
    console.log(`La sesión de chat de [${this.nombre}] ${s}`);
    this.registroChat.push(s);
  }
  
  decir(mensaje) {
    this.room.broadcast(this.nombre, mensaje);
  }
  
  pm(quien, mensaje) {
    this.room.mensaje(this.nombre, quien, mensaje);
  }
}
```

Crear sala de chat,

```
class SalaChat {
  constructor() {
    this.gente = [];
  }
  
  transmision(origen, mensaje) {
    for(let p of this.gente)
      if(p.nombre !== origen) p.recibir(origen, mensaje);
  }
  
  unir(p) {
    let unirMensaje = `${p.nombre} se unió al chat`;
    this.transmision("room", unirMensaje) {
    p.room == this;
    this.gente.push(p);
    }
  }
  
  message(origen, destinacion, mensaje) {
    for(let p of this.gente)
      if(p.nombre === destino) p.recibir(origen, mensaje);
  }
}
```

Así es como usamos esto,

```
let sala = new SalaChat();
let John = new Persona("John");
let Tony = new Persona("Tony");

sala.unir(John);
sala.unir(Tony);
John.decir("¡Hola!");

let doe = new Persona("Doe");
sala.unir(doe);
doe.decir("¡Hola a todos!");
```