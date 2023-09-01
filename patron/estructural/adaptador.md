### Adaptador

Este patrón permite que las clases con interfaces incompatibles trabajen juntas ajustando su propia interfaz alrededor de la clase existente.

En ingeniería de software, el patrón adaptador es un patrón de diseño de software que permite utilizar la interfaz de una clase existente como otra interfaz. A menudo se usa para hacer que las clases existentes funcionen con otras sin modificar su código fuente.

### Ejemplo:

Estamos usando un ejemplo de una calculadora. Calculadora1 es una interfaz antigua y Calculadora2 es una interfaz nueva. Construiremos un adaptador que envolverá la nueva interfaz y nos dará resultados usando sus nuevos métodos.

```
class Calculadora1 {
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

class Calculadora2 {
  constructor() {
    this.sumar = function(valor1, valor2) {
      return valor1 + valor2;
    };
    
    this.restar = function(valor1, valor2) {
      return valor1 - valor2;
    };
  }
}

// Creemos la clase adaptadora

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

// Ahora usemos todo esto combinado
const calAdaptada = new CalAdaptador();
console.log(calcAdaptada.operaciones(10, 55, 'restar'));
```