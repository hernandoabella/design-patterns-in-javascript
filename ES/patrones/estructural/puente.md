

**Bridge (Puente)**

El patrón de diseño Bridge se utiliza para separar la abstracción de la implementación, permitiendo que ambas puedan cambiar de forma independiente. En otras palabras, el patrón Bridge se utiliza cuando se desea evitar una conexión rígida entre una clase abstracta y sus clases concretas, permitiendo que ambas evolucionen de manera independiente sin afectar a la otra.

**Ejemplo:**

En este ejemplo, crearemos clases para renderizar formas geométricas. Utilizaremos dos clases de renderizador: RenderizadorVectores y RenderizadorRaster. Luego, crearemos una clase abstracta Forma y una clase Circulo que hereda de Forma. La clave del patrón Bridge es que Forma tiene una referencia a un renderizador y delega la tarea de renderizar al renderizador concreto.

**Paso 1. Definición de las Clases de Renderizadores:** En este paso, creamos las clases RenderizadorVectores y RenderizadorRaster que representan diferentes métodos de renderización.

```
class RenderizadorVectores {
  renderizarCirculo(radio) {
    console.log(`Dibujando un círculo de radio ${radio}`);
  }
}

class RenderizadorRaster {
  rasterizarCirculo(radio) {
    console.log(`Dibujando pixeles para círculo de radio ${radio}`);
  }
}
```

**Paso 2. Definición de la Clase Abstracta Forma:** En este paso, creamos la clase abstracta Forma que actuará como nuestra abstracción. Esta clase tiene un atributo renderizador que es una referencia al renderizador que utilizaremos para dibujar la forma.

class Forma {
  constructor(renderizador) {
    this.renderizador = renderizador;
  }
}

**Paso 3. Definición de la Clase Circulo:** En este paso, creamos la clase Circulo que hereda de Forma. La clase Circulo tiene un atributo radio que representa el radio del círculo.

```
class Circulo extends Forma {
  constructor(renderizador, radio) {
    super(renderizador);
    this.radio = radio;
  }
}
```

**Paso 4 Implementación del Método dibujar:** En la clase Circulo, implementamos el método dibujar. Este método delega la tarea de renderizar al renderizador concreto (RenderizadorVectores o RenderizadorRaster) a través de la referencia this.renderizador.

```
dibujar() {
  this.renderizador.renderizarCirculo(this.radio);
}
```

**Paso 5. Creación de Instancias de Renderizadores y Circulo:** En este paso, creamos instancias de los renderizadores RenderizadorVectores y RenderizadorRaster. Luego, creamos una instancia de Circulo llamada circulo y le proporcionamos el renderizador de vectores y un radio de 5.

```
let raster = new RenderizadorRaster();
let vector = new RenderizadorVectores();
let circulo = new Circulo(vector, 5);
```

**Paso 6. Dibujar el Círculo y Cambiar su Tamaño:** Llamamos al método dibujar en la instancia de circulo, lo que resulta en la impresión del mensaje correspondiente al renderizador de vectores. Luego, cambiamos el tamaño del círculo llamando al método cambiarTamano, duplicando su radio.

```
circulo.dibujar();
circulo.cambiarTamano(2);
```

**Paso 7. Dibujar el Círculo Después del Cambio de Tamaño:** Llamamos nuevamente al método dibujar en la instancia de circulo, lo que resulta en la impresión del mensaje actualizado después del cambio de tamaño.

```
circulo.dibujar();
```

**Código final:**

```
// Definición de las Clases de Renderizadores
class RenderizadorVectores {
  renderizarCirculo(radio) {
    console.log(`Dibujando un círculo de radio ${radio}`);
  }
}

class RenderizadorRaster {
  rasterizarCirculo(radio) {
    console.log(`Dibujando pixeles para círculo de radio ${radio}`);
  }
}

// Definición de la Clase Abstracta `Forma`
class Forma {
  constructor(renderizador) {
    this.renderizador = renderizador;
  }
}

// Definición de la Clase `Circulo`
class Circulo extends Forma {
  constructor(renderizador, radio) {
    super(renderizador);
    this.radio = radio;
  }

  // Implementación del Método `dibujar`
  dibujar() {
    this.renderizador.renderizarCirculo(this.radio);
  }

  cambiarTamano(factor) {
    this.radio *= factor;
  }
}

// Creación de Instancias de Renderizadores y Circulo
let raster = new RenderizadorRaster();
let vector = new RenderizadorVectores();
let circulo = new Circulo(vector, 5);

// Dibujar el Círculo y Cambiar su Tamaño
circulo.dibujar();
circulo.cambiarTamano(2);

// Dibujar el Círculo Después del Cambio de Tamaño
circulo.dibujar();

// Salida esperada:
// Dibujando un círculo de radio 5
// Dibujando un círculo de radio 10
```