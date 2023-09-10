### Decorador

El patrón decorador permite agregar o anular dinámicamente comportamientos a un objeto individual sin afectar a otros objetos de la misma clase. Es especialmente útil cuando se desea extender las capacidades de un objeto sin crear subclases.

**Ejemplo:**

**1. Definición de Clases:** En este ejemplo, creamos las clases Forma como base y Circulo como una forma concreta que queremos decorar. También creamos una clase llamada FormaColoreada que actuará como un decorador para agregar colores a las formas.

```
class Forma {
  constructor(color) {
    this.color = color;
  }
}

class Circulo extends Forma {
  constructor(radio = 0) {
    super();
    this.radio = radio;
  }
  
  cambiarTamano(factor) {
    this.radio *= factor;
  }
  
  toString() {
    return `Un círculo de radio ${this.radio}`;
  }
}

class FormaColoreada extends Forma {
  constructor(forma, color) {
    super();
    this.forma = forma;
    this.color = color;
  }
  
  toString() {
    return `${this.forma.toString()}, coloreado de ${this.color}`;
  }
}
```

**2. Uso del Decorador:** Creamos una instancia de un círculo y luego decoramos ese círculo con un color rojo usando la clase FormaColoreada.

```
// Crear un círculo
let circulo = new Circulo(2);
console.log(circulo.toString()); // Salida: Un círculo de radio 2

// Decorar el círculo con un color rojo
let circuloRojo = new FormaColoreada(circulo, "rojo");
console.log(circuloRojo.toString()); // Salida: Un círculo de radio 2, coloreado de rojo
```

**Código final**

```
// Clase base para todas las formas
class Forma {
  constructor(color) {
    this.color = color;
  }
}

// Clase concreta para un círculo que hereda de Forma
class Circulo extends Forma {
  constructor(radio = 0) {
    super();
    this.radio = radio;
  }
  
  cambiarTamano(factor) {
    this.radio *= factor;
  }
  
  toString() {
    return `Un círculo de radio ${this.radio}`;
  }
}

// Clase decoradora que agrega color a una forma existente
class FormaColoreada extends Forma {
  constructor(forma, color) {
    super();
    this.forma = forma;
    this.color = color;
  }
  
  toString() {
    return `${this.forma.toString()}, coloreado de ${this.color}`;
  }
}

// Crear un círculo base
let circulo = new Circulo(2);
console.log(circulo.toString()); // Salida: Un círculo de radio 2

// Decorar el círculo con un color rojo
let circuloRojo = new FormaColoreada(circulo, "rojo");
console.log(circuloRojo.toString()); // Salida: Un círculo de radio 2, coloreado de rojo
```
