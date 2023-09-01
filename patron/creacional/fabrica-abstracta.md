Fábrica Abstracta (Abstract Factory)

En diseño de software, el patrón de diseño de Fábrica Abstracta es una técnica que se utiliza para crear familias o grupos de objetos relacionados sin especificar sus clases concretas. Este patrón proporciona una forma de encapsular un conjunto de fábricas individuales que comparten un tema común sin necesidad de conocer los detalles de las clases exactas de los objetos que se crearán. Esto promueve la creación de objetos de manera coherente y modular, lo que facilita la gestión y extensión del código.

**Ejemplo:**

Para comprender mejor el patrón de Fábrica Abstracta, consideremos un ejemplo relacionado con la preparación de bebidas, como té y café.

```
// Definición de las clases base y subclases

class Bebida {
  consumir() {
    // Método abstracto, se implementará en las subclases
  }
}

class Tea extends Bebida {
  consumir() {
    console.log('Esto es Tea');
  }
}

class Cafe extends Bebida {
  consumir() {
    console.log('Esto es Café');
  }
}

// Definición de la clase de fábrica base y subclases de fábrica

class FabricaBebidas {
  preparar(cantidad) {
    // Método abstracto, se implementará en las subclases
  }
}

class FabricaTea extends FabricaBebidas {
  hacerTea() {
    console.log('Té creado');
    return new Tea();
  }
}

class FabricaCafe extends FabricaBebidas {
  hacerCafe() {
    console.log('Café creado');
    return new Cafe();
  }
}

// Ejemplo de uso

let fabricaBebidaTea = new FabricaTea(); // Creamos una fábrica de té
let tea = fabricaBebidaTea.hacerTea(); // Usamos la fábrica para crear una bebida de té
tea.consumir(); // Consumimos la bebida de té

// Salida esperada:
// Té creado
// Esto es Tea
```
