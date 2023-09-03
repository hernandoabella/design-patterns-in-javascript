### Facade (fachada)

El patrón de fachada (también deletreado fachada) es un patrón de diseño de software comúnmente utilizado en la programación orientada a objetos. De manera análoga a una fachada en arquitectura, una fachada es un objeto que sirve como una interfaz frontal que enmascara un código subyacente o estructural más complejo. Proporciona una interfaz simplificada para acceder a un conjunto de subsistemas o clases relacionadas, lo que facilita la interacción con el sistema sin necesidad de conocer los detalles internos.

**Ejemplo:**

En este ejemplo, vamos a simular el funcionamiento de una computadora utilizando el patrón de fachada. La computadora consta de varios componentes, como CPU, memoria y disco duro. La fachada ComputerFacade simplificará la interacción con estos componentes.

1. Definimos las clases para los componentes de la computadora: CPU, Memoria y DiscoDuro. Estas clases tienen métodos para realizar diversas operaciones, como congelar la CPU, cargar datos en la memoria y leer desde el disco duro.

```
class CPU {
  congelar() { console.log("CPU Congelada...") }
  saltar(posicion) { console.log("Saltar a la posición " + posicion) }
  ejecutar() { console.log("Ejecutar CPU...") }
}

class Memoria {
  cargar(posicion, dato) { console.log("Cargar en posición " + posicion + " el dato: " + dato) }
}

class DiscoDuro {
  leer(lba, tamano) { console.log("Leer desde LBA " + lba + " con tamaño " + tamano) }
}
```

2. Creamos la fachada ComputerFacade que proporcionará una interfaz simplificada para interactuar con los componentes de la computadora. En el método iniciar(), se utilizan los componentes de manera coherente y enmascaran los detalles complejos.

```
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
```

3.Finalmente, creamos una instancia de ComputerFacade y utilizamos su método iniciar() para simular el arranque de la computadora.

```
let computadora = new ComputerFacade();
computadora.iniciar();
```

**Código final:**

```
// Definición de la clase CPU que representa la unidad central de procesamiento.
class CPU {
  congelar() { console.log("CPU Congelada...") } // Método para congelar la CPU.
  saltar(posicion) { console.log("Saltar a la posición " + posicion) } // Método para saltar a una posición específica.
  ejecutar() { console.log("Ejecutar CPU...") } // Método para ejecutar la CPU.
}

// Definición de la clase Memoria que representa la memoria de la computadora.
class Memoria {
  cargar(posicion, dato) { console.log("Cargar en posición " + posicion + " el dato: " + dato) } // Método para cargar datos en la memoria.
}

// Definición de la clase DiscoDuro que representa el disco duro de la computadora.
class DiscoDuro {
  leer(lba, tamano) { console.log("Leer desde LBA " + lba + " con tamaño " + tamano) } // Método para leer desde el disco duro.
}

// Definición de la clase ComputerFacade que actúa como la fachada para interactuar con los componentes de la computadora.
class ComputerFacade {
  constructor() {
    this.procesador = new CPU(); // Crear una instancia de la CPU.
    this.ram = new Memoria(); // Crear una instancia de la Memoria.
    this.hd = new DiscoDuro(); // Crear una instancia del Disco Duro.
  }

  iniciar() {
    this.procesador.congelar(); // Congelar la CPU.
    this.ram.cargar(this.DIRECCION_ARRANQUE, this.hd.leer(this.SECTOR_ARRANQUE, this.TAMANO_SECTOR)); // Cargar datos en la memoria desde el disco duro.
    this.procesador.saltar(this.DIRECCION_ARRANQUE); // Saltar a la dirección de inicio.
    this.procesador.ejecutar(); // Ejecutar la CPU.
  }
}

// Crear una instancia de ComputerFacade y utilizarla para simular el arranque de la computadora.
let computadora = new ComputerFacade();
computadora.iniciar();

// Salida esperada:
// CPU Congelada...
// Cargar en posición DIRECCION_ARRANQUE el dato: Leer desde LBA SECTOR_ARRANQUE con tamaño TAMANO_SECTOR
// Saltar a la posición DIRECCION_ARRANQUE
// Ejecutar CPU...
```
