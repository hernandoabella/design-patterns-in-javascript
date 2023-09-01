### Adaptador

El patrón adaptador permite que las clases con interfaces incompatibles trabajen juntas ajustando su propia interfaz alrededor de la clase existente. Esto es especialmente útil cuando necesitamos que objetos con interfaces diferentes colaboren sin modificar su código fuente.

**Ejemplo:**

**1. Definición de las Interfaces Incompatibles:** En este ejemplo, tenemos dos interfaces de calculadora: Calculadora1 (antigua) y Calculadora2 (nueva).

```
class Calculadora1 {
  constructor() {
    this.operaciones = function(valor1, valor2, operacion) {
      // Implementación de la calculadora antigua
      switch(operacion) {
        case 'sumar':
          return valor1 + valor2;
        case 'restar':
          return valor1 - valor2;
      }
    };
  }
}

class Calculadora2 {
  constructor() {
    this.sumar = function(valor1, valor2) {
      // Implementación de la calculadora nueva
      return valor1 + valor2;
    };
    
    this.restar = function(valor1, valor2) {
      // Implementación de la calculadora nueva
      return valor1 - valor2;
    };
  }
}
```

**2. Creación de un Adaptador:** Creamos una clase CalcAdaptador que actuará como adaptador entre las dos interfaces de calculadora. El adaptador envolverá la nueva interfaz (Calculadora2) y proporcionará métodos para las operaciones requeridas.

```
class CalcAdaptador {
  constructor() {
    const cal2 = new Calculadora2();
    this.operaciones = function(valor1, valor2, operacion) {
      switch(operacion) {
        case 'sumar':
          return cal2.sumar(valor1, valor2);
        case 'restar':
          return cal2.restar(valor1, valor2);
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

**Código final:**

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
