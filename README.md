# Patrones de Diseño en JavaScript

## Introducción a los Patrones de Diseño
Los patrones de diseño son enfoques probados y sólidos para resolver desafíos recurrentes en el diseño de software, así como en otros campos relacionados con la interacción y las interfaces. Estas técnicas ofrecen soluciones estructuradas a problemas comunes, promoviendo la eficiencia, la reusabilidad y la expresividad en el desarrollo.

Un patrón de diseño representa una solución consolidada y madura para un problema de diseño específico. Para ser considerado como tal, debe cumplir con ciertas características clave. En primer lugar, debe haber demostrado su efectividad al abordar problemas similares en situaciones previas. Además, la reutilización es un pilar fundamental en los patrones de diseño; deben ser adaptables y aplicables a una variedad de contextos y desafíos de diseño.

### Tipos de patrones de diseño:

- [Creacional](/patron/creacional.md)
- [Estructural](/patron/estructural.md)
- [Conductual](/patron/conductual.md)

## Patrones de diseño creacionales

Los patrones de diseño creacionales crearán objetos para ti en lugar de instanciar un objeto directamente.

En ingeniería de software, los patrones de diseño creacionales son patrones de diseño que se ocupan de los mecanismos de creación de objetos, tratando de crear objetos de una manera adecuada a la situación. La forma básica de creación de objetos podría dar lugar a problemas de diseño o complejidad añadida al diseño. Los patrones de diseño creacional resuelven este problema al controlar de alguna manera la creación de este objeto.

- Método de fábrica
- Fábrica abstracta
- Constructor
- Prototipo
- Singleton

### Factory Method (método de fábrica)

En diseño de software, el patrón de diseño Factory Method consiste en utilizar una clase constructora (al estilo del Abstract Factory) abstracta con unos cuantos métodos definidos y otro(s) abstracto(s): el dedicado a la construcción de objetos de un subtipo de un tipo determinado. Es una simplificación del Abstract Factory, en la que la clase abstracta tiene métodos concretos que usan algunos de los abstractos; según usemos una u otra hija de esta clase abstracta, tendremos uno u otro comportamiento.

### Ejemplo:

Tomemos un ejemplo de un punto. Tenemos una clase de puntos y tenemos que crear un punto cartesiano y un punto polar. Definiremos una fábrica de Puntos que hará este trabajo.

```
SistemaCoordenadas = {
  CARTESIANO: 0,
  POLARES: 1,
}

class Punto{
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  
  static get factory() {
    return new PuntoFactory();
  }
}
```

Ahora crearemos una clase PuntoFactory y usaremos nuestra fábrica ahora,

```
class PuntoFactory {

  static nuevoPuntoCartesiano(x, y) {
    return new Punto(x, y);
  }
  
  static nuevoPuntoPolar(rho, theta) {
    return new Punto(rho * Math.cos(theta), rho * Math.sin(theta));
  }
}

// Así es como usaremos esta clase

let punto = PuntoFactory.nuevoPuntoPolar(5, Math.Pi/2);
let punto2 = PuntoFactory.nuevoPuntoCartesiano(5, 6);
console.log(punto);
console.log(punto2);
```

### Fábrica Abstracta (abstract factory)

Crea familias o grupos de objetos comunes sin especificar sus clases concretas.

El patrón de fábrica abstracto proporciona una forma de encapsular un grupo de fábricas individuales que tienen un tema común sin especificar sus clases concretas.

### Ejemplo:

Usaremos el ejemplo de una máquina para hacer bebidas y bebidas.

```
class Bebida {
  consumir() {
  
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

class FabricaBebidas {
  preparar(cantidad)
}

class FabricaTea extends FabricaBebidas {
  hacerTea() {
    console.log('Tea creado');
    return new Tea();
  }
}

class FabricaCafe extends FabricaBebidas {
  hacerCafe() {
    console.log('Cafe creado');
    return new Cafe();
  }
}

// Y así es como podemos usarlo

let fabricaBebidaTea = FabricaTea();
let tea  fabricaBebidaTea.hacerTea();
tea.consumir()
```

### Constructor

Construye objetos complejos a partir de objetos simples.

El patrón constructor es un patrón de diseño diseñado para proporcionar una solución flexible a varios problemas de creación de objetos en la programación orientada a objetos.

