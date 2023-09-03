### Adapter 🔌

The adapter pattern enables classes with incompatible interfaces to collaborate by adapting their own interface to fit around the existing class. This is particularly useful when we need objects with different interfaces to work together without altering their source code.

**Example::** 

**1. Definition of Incompatible Interfaces:** In this example, we have two calculator interfaces: Calculator1 (old) and Calculator2 (new).

```
class Calculator1 {
  constructor() {
    this.operations = function(value1, value2, operation) {
      // Implementation of the old calculator
      switch(operation) {
        case 'sum':
          return value1 + value2;
        case 'subtract':
          return value1 - value2;
      }
    };
  }
}

class Calculator2 {
  constructor() {
    this.add = function(value1, value2) {
      // Implementation of the new calculator
      return value1 + value2;
    };
    
    this.subtract = function(value1, value2) {
      // Implementation of the new calculator
      return value1 - value2;
    };
  }
}
```

**2. Creating an Adapter:** We create a CalcAdapter class that will act as an adapter between the two calculator interfaces. The adapter wraps the new interface (Calculator2) and provides methods for the required operations.

```
class CalcAdapter {
  constructor() {
    const cal2 = new Calculator2();
    this.operations = function(value1, value2, operation) {
      switch(operation) {
        case 'sum':
          return cal2.add(value1, value2);
        case 'subtract':
          return cal2.subtract(value1, value2);
      }
    };
  }
}
```

**3. Uso del Adaptador:** Ahora podemos utilizar el adaptador CalcAdaptador para realizar operaciones en la nueva interfaz (Calculadora2) sin modificar su código. Esto facilita la transición de la calculadora antigua a la nueva.

```
// Creemos una instancia del adaptador
const calcAdaptada = new CalcAdaptador();

// Utilizamos el adaptador para realizar una operación de resta
console.log(calcAdaptada.operaciones(10, 55, 'restar'));
```

**Final Code:**

```
// Definimos la clase para la Calculadora Antigua
class CalculadoraAntigua {
  constructor() {
    this.operaciones = function(valor1, valor2, operacion) {
      switch(operacion) {
        case 'sumar':
          return valor1 + valor2;
        case 'restar':
          return valor1 - valor2;
      }
    };
  }
}

// Definimos la clase para la Calculadora Nueva
class CalculadoraNueva {
  constructor() {
    this.sumar = function(valor1, valor2) {
      return valor1 + valor2;
    };
    
    this.restar = function(valor1, valor2) {
      return valor1 - valor2;
    };
  }
}

// Definimos la clase para el Adaptador
class CalculadoraAdaptadora {
  constructor() {
    // Creamos una instancia de la Calculadora Nueva
    const calculadoraNueva = new CalculadoraNueva();
    
    // Definimos el método operaciones que utilizará la Calculadora Nueva
    this.operaciones = function(valor1, valor2, operacion) {
      switch(operacion) {
        case 'sumar':
          return calculadoraNueva.sumar(valor1, valor2);
        case 'restar':
          return calculadoraNueva.restar(valor1, valor2);
      }
    };
  }
}

// Creamos una instancia de la Calculadora Adaptadora
const calculadoraAdaptada = new CalculadoraAdaptadora();

// Utilizamos la Calculadora Adaptadora para realizar una operación de resta
console.log(calculadoraAdaptada.operaciones(10, 55, 'restar')); // -45
console.log(calculadoraAdaptada.operaciones(10, 55, 'sumar')); // 65
```
