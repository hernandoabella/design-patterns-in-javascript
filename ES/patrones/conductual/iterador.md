### Iterador

Iterator accede a los elementos de un objeto sin exponer su representación subyacente.

En la programación orientada a objetos, el patrón de iterador es un patrón de diseño en el que se utiliza un iterador para atravesar un contenedor y acceder a los elementos del contenedor.

Definición de la Clase Cosa: Primero, definimos una clase llamada Cosa que tiene dos propiedades a y b.

**Ejemplo:**

```
class Cosa {
  constructor() {
    this.a = 11;
    this.b = 22;
  }
  // ...
}

```

Método [Symbol.iterator]: Definimos un método [Symbol.iterator] dentro de la clase Cosa. Este método se utiliza para crear un iterador personalizado que recorrerá los elementos a y b de la clase.

```
[Symbol.iterator]() {
  let i = 0;
  let self = this;
  return {
    next: function() {
      return {
        done: i > 1, // Indica si se ha recorrido todo
        value: self[i++ === 0 ? 'a' : 'b'] // Obtiene el valor correspondiente
      };
    }
  };
}

```

Método haciaAtras: Definimos un método llamado haciaAtras que devuelve un iterador para recorrer los elementos en orden inverso.

```
get haciaAtras() {
  let i = 0;
  let self = this;
  return {
    next: function() {
      return {
        done: i > 1,
        value: self[i++ === 0 ? 'b' : 'a']
      };
    },
    [Symbol.iterator]: function() { return this; } // Hacer que el iterador sea iterable
  };
}

```

Usar un Arreglo: Creamos un arreglo llamado valores y lo recorremos utilizando un bucle for...in para mostrar sus elementos y valores.

```
let valores = [100, 200, 300];

for (let i in valores) {
  console.log(`Elemento en la posición ${i} es ${valores[i]}`);
}

for (let v in valores) {
  console.log(`El valor es ${v}`);
}

```

Usar la Clase Cosa: Creamos una instancia de la clase Cosa llamada cosa y utilizamos un bucle for...of para recorrer sus elementos utilizando el iterador personalizado.

```
let cosa = new Cosa();

console.log("Recorriendo 'a' y 'b':");
for (let elemento of cosa) {
  console.log(`${elemento}`);
}

```

Recorriendo en Orden Inverso: Utilizamos el método haciaAtras de la clase Cosa para obtener un iterador en orden inverso y lo recorremos usando un bucle for...of.

```
console.log("Recorriendo en orden inverso:");
for (let elemento of cosa.haciaAtras) {
  console.log(`${elemento}`);
}

```

**Código final:**

Tomaremos el ejemplo de un arreglo en el que imprimimos los valores de un arreglo y luego, mediante el uso de un iterador, imprimimos sus valores hacia atrás.

```
class Cosa {
  constructor() {
    this.a = 11;
    this.b = 22;
  }

  // Definir un iterador para recorrer los elementos 'a' y 'b' de esta clase
  [Symbol.iterator]() {
    let i = 0;
    let self = this;
    return {
      next: function() {
        return {
          done: i > 1, // Indica si se ha recorrido todo
          value: self[i++ === 0 ? 'a' : 'b'] // Obtiene el valor correspondiente
        };
      }
    };
  }

  // Obtener un iterador para recorrer los elementos en orden inverso
  get haciaAtras() {
    let i = 0;
    let self = this;
    return {
      next: function() {
        return {
          done: i > 1,
          value: self[i++ === 0 ? 'b' : 'a']
        };
      },
      [Symbol.iterator]: function() { return this; } // Hacer que el iterador sea iterable
    };
  }
}

let valores = [100, 200, 300];

// Usar un bucle for...in para recorrer un arreglo
for (let i in valores) {
  console.log(`Elemento en la posición ${i} es ${valores[i]}`);
}

// Usar un bucle for...in para recorrer un objeto
for (let v in valores) {
  console.log(`El valor es ${v}`);
}

let cosa = new Cosa();

console.log("Recorriendo 'a' y 'b':");
for (let elemento of cosa) {
  console.log(`${elemento}`);
}

console.log("Recorriendo en orden inverso:");
for (let elemento of cosa.haciaAtras) {
  console.log(`${elemento}`);
}

```
