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