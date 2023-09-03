### Observador

Permite que varios objetos observadores vean un evento.

El patrón de observador es un patrón de diseño de software en el que un objeto, llamado sujeto, mantiene una lista de sus dependientes, llamados observadores, y les notifica automáticamente cualquier cambio de estado, generalmente llamando a uno de sus métodos.

### Ejemplo:

Tomaremos un ejemplo de una persona en la que si una persona se enferma, mostrará una notificación.

```
class Evento {
  contructor() {
    this.manejadores = new Map();
    this.contar = 0;
  }
  
  suscribir(manejador) {
    this.manejadores.set(++this.contar, manejador);
    return this.contar;
  }
  
  darseDeBaja(idx) {
    this.manejadores.delete(idx);
  }
  
  fuego(enviador, argumentos) {
    this.manejadores.forEach((v, k) => v(remitente, argumentos));
  }
}

class Enfermarse {
  constructor(direccion) {
    this.direccion = direccion;
  }
}

class Persona {
  constructor(direccion) {
    this.direccion = direccion;
    this.enfermarse = new Evento();
  }
  
  agarrarResfriado() {
    this.enfermarse.fuego(this, new Enfermarse(this.direccion));
  }
}
```

Así es como usaremos esto,

```
let persona = new Persona("Ruta ABC");
let sub = persona.enfermarse.suscribir((s, a) => {
  console.log(`Un doctor ha sido llamado ` + ` a ${a.direccion}`);
});

persona.agarrar.Resfriado();
persona.agarrar.Resfriado();

persona.enfermarse.darseDeBaja(sub);
persona.agarrarResfriado();
```