### Ejemplo:

Usaremos un ejemplo ab de una clase Persona que almacena la información de una Persona.

```
class Persona {
  constructor() {
    this.direccionCalle = this.codigopostal = this.ciudad = "";
    this.nombreCompania = this.posicion = "";
    this.ingresoAnual = 0;
  }
  
  toString() {
    return (
      `Persona vive en
      ${this.direccionCalle}, ${this.ciudad}, ${this.codigopostal}
      y trabaja en ${this.nombreCompania} como
      ${this.posicion} ganando ${this.ingresoAnual}`
    );
  }
}
```

Ahora crearemos Person Builder, Person Job Builder y Person Address Builder.

```
class ConstructorPersona() {
  constructor(persona = new Persona()) {
    this.persona = persona;
  }
  
  get vive() {
    return new ConstructorDireccionPostalPersona(this.persona);
  }
  
  get trabaja() {
    return new ConstructorTrabajoPersona(this.persona);
  }
  
  build() {
    return this.persona;
  }
}

// También crearemos Constructor Trabajo Persona

class ConstructorTrabajoPersona extends ConstructorPersona {
  constructor(persona) {
    super(persona);
  }
  
  at(nombreCompania) {
    this.persona.nombreCompania = nombreCompania;
    return this;
  }
  
  asA(posicion) {
    this.person.posicion = posicion;
    return this;
  }
  
  earning(ingresoAnual) {
    this.persona.ingresoAnual = ingresoAnual;
    return this;
  }
}

// ConstructorDireccionPersona contendrá la información de dónde vive la persona
class ConstructorDireccionPersona extends ConstructorPersona {
  constructor(persona) {
    super(persona);
  }
  
  at(direccionCalle) {
    this.persona.direccionCalle = direccionCalle;
    return this;
  }
  
  withPostcode(codigopostal) {
    this.persona.codigopostal = codigopostal;
    return this;
  }
  
  in(ciudad) {
    this.persona.ciudad = ciudad;
    return this;
  }
}
```

Ahora usaremos nuestro constructor:

```
let constructorPersona = new ConstructorPersona();
let persona = ConstructorPersona.vive
  .at("Calle ABC #13 Esquina")
  .in("Santa Marta")
  .withPostcode("404599")
  .trabaja.at("Computer Systems")
  .asA("Ingeniero")
  .earning(10000)
  .build();

console.log(persona.toString());
```

### Prototipo

Crea nuevos objetos a partir de los objetos existentes.

El patrón prototipo es un patrón de diseño creacional en el desarrollo de software. Se utiliza cuando el tipo de objetos a crear está determinado por una instancia prototípica, que se clona para producir nuevos objetos.

### Ejemplo:

Usaremos el ejemplo de un automóvil.

```
class Carro {
  constructor(nombre, modelo) {
    this.nombre = nombre;
    this.modelo = modelo;
  }
  
  ajustarNombre(nombre) {
    console.log(`${nombre}`)
  }
  
  clonar(){
    return new Carro(this.nombre, this.modelo)
  }
  
// Y así es como lo usamos
let carro = new Carro();
carro.ajustarNombre('Audi');

let carro2 = carro.clonar();
carro2.ajustarNombre('BMW');
}
```

### Singleton

Asegura que solo haya un objeto creado para una clase en particular.

En ingeniería de software, el patrón singleton es un patrón de diseño de software que restringe la creación de instancias de una clase a una instancia "única". Esto es útil cuando se necesita exactamente un objeto para coordinar acciones en todo el sistema.

### Ejemplo:

Creando una clase Singleton:

```
class Singleton {
  constructor() {
    const instancia = this.constructor.instancia;
    if(instancia) {
      return instancia;
    }
    
    this.constructor.instancia = this;
  }
  
  decir(){
    console.log('Diciendo...')
  }
}

// Usemos el Singleton que hemos creado

let s1 = new Singleton();
let s2 = new Singleton();
console.log('¿Son lo mismo? ' + (s1 === s2));

s1.decir();
```

## Patrones de diseño estructural

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

## Patrones de diseño de comportamiento

Los patrones de diseño de comportamiento se ocupan específicamente de la comunicación entre objetos.

