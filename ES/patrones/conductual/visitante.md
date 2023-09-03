### Visitante

Agrega operaciones a los objetos sin tener que modificarlos.

El patrón de diseño del visitante es una forma de separar un algoritmo de una estructura de objeto en la que opera. Un resultado práctico de esta separación es la capacidad de agregar nuevas operaciones a estructuras de objetos existentes sin modificar las estructuras.

### Ejemplo:

Tomaremos un ejemplo de la clase ExpresionNumerica en el que nos da el resultado de la expresión dada.

```
class ExpresionNumerica {
  constructor(valor) {
    this.valor = valor;
  }
  
  imprimir(buffer) {
    buffer.push(this.valor.toString());
  }
}

// Creando Expresión de Suma
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

// Así es como usamos esto, 
// Expresión dada => 5 + (1 + 9)

let e = new ExpresionSuma(
    new ExpresionNumerica(5),
    new ExpresionSuma(
        new ExpresionNumerica(1),
        new ExpresionNumerica(9)
        )
);

let buffer = [];
e.print(buffer);

console.log(buffer.join(''));
```