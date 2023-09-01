## Patrones de diseño estructurales

Estos patrones se refieren a la composición de clases y objetos. Usan herencia para componer interfaces.

En ingeniería de software, los patrones de diseño estructural son patrones de diseño que facilitan el diseño al identificar una forma sencilla de realizar relaciones entre entidades.

- Adaptador
- Bridge
- Compuesto
- Decorador
- Facade
- Peso mosca
- Apoderado

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

### Composite (Compuesto)

Compone objetos para que puedan ser manipulados como objetos individuales.

El patrón compuesto describe un grupo de objetos que se tratan de la misma manera que una sola instancia del mismo tipo de objeto.

### Ejemplo:

Usaremos ejemplos de trabajo:

```
class Empleador {
  constructor(nombre, rol) {
    this.nombre = nombre;
    this.rol = rol;
  }
  
  imprimir() {
    console.log("nombre": + this.nombre + "tiempo relajado: ");
  }
}

// Creando un grupo de empleados
class GrupoEmpleados {
  constructor(nombre, compuesto = []) {
    console.log(nombre);
    this.nombre = nombre;
    this.compuesto = compuesto;
  }
  
  imprimir() {
    console.log(this.nombre);
    this.compuesto.forEach(emp => {
      emp.imprimir();
    })
  }
}

// Usemos estas clases
let hernando = new Empleador("hernando", "desarollador")
let albert = new Empleador("albert", "desarrollador")
let grupoDesarrolador = new GrupoEmpleados("Desarrolladores", [hernando, albert]);
```

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

### Facade (fachada)

Proporciona una interfaz simplificada para código complejo.

El patrón de fachada (también deletreado fachada) es un patrón de diseño de software comúnmente utilizado en la programación orientada a objetos. De manera análoga a una fachada en arquitectura, una fachada es un objeto que sirve como una interfaz frontal que enmascara un código subyacente o estructural más complejo.

### Ejemplo:

Tomemos un ejemplo de un cliente que interactúa con la computadora.

```
class CPU {
  congelar() {console.log("Congelada...")}
  saltar(posicion) {console.log("Ir...")}
  ejecutar() {console.log("Correr...")}
}

class Memoria {
  cargar(posicion, dato) {console.log("Cargar...")}
}

class DiscoDuro {
  leer(lba, tamano) {console.log("leer...")}
}

// Creemos la fachada
class ComputerFacade {
  constructor() {
    this.procesador = new CPU();
    this.ram = new Memoria();
    this.hd = new DiscoDuro();
  }
  
  iniciar() {
    this.procesador.congelar();
    this.ram.cargar(this.DIRECCION_ARRANQUE, this.hd.leer(this.SECTOR_ARRANQUE, this.TAMANO_SECTOR));
    this.procesador.saltar(this.DIRECCION_ARRANQUE);
    this.procesador.ejecutar();
  }
}

// Usemos esta fachada
let computadora = new ComputerFacade();
computadora.iniciar();
```

### Peso Mosca

Reduce el costo de memoria de crear objetos similares.

Un peso mosca es un objeto que minimiza el uso de la memoria al compartir la mayor cantidad de datos posible con otros objetos similares.

### Ejemplo:

Tomemos el ejemplo de un usuario. Tengamos varios usuarios con el mismo nombre. Podemos guardar nuestra memoria almacenando un nombre y dandole una referencia a los usuarios que tienen los mismos nombres.

```
class Usuario {
  constructor(nombreCompleto) {
    this.nombreCompleto = nombreCompleto;
  }
}

class Usuario2 {
  constructor(nombreCompleto) {
    let obtenerOAgregar = function(s) {
      let idx = Usuario2.strings.idexOf(s);
      if(idx !== 1) return idx;
      else {
        Usuario2.strings.push(s);
        return Usuario.strings.length -1;
      }
    };
    this.nombres = nombreCompleto.split(' ').map(obtenerOAgregar;)
  }
}

Usuario2.strings = [];

function obtenerEnteroAletario = function(max) {
  return Math.floor(Math.random() * Math.floor(max));
}

let cadenaTextoAleatorio = function() {
  let resultado = [];
  for(let x = 0; x < 10; ++x)
    resultado.push(String.fromCharCode(65 + getRandomInt(26)));
  return resultado.join('');  
};
```

Así es como usaremos esto.

Ahora haremos una comparación de memoria sin Peso mosca y con Peso mosca, haciendo 10k usuarios.

```
let usuarios = usuarios2 = nombres = apellidos = [];
for(let i = 0; i < 100; ++i) {
  nombres.push(cadenaTextoAleatoria());
  apellidos.push(cadenaTextoAleatoria());
}

// Creand 10k usuarios
for(let nombre of nombres) {
  for(let apellido of apellidos) {
    usuarios.push(new Usuario(`${nombre} ${apellido}`));
    usuarios2.push(new Usuario2(`${nombre} ${apellido}`));
  }
}

console.log(`10k usuarios ocupan aproximadamente ${JSONN.stringyfy(usuarios).length} carácteres`);

let largousuarios2 = [usuarios2, Usuario2.strings].map(x => JSON.stringify(x).length).reduce((x, y) => x + y);

console.log(`10k Los usuarios de peso mosca toman ~${largousuarios2} carácteres`)
```

### Proxy

Al usar Proxy, una clase puede representar la funcionalidad de otra clase.

El patrón proxy es un patrón de diseño de software. Un proxy, en su forma más general, es una clase que funciona como una interfaz para otra cosa.

### Ejemplo:

Tomemos el ejemplo del valor de proxy.

```
class Porcentaje {
  constructor(porcentaje) {
    this.porcentaje = porcentaje;
  }
  
  toString() {
    return `${this.porcentaje}&`';
  }
  
  valueOf() {
    return this.porcentae / 100;
  }
}

// Usemos este ejemplo de Porcentaje
let porcentajeCinco = new Porcentaje(5);
console.log(porcentajeCinco.toString());
console.log(`El 5% de 50% es ${50 * porcentajeCinco}`);
```