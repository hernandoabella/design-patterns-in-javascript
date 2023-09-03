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