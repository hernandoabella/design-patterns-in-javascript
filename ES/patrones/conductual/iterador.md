### Iterador

Iterator accede a los elementos de un objeto sin exponer su representación subyacente.

En la programación orientada a objetos, el patrón de iterador es un patrón de diseño en el que se utiliza un iterador para atravesar un contenedor y acceder a los elementos del contenedor.

**Ejemplo:**

Tomaremos el ejemplo de un arreglo en el que imprimimos los valores de un arreglo y luego, mediante el uso de un iterador, imprimimos sus valores hacia atrás.

```
class Cosa {
  constructor() {
    this.a = 11;
    this.b = 22;
  }
  
  [Symbol.iterador]() {
    let i = 0;
    let self = this;
    return {
      next: function() {
        done: i > 1, 
        valor: self[i++ === 0 ? 'a' : 'b']
      };
    }
  }
  
  get haciaAtras() {
    let i = 0;
    let self = this;
    return {
      next: function() {
        return {
          done: i > 1,
          valor: self[i++ === 0 ? 'b' : 'a']
        };
      },
      // Crear iterador iterable
      [Symbol.iterator]: function() {return this;}
    }
  }
}
```

Así es como usaremos esto,

```
let valores = [100, 200, 300];

for(let i in valores) {
  console.log(`Elemento en la posicion ${i} es ${valores[i]}`);
}

for(let v in valores) {
  console.log(`El valor es ${v}`);
}

let cosa = new Cosa();

for(let elemento of cosa)
  console.log(`${elemento}`);
  
for(let elemento of cosa)
  console.log(`${elemento}`);
```