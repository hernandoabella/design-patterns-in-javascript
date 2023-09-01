### Singleton

Asegura que solo haya un objeto creado para una clase en particular.

En ingeniería de software, el patrón singleton es un patrón de diseño de software que restringe la creación de instancias de una clase a una instancia "única". Esto es útil cuando se necesita exactamente un objeto para coordinar acciones en todo el sistema.

### Ejemplo:

Creando una clase Singleton:

```
class Singleton {
  constructor() {
    const instancia = this.constructor.instancia;
    if(instancia) {
      return instancia;
    }
    
    this.constructor.instancia = this;
  }
  
  decir(){
    console.log('Diciendo...')
  }
}

// Usemos el Singleton que hemos creado

let s1 = new Singleton();
let s2 = new Singleton();
console.log('¿Son lo mismo? ' + (s1 === s2));

s1.decir();
```