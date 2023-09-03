### Cadena de responsabilidad

Crea una cadena de objetos. Partiendo de un punto, se detiene hasta encontrar una determinada condición.

En el diseño orientado a objetos, el patrón de cadena de responsabilidad es un patrón de diseño que consta de una fuente de objetos de comando y una serie de objetos de procesamiento.

### Ejemplo:

Usaremos un ejemplo de un juego que tiene una criatura. La criatura aumentará su defensa y ataque cuando llegue a cierto punto. Creará una cadena y el ataque y la defensa aumentarán y disminuirán.

```
class Creatura {
  constructor(nombre, ataque, defensa) {
    this.nombre = nombre;
    this.ataque = ataque;
    this.defensa = defensa;
  }
  
  toString() {
    return `${this.nombre} (${this.ataque} / ${this.defensa})`;
  }
  
}

class ModificadorCreatura {
  constructor(creatura) {
    this.creatura = creatura;
    this.siguiente = null;
  }
  
  agregar(modificador) {
    if(this.siguiente) this.siguiente.agregar(modificador);
    else this.siguiente = modificador;
  }
  
  manejar() {
    if(this.siguiente) this.siguiente.manejar();
  }
}

class ModificadorSinBonificaciones extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }
  
  manejar() {
    console.log("¡no hay bonificaciones para ti!")
  }
}

```

Aumentar el ataque

```
class ModificadorDobleAtaque extends ModificadorCretura {
  constructor(creatura) {
    super(creatura);
  }
  
  manejar() {
    console.log(`Doblando ataque de ${this.creatura.nombre}`);
    this.creatura.ataque *= 2;
    super.manejar();
  }
}

```

Aumentar la defensa

```
class ModificadorAumentarDefensa extends ModificadorCreatura {
  constructor(creatura) {
    super creatura;
  }
  
  manejar() {
    if(this.creatura.ataque <= 2) {
      console.log(`Incrementando defensa de ${this.creatura.nombre}`);
      this.creatura.defensa++;
    }
    super.manejar();
  }
}
```

Así es como usaremos esto

```
let picachu = new Creatura("Picachu", 1, 1);
console.log(picachu.toString());

let raiz = new ModificadorCreatura(picachu);
raiz.agregar(new ModificadorCreatura(picachu));
raiz.agregar(new ModificadorAumentarDefensa(picachu));
raiz.manejar();

console.log(picachu.toString());

```