En ingeniería de software, los patrones de diseño de comportamiento son patrones de diseño que identifican patrones de comunicación comunes entre objetos. Al hacerlo, estos patrones aumentan la flexibilidad en la realización de la comunicación.

- Cadena de responsabilidad
- Comando
- Iterador
- Mediador
- Memento
- Observador
- Visitante
- Estrategia
- Estado
- Método de plantilla

### Cadena de responsabilidad

Crea una cadena de objetos. Partiendo de un punto, se detiene hasta encontrar una determinada condición.

En el diseño orientado a objetos, el patrón de cadena de responsabilidad es un patrón de diseño que consta de una fuente de objetos de comando y una serie de objetos de procesamiento.

### Ejemplo:

Usaremos un ejemplo de un juego que tiene una criatura. La criatura aumentará su defensa y ataque cuando llegue a cierto punto. Creará una cadena y el ataque y la defensa aumentarán y disminuirán.

```
class Creatura {
  constructor(nombre, ataque, defensa) {
    this.nombre = nombre;
    this.ataque = ataque;
    this.defensa = defensa;
  }
  
  toString() {
    return `${this.nombre} (${this.ataque} / ${this.defensa})`;
  }
  
}

class ModificadorCreatura {
  constructor(creatura) {
    this.creatura = creatura;
    this.siguiente = null;
  }
  
  agregar(modificador) {
    if(this.siguiente) this.siguiente.agregar(modificador);
    else this.siguiente = modificador;
  }
  
  manejar() {
    if(this.siguiente) this.siguiente.manejar();
  }
}

class ModificadorSinBonificaciones extends ModificadorCreatura {
  constructor(creatura) {
    super(creatura);
  }
  
  manejar() {
    console.log("¡no hay bonificaciones para ti!")
  }
}

```

Aumentar el ataque

```
class ModificadorDobleAtaque extends ModificadorCretura {
  constructor(creatura) {
    super(creatura);
  }
  
  manejar() {
    console.log(`Doblando ataque de ${this.creatura.nombre}`);
    this.creatura.ataque *= 2;
    super.manejar();
  }
}

```

Aumentar la defensa

```
class ModificadorAumentarDefensa extends ModificadorCreatura {
  constructor(creatura) {
    super creatura;
  }
  
  manejar() {
    if(this.creatura.ataque <= 2) {
      console.log(`Incrementando defensa de ${this.creatura.nombre}`);
      this.creatura.defensa++;
    }
    super.manejar();
  }
}
```

Así es como usaremos esto

```
let picachu = new Creatura("Picachu", 1, 1);
console.log(picachu.toString());

let raiz = new ModificadorCreatura(picachu);
raiz.agregar(new ModificadorCreatura(picachu));
raiz.agregar(new ModificadorAumentarDefensa(picachu));
raiz.manejar();

console.log(picachu.toString());

```

### Command (Comando)

En la programación orientada a objetos, el patrón de comando es un patrón de diseño de comportamiento en el que se utiliza un objeto para encapsular toda la información necesaria para realizar una acción o desencadenar un evento en un momento posterior. Esta información incluye el nombre del método, el objeto que posee el método y los valores de los parámetros del método.

### Ejemplo:

Estaremos tomando un ejemplo sencillo de una cuenta bancaria en la que damos una orden si tenemos que depositar o retirar una determinada cantidad de dinero.

```
class CuentaBanco {
  constructor(balance = 0) {
    this.balance = balance;
  }
  
  deposito(cantidad) {
    this.balance += cantidad;
    console.log(`${cantidad} depositado al balance total ${total.balance}`);
  }
  
  retirar(cantidad) {
    if(this.balance - cantidad >= CuentaBanco.limiteDescubierto) {
      this.balance -= cantidad;
      console.log('retirar');
    }
  }
  
  toString() {
    return `Balance ${this.balance}`;
  }
}

CuentaBanco.limiteDescubierto = -500;
```

Creando nuestros comandos,

```
let Accion = Object.freeze({
  deposito: 1,
  retirar: 2,
});

class ComandoCuentaBanco {
  constructor(cuenta, accion, cantidad) {
    this.cuenta = cuenta;
    this.accion = accion;
    this.cantidad = cantidad;
  }
  
  llamar() {
    switch(this.accion) {
      case Accion.deposito:
        this.cuenta.deposito(this.cantidad);
        break;
      case Accion.retirar(this.cantidad);
        break;
    }
  }
  
  undo() {
    switch(this.accion) {
      case Accion.deposito:
        this.cuenta.deposito(this.cantidad);
        break;
      case Accion.retirar:
        this.cuenta.deposito(this.cantidad);
        break;
    }
  }
}
```

