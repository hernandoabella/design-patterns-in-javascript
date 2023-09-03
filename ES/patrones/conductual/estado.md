### Estado

Altera el comportamiento de un objeto cuando cambia su estado interno.

El patrón de estado es un patrón de diseño de software de comportamiento que permite que un objeto altere su comportamiento cuando cambia su estado interno. Este patrón está cerca del concepto de máquinas de estados finitos.

**Ejemplo:**

Estaremos tomando un ejemplo de un interruptor de luz en el que si encendemos o apagamos el interruptor, su estado cambia.

Este es un ejemplo del patrón de diseño "State", que permite que un objeto cambie su comportamiento cuando cambia su estado interno. Aquí tienes el código con comentarios que muestran cada paso:

**Paso 1:** Creamos dos clases de estado, EstadoEncendido y EstadoApagado, que heredan de la clase base Estado. Cada clase de estado define cómo debe comportarse el interruptor cuando está en ese estado particular.

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

**Paso 2:** Creamos la clase Switch, que contiene un estado interno y métodos encender() y apagar() para cambiar el estado. Inicializamos el interruptor con el estado apagado.

```
class Switch {
  constructor() {
    this.estado = new EstadoApagado();
  }
  
  encender() {
    this.estado.encender(this);
  }
  
  apagar() {
    this.estado.apagar(this);
  }
}

```

**Paso 3:** Creamos la clase base abstracta Estado, que define los métodos encender() y apagar(). Las clases de estado concretas deben implementar estos métodos.

```
class Estado {
  constructor() {
    if (this.constructor === Estado) throw new Error("¡Abstracto!");
  }
  
  encender(sw) {
    console.log("La luz está encendida.");
  }
  
  apagar(sw) {
    console.log("La luz está apagada.");
  }
}

```

**Paso 4:** Creamos una instancia de la clase Switch y probamos sus métodos para cambiar el estado de las luces. Primero, encendemos las luces y luego las apagamos.

```
let interruptor = new Switch();
interruptor.encender();
interruptor.apagar();
```

Este ejemplo demuestra cómo el patrón de diseño "State" permite que un objeto, en este caso, un interruptor de luz, cambie su comportamiento según su estado interno (encendido o apagado). Cada estado tiene sus propios comportamientos definidos en las clases de estado concretas.
  

**Código final:**

```
// Creamos dos clases de estado

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

// Creamos la clase Switch

class Switch {
  constructor() {
    this.estado = new EstadoApagado(); // Inicializamos con el estado apagado
  }
  
  encender() {
    this.estado.encender(this); // Llamamos al método de encendido del estado actual
  }
  
  apagar() {
    this.estado.apagar(this); // Llamamos al método de apagado del estado actual
  }
}

// Creamos la clase base abstracta Estado

class Estado {
  constructor() {
    if (this.constructor === Estado) throw new Error("¡Abstracto!"); // Evita instanciar directamente
  }
  
  encender(sw) {
    console.log("La luz está encendida.");
  }
  
  apagar(sw) {
    console.log("La luz está apagada.");
  }
}

// Creamos una instancia de la clase Switch y probamos sus métodos

let interruptor = new Switch();
interruptor.encender(); // Encendemos las luces
interruptor.apagar();  // Apagamos las luces
```