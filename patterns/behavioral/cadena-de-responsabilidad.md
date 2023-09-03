### Cadena de responsabilidad

Crea una cadena de objetos. Partiendo de un punto, se detiene hasta encontrar una determinada condición.

En el diseño orientado a objetos, el patrón de cadena de responsabilidad es un patrón de diseño que consta de una fuente de objetos de comando y una serie de objetos de procesamiento.

**Ejemplo:**

Usaremos un ejemplo de un juego que tiene una criatura. La criatura aumentará su defensa y ataque cuando llegue a cierto punto. Creará una cadena y el ataque y la defensa aumentarán y disminuirán.

**Paso 1. Definición de las clases clave y el patrón Cadena de Responsabilidad:** En este paso, definimos las clases principales, incluyendo Creatura y ModificadorCreatura, así como las clases de modificadores específicos.

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
    if (this.siguiente) this.siguiente.agregar(modificador);
    else this.siguiente = modificador;
  }

  manejar() {
    if (this.siguiente) this.siguiente.manejar();
  }
}
```

**Paso 2. Implementación de los modificadores específicos:** Creamos los modificadores específicos, como ModificadorSinBonificaciones, ModificadorDobleAtaque, y ModificadorAumentarDefensa.

```
class ModificadorSinBonificaciones extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }

  manejar() {
    console.log("¡No hay bonificaciones para ti!");
  }
}

class ModificadorDobleAtaque extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }

  manejar() {
    console.log(`Doblando ataque de ${this.creatura.nombre}`);
    this.creatura.ataque *= 2;
    super.manejar();
  }
}

class ModificadorAumentarDefensa extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }

  manejar() {
    if (this.creatura.ataque <= 2) {
      console.log(`Incrementando defensa de ${this.creatura.nombre}`);
      this.creatura.defensa++;
    }
    super.manejar();
  }
}
```

**Paso 3. Uso del patrón Cadena de Responsabilidad:** En este paso, creamos una instancia de Creatura, luego creamos una cadena de responsabilidad de modificadores y la aplicamos a la criatura.

```
let picachu = new Creatura("Picachu", 1, 1);
console.log(picachu.toString());

let raiz = new ModificadorCreatura(picachu);
raiz.agregar(new ModificadorSinBonificaciones(picachu));
raiz.agregar(new ModificadorAumentarDefensa(picachu));
raiz.manejar();

console.log(picachu.toString());
```

Este código final combina todos los pasos y muestra la salida esperada cuando se ejecuta.

**Código final:**

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
    if (this.siguiente) this.siguiente.agregar(modificador);
    else this.siguiente = modificador;
  }

  manejar() {
    if (this.siguiente) this.siguiente.manejar();
  }
}

class ModificadorSinBonificaciones extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }

  manejar() {
    console.log("¡No hay bonificaciones para ti!");
  }
}

class ModificadorDobleAtaque extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }

  manejar() {
    console.log(`Doblando ataque de ${this.creatura.nombre}`);
    this.creatura.ataque *= 2;
    super.manejar();
  }
}

class ModificadorAumentarDefensa extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }

  manejar() {
    if (this.creatura.ataque <= 2) {
      console.log(`Incrementando defensa de ${this.creatura.nombre}`);
      this.creatura.defensa++;
    }
    super.manejar();
  }
}

// Crear una criatura y mostrar su estado inicial
let picachu = new Creatura("Picachu", 1, 1);
console.log(picachu.toString());

// Crear una cadena de responsabilidad y agregar modificadores
let raiz = new ModificadorCreatura(picachu);
raiz.agregar(new ModificadorSinBonificaciones(picachu));
raiz.agregar(new ModificadorAumentarDefensa(picachu));

// Aplicar los modificadores a la criatura
raiz.manejar();

// Mostrar el estado final de la criatura después de aplicar modificadores
console.log(picachu.toString());

// Salida esperada:
// Picachu (1 / 1)
// Incrementando defensa de Picachu
// Picachu (1 / 2)
```