Así es como usaremos esto,


```
let cuentaBancaria = new CuentaBanco(100);
let cmd = new ComandoCuentaBanco(cuentaBancaria, Accion.deposito, 50);

cmd.llamar();
console.log(cuentaBancaria.toString());

cmd.undo();
console.log(cuentaBancaria.toString());
```

### Iterador

Iterator accede a los elementos de un objeto sin exponer su representación subyacente.

En la programación orientada a objetos, el patrón de iterador es un patrón de diseño en el que se utiliza un iterador para atravesar un contenedor y acceder a los elementos del contenedor.

### Ejemplo:

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

### Mediador

El patrón mediador agrega un objeto de terceros para controlar la interacción entre dos objetos. Permite un acoplamiento flexible entre clases al ser la única clase que tiene un conocimiento detallado de sus métodos.

El patrón mediador define un objeto que encapsula cómo interactúa un conjunto de objetos. Este patrón se considera un patrón de comportamiento debido a la forma en que puede alterar el comportamiento de ejecución del programa. En la programación orientada a objetos, los programas a menudo constan de muchas clases.

Usaremos un ejemplo de una persona que usa una sala de chat. Aquí, una sala de chat actúa como mediador entre dos personas que se comunican entre sí.

```
class Persona {
  constructor(nombre) {
    this.nombre = nombre;
    this.registroChat = [];
  }
  
  recibir(enviador, mensaje) {
    let s = `${enviador}: ${mensaje}`;
    console.log(`La sesión de chat de [${this.nombre}] ${s}`);
    this.registroChat.push(s);
  }
  
  decir(mensaje) {
    this.room.broadcast(this.nombre, mensaje);
  }
  
  pm(quien, mensaje) {
    this.room.mensaje(this.nombre, quien, mensaje);
  }
}
```

Crear sala de chat,

```
class SalaChat {
  constructor() {
    this.gente = [];
  }
  
  transmision(origen, mensaje) {
    for(let p of this.gente)
      if(p.nombre !== origen) p.recibir(origen, mensaje);
  }
  
  unir(p) {
    let unirMensaje = `${p.nombre} se unió al chat`;
    this.transmision("room", unirMensaje) {
    p.room == this;
    this.gente.push(p);
    }
  }
  
  message(origen, destinacion, mensaje) {
    for(let p of this.gente)
      if(p.nombre === destino) p.recibir(origen, mensaje);
  }
}
```

Así es como usamos esto,

```
let sala = new SalaChat();
let John = new Persona("John");
let Tony = new Persona("Tony");

sala.unir(John);
sala.unir(Tony);
John.decir("¡Hola!");

let doe = new Persona("Doe");
sala.unir(doe);
doe.decir("¡Hola a todos!");
```

### Memento

Memento restaura un objeto a su estado anterior.

El patrón memento es un patrón de diseño de software que brinda la capacidad de restaurar un objeto a su estado anterior. El patrón memento se implementa con tres objetos: el originador, un cuidador y un recuerdo.

### Ejemplo:

Estaremos tomando un ejemplo de una cuenta bancaria en la que almacenamos nuestro estado anterior y tendrá la funcionalidad de deshacer.

```
class Memento {
  constructor(balance) {
    this.balance = balance;
  }
}

// Agregando cuenta de banco
class CuentaBanco {
  constructor(balance = 0) {
    this.balance = balance;
  }
  
  deposito(cantidad) {
    this.balance += cantidad;
    return new Memento(this.balance);
  }
  
  restaurar(m) {
    this.balance = m.balance;
  }
  
  toString() {
    return `Balance: ${this.balance}`;
  }
}
```

### Observador

Permite que varios objetos observadores vean un evento.

El patrón de observador es un patrón de diseño de software en el que un objeto, llamado sujeto, mantiene una lista de sus dependientes, llamados observadores, y les notifica automáticamente cualquier cambio de estado, generalmente llamando a uno de sus métodos.

