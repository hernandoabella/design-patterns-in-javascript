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