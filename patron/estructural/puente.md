

### Bridge (Puente)

Separa la abstracción de la implementación para que las dos puedan variar de forma independiente.

Puente es un patrón de diseño estructural que le permite dividir una clase grande o un conjunto de clases estrechamente relacionadas en dos jerarquías separadas, abstracción e implementación, que se pueden desarrollar de forma independiente.

### Ejemplo:

Crearemos clases de Renderer para renderizar múltiples formas geométricas:

```
class RenderizadorVectores {
  renderizarCirculo(radio) {
    console.log(`Dibujando un circulo de radio ${radio}`);
  }
}

class RenderizadorRaster {
  rasterizarCirculo(radio) {
    console.log(`Dibujando pixeles para circulo de radio ${radio}`);
  }
}

class Forma {
  constructor(renderizador) {
    this.renderizador = renderizador;
  }
}

class Circulo extends Forma {
  constructor(renderizador, radio) {
    super(renderizador);
    this.radio = radio;
  }
  
  dibujar() {
    this.renderizador.renderizarCirculo(this.radio);
  }
  
  cambiarTamano(factor) {
    this.radius *= factor;
  }
}

// Así es como utilizaremos esto:
let raster = new RenderizadorRaster();
let vector = new RenderizadorVector();
let circulo = new Circulo(vector, 5);

circulo.dibujar();
circulo.cambiarTamano(2);
circulo.dibujar();

```