### Ejemplo:

Tomaremos un ejemplo de una persona en la que si una persona se enferma, mostrará una notificación.

```
class Evento {
  contructor() {
    this.manejadores = new Map();
    this.contar = 0;
  }
  
  suscribir(manejador) {
    this.manejadores.set(++this.contar, manejador);
    return this.contar;
  }
  
  darseDeBaja(idx) {
    this.manejadores.delete(idx);
  }
  
  fuego(enviador, argumentos) {
    this.manejadores.forEach((v, k) => v(remitente, argumentos));
  }
}

class Enfermarse {
  constructor(direccion) {
    this.direccion = direccion;
  }
}

class Persona {
  constructor(direccion) {
    this.direccion = direccion;
    this.enfermarse = new Evento();
  }
  
  agarrarResfriado() {
    this.enfermarse.fuego(this, new Enfermarse(this.direccion));
  }
}
```

Así es como usaremos esto,

```
let persona = new Persona("Ruta ABC");
let sub = persona.enfermarse.suscribir((s, a) => {
  console.log(`Un doctor ha sido llamado ` + ` a ${a.direccion}`);
});

persona.agarrar.Resfriado();
persona.agarrar.Resfriado();

persona.enfermarse.darseDeBaja(sub);
persona.agarrarResfriado();
```

### Visitante

Agrega operaciones a los objetos sin tener que modificarlos.

El patrón de diseño del visitante es una forma de separar un algoritmo de una estructura de objeto en la que opera. Un resultado práctico de esta separación es la capacidad de agregar nuevas operaciones a estructuras de objetos existentes sin modificar las estructuras.

### Ejemplo:

Tomaremos un ejemplo de la clase ExpresionNumerica en el que nos da el resultado de la expresión dada.

```
class ExpresionNumerica {
  constructor(valor) {
    this.valor = valor;
  }
  
  imprimir(buffer) {
    buffer.push(this.valor.toString());
  }
}

// Creando Expresión de Suma
class ExpresionSuma {
  constructor(izquierda, derecha) {
    this.izquierda = izquierda;
    this.derecha = derecha;
  }
  
  imprimir(buffer) {
    buffer.push('(');
    this.izquierda.imprimir(buffer);
    buffer.push('+');
    this.derecha.imprimir(buffer);
    buffer.push(')');
  }
}

// Así es como usamos esto, 
// Expresión dada => 5 + (1 + 9)

let e = new ExpresionSuma(
    new ExpresionNumerica(5),
    new ExpresionSuma(
        new ExpresionNumerica(1),
        new ExpresionNumerica(9)
        )
);

let buffer = [];
e.print(buffer);

console.log(buffer.join(''));
```

### Estrategia

Permite seleccionar uno de los algoritmos en determinadas situaciones.

El patrón de estrategia es un patrón de diseño de software de comportamiento que permite seleccionar un algoritmo en tiempo de ejecución. En lugar de implementar un solo algoritmo directamente, el código recibe instrucciones en tiempo de ejecución sobre cuál usar en una familia de algoritmos.

### Ejemplo:

Tomaremos un ejemplo en el que tenemos un procesador de texto que mostrará datos en función de la estrategia (HTML o Markdown).

```
let FormatoSalida = Object.freeze({
  markdown: 0,
  html: 1,
});

class EstrategiaDeLista {
  iniciar(buffer) {}
  finalizar(buffer) {}
  agregarElementoLista(buffer, elemento) {}
}

class MarkDownEstrategiaLista extends EstrategiaLista {
  agregarElementoLista(buffer, elemento) {
    buffer.push(' * ${elemento}');
  }
}

class EstrategiaListaHTML extends EstrategiaLista {
  iniciar(buffer){
    buffer.push("<ul>");
  }
  
  finalizar(buffer){
    buffer.push("</ul>");
  }
  
  agregarElementoLista(buffer, elemento) {
    buffer.push(' <li>${item}</li>');
  }
}
```

Creando la clase ProcesadorTexto:

