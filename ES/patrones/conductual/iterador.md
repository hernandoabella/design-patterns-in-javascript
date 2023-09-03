### Iterador

Iterator accede a los elementos de un objeto sin exponer su representación subyacente.

En la programación orientada a objetos, el patrón de iterador es un patrón de diseño en el que se utiliza un iterador para atravesar un contenedor y acceder a los elementos del contenedor.

Definición de la Clase Cosa: Primero, definimos una clase llamada Cosa que tiene dos propiedades a y b.

**Paso 1:** Definir la clase 'Cosa' y sus propiedades 'a' y 'b'.

```
class Cosa {
  constructor() {
    this.a = 11;
    this.b = 22;
  }
  // Resto del código
}

```

**Paso 2:** Implementar el método [Symbol.iterator]() para recorrer las propiedades 'a' y 'b' de la clase 'Cosa'.


```
class Cosa {
  // ...

  [Symbol.iterator]() {
    let i = 0;
    let self = this;
    return {
      next: function() {
        return {
          done: i > 1,
          value: self[i++ === 0 ? 'a' : 'b']
        };
      }
    };
  }

  // Resto del código
}
```

**Paso 3:** Implementar la propiedad 'haciaAtras' para recorrer las propiedades en orden inverso.

```
class Cosa {
  // ...

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
      [Symbol.iterator]: function() { return this; }
    };
  }

  // Resto del código
}

```

**Paso 4:** Crear un arreglo 'valores' con elementos numéricos.

```
let valores = [100, 200, 300];

```

**Paso 5:** Utilizar un bucle 'for...in' para recorrer el arreglo 'valores'.

```
for (let i in valores) {
  console.log(`Elemento en la posición ${i} es ${valores[i]}`);
}

```

**Paso 6:** Utilizar otro bucle 'for...in' para recorrer un objeto (no recomendado).

```
for (let v in valores) {
  console.log(`El valor es ${v}`);
}

```

**Paso 7:** Crear una instancia de la clase 'Cosa' llamada 'cosa'.
```
let cosa = new Cosa();

```
**Paso 8:** Utilizar un bucle 'for...of' para recorrer las propiedades de 'cosa'.

```
console.log("Recorriendo 'a' y 'b':");
for (let elemento of cosa) {
  console.log(`${elemento}`);
}

```

**Paso 9:** Utilizar otro bucle 'for...of' para recorrer en orden inverso.

```
console.log("Recorriendo en orden inverso:");
for (let elemento of cosa.haciaAtras) {
  console.log(`${elemento}`);
}

```



**Código final:**

Tomaremos el ejemplo de un arreglo en el que imprimimos los valores de un arreglo y luego, mediante el uso de un iterador, imprimimos sus valores hacia atrás.

```
// Definir una clase llamada 'Cosa'
class Cosa {
  constructor() {
    this.a = 11; // Propiedad 'a' con valor 11
    this.b = 22; // Propiedad 'b' con valor 22
  }

  // Definir un iterador para recorrer los elementos 'a' y 'b' de esta clase
  [Symbol.iterator]() {
    let i = 0; // Inicializar un índice para llevar el control
    let self = this; // Capturar una referencia a la instancia actual ('this')
    return {
      next: function() {
        return {
          done: i > 1, // Indica si se ha recorrido todo (cuando 'i' sea mayor a 1)
          value: self[i++ === 0 ? 'a' : 'b'] // Obtiene el valor correspondiente ('a' o 'b')
        };
      }
    };
  }

  // Obtener un iterador para recorrer los elementos en orden inverso
  get haciaAtras() {
    let i = 0; // Inicializar un índice para llevar el control
    let self = this; // Capturar una referencia a la instancia actual ('this')
    return {
      next: function() {
        return {
          done: i > 1, // Indica si se ha recorrido todo (cuando 'i' sea mayor a 1)
          value: self[i++ === 0 ? 'b' : 'a'] // Obtiene el valor correspondiente ('b' o 'a')
        };
      },
      [Symbol.iterator]: function() { return this; } // Hacer que el iterador sea iterable
    };
  }
}

let valores = [100, 200, 300];

// Usar un bucle for...in para recorrer un arreglo (Nota: no es la forma recomendada para arreglos)
for (let i in valores) {
  console.log(`Elemento en la posición ${i} es ${valores[i]}`);
}

// Usar un bucle for...in para recorrer un objeto (Nota: no es la forma recomendada para objetos)
for (let v in valores) {
  console.log(`El valor es ${v}`);
}

let cosa = new Cosa(); // Crear una instancia de la clase 'Cosa'

console.log("Recorriendo 'a' y 'b':");
for (let elemento of cosa) {
  console.log(`${elemento}`);
}

console.log("Recorriendo en orden inverso:");
for (let elemento of cosa.haciaAtras) {
  console.log(`${elemento}`);
}

```
