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