```
class ProcesadorTexto {
  constructor(FormatoSalida) {
    this.buffer = [];
    this.ajustarFormatoSalida(formatoSalida);
  }
  
  ajustarFormatoSalida(formatoSalida);

  ajustarFormatoSalida(formato) {
    switch (formato) {
      case FormatoSalida.markdown:
        this.estrategiaDeLista = new MarkDownEstrategiaLista();
        break;
      case FormatoSalida.html:
        this.estrategiaLista = new HTMLEstrategiaLista();
        break;
    }
  }

  agregarLista(elementos) {
    this.estrategiaLista.iniciar(this.buffer);
    for(let articulo of articulos) {
      this.estrategiaLista.agregarElementoLista(this.buffer, item);
    }
    this.estrategiaLista.finalizar(this.buffer);
  }
  
  limpiar() {
    this.buffer = [];
  }
  
  toString() {
    return this.buffer.join("\n");
  }

}
```

Así es como usaremos esto,

```
let pt = new ProcesadorTexto();

pt.ajustarFormatoSalida(FormatoSalida.markdown);
pt.agregarLista(["uno", "dos", "tres"]);
console.log(pt.toString());

pt.limpiar();
pt.ajustarFormatoSalida(FormatoSalida.html);
pt.agregarLista(["uno", "dos", "tres"]);
console.log(pt.toString());
```

### Estado

Altera el comportamiento de un objeto cuando cambia su estado interno.

El patrón de estado es un patrón de diseño de software de comportamiento que permite que un objeto altere su comportamiento cuando cambia su estado interno. Este patrón está cerca del concepto de máquinas de estados finitos.

### Ejemplo:

Estaremos tomando un ejemplo de un interruptor de luz en el que si encendemos o apagamos el interruptor, su estado cambia.

```
class EstadoEncendido extends Estado {
  constructor() {
    super();
    console.log("Luces encendidas");
  }
  
  apagar(sw) {
    console.log("Apagando luces...");
    sw.estado = new EstadoApagado();
  }
}

class EstadoApagado extends Estado {
  constructor() {
    super();
    console.log("Luz apagada...");
  }
  
  encender(sw) {
    console.log("Encendiendo luz...");
    sw.estado = new EstadoEncendido();
  }
}

```

Vamos a crear una clase Switch para usar estos estados de encendido y apagado.

```
class Switch {
  constructor() {
    this.estado = new EstadoApagado();
  }
  
  encender() {
    this.estado.encender(this);
  }
  
  apagar() {
    this.state.off(this);
  }
}

class Estado {
  constructor() {
    if(this.constructor === Estado) throw new Error("¡Abstracto!")ñ
  }
  
  encender(sw) {
    console.log("La luz está encendida.");
  }
  
  apagar(sw) {
    console.log("La luz está apagada");
  }
}

// Usemos la clase Switch
let swtich = new Switch();
switch.encender();
switch.apagar();
```

### Método de plantilla

Define el esqueleto de un algoritmo como una clase abstracta, cómo debe realizarse.

Template Method (método de plantilla) es un método en una superclase, generalmente una superclase abstracta, y define el esqueleto de una operación en términos de una serie de pasos de alto nivel.

### Ejemplo:

Tomaremos un ejemplo de un juego de ajedrez,

```
class Juego {
  constructor(numeroJugadores) {
    this.numeroDeJugadores = numeroDeJugadores;
    this.jugadorActual = 0;
  }
  
  ejecutar() {
    this.iniciar();
    while(!this.hayaGanador) {
      this.tomarTurno();
    }
    console.log(`Jugador ${this.jugadorGanador} gana.`);
  }
  iniciar() {}
  get hayaJugador {}
  tomarTurno();
  get jugadorGanador() {}
}
```

Creando nuestra clase Ajedrez,

```
class Ajedrez extends Juego {
  constructor() {
    super(2);
    this.turnosMaximos = 10;
    this.turno = 1;
  }
  
  iniciar() {
    console.log(`Iniciando un juego de ajedrez con ${this.numeroDeJugadores} jugadores.`);
  }
  
  get hayaGanador() {
    return this.turno === this.turnosMaximos;
  }
  
  tomarTurno(){
    console.log(`Turno ${this.turno} tomado por jugador ${this.jugadorActual}`);
    this.jugadorActual = (this.jugadorActual + 1) % this.numeroDeJugadores;
  }
  
  get jugadorGanador() {
    return this.jugadorActual;
  }
  
}
```

Así usaremos esto:

```
let ajedrez = new Ajedrez();
ajedrez.ejecutar();
```