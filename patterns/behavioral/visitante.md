### Visitante

Agrega operaciones a los objetos sin tener que modificarlos.

El patrón de diseño del visitante es una forma de separar un algoritmo de una estructura de objeto en la que opera. Un resultado práctico de esta separación es la capacidad de agregar nuevas operaciones a estructuras de objetos existentes sin modificar las estructuras.

**Ejemplo:**

Tomaremos un ejemplo de la clase ExpresionNumerica en el que nos da el resultado de la expresión dada.



**1.Clase ExpresionNumerica:** Esta clase representa una expresión numérica simple con un valor.


```
class ExpresionNumerica {
  constructor(valor) {
    this.valor = valor;
  }

  imprimir(buffer) {
    buffer.push(this.valor.toString());
  }
}
```

**2.Clase ExpresionSuma:** Esta clase representa una expresión de suma que toma dos expresiones numéricas (izquierda y derecha) y las suma.

```
class ExpresionSuma {
  constructor(izquierda, derecha) {
    this.izquierda = izquierda;
    this.derecha = derecha;
  }

  imprimir(buffer) {
    buffer.push('(');
    this.izquierda.imprimir(buffer);
    buffer.push('+');
    this.derecha.imprimir(buffer);
    buffer.push(')');
  }
}
```

**3.Uso del Patrón del Visitante:** Luego, creas una expresión compuesta que representa "5 + (1 + 9)" utilizando instancias de las clases ExpresionNumerica y ExpresionSuma.

```
let e = new ExpresionSuma(
    new ExpresionNumerica(5),
    new ExpresionSuma(
        new ExpresionNumerica(1),
        new ExpresionNumerica(9)
    )
);
```

Impresión de la Expresión: Finalmente, se utiliza el método imprimir() para obtener una representación legible de la expresión y se almacena en un buffer.

```
let buffer = [];
e.imprimir(buffer);
console.log(buffer.join('')); // Salida: (5+(1+9))
```

Este ejemplo ilustra cómo el patrón de diseño del visitante permite agregar la operación de impresión a objetos complejos sin tener que modificar su estructura interna. Esto hace que el código sea más flexible y extensible para futuras operaciones sin afectar las clases existentes.

**Código final:**

```
class ExpresionNumerica {
  constructor(valor) {
    this.valor = valor;
  }

  imprimir(buffer) {
    buffer.push(this.valor.toString());
  }
}

class ExpresionSuma {
  constructor(izquierda, derecha) {
    this.izquierda = izquierda;
    this.derecha = derecha;
  }

  imprimir(buffer) {
    buffer.push('(');
    this.izquierda.imprimir(buffer);
    buffer.push('+');
    this.derecha.imprimir(buffer);
    buffer.push(')');
  }
}

// Creación de una expresión compuesta: 5 + (1 + 9)
let e = new ExpresionSuma(
    new ExpresionNumerica(5),
    new ExpresionSuma(
        new ExpresionNumerica(1),
        new ExpresionNumerica(9)
    )
);

let buffer = [];
e.imprimir(buffer);

console.log(buffer.join('')); // Salida esperada: (5+(1+9))

```

La salida esperada es (5+(1+9)), que es la representación de la expresión "5 + (1 + 9)" después de imprimirla utilizando el patrón del visitante. Este código demuestra cómo el patrón del visitante permite agregar la operación de impresión a objetos complejos sin modificar su estructura interna.
