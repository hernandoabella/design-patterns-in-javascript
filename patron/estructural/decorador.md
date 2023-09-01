### Decorador

Agrega o anula dinámicamente el comportamiento de un objeto.

El patrón decorador es un patrón de diseño que permite agregar comportamiento a un objeto individual, de forma dinámica, sin afectar el comportamiento de otros objetos de la misma clase.

### Ejemplo:

Tomaremos el ejemplo del color y las formas. Si tenemos que dibujar un círculo crearemos métodos y dibujaremos un círculo. Si tenemos que dibujar un círculo rojo. Ahora el comportamiento se agrega a un objeto y el patrón Decorator (decorador) me ayudará en eso.

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
    return `Un circulo ${this.radio}`;
  }
}

// Creemos la clase FormaColoreada
class FormaColoreada extends Forma {
  constructor(forma, color) {
    super();
    this.forma = forma;
    this.color = color;
  }
  
  toString() {
    return `${this.forma.toString()}` + `tiene el color ${this.color}`;
  }
}

// Así es como la usamos
let circulo = Circulo(2);
console.log(circulo);

let circuloRojo = new FormaColoreada(circulo, "rojo");
console.log(circuloRojo.toString());
```