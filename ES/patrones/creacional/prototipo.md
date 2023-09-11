### Prototipo

Crea nuevos objetos a partir de los objetos existentes.

El patrón prototipo es un patrón de diseño creacional en el desarrollo de software. Se utiliza cuando el tipo de objetos a crear está determinado por una instancia prototípica, que se clona para producir nuevos objetos.

**Ejemplo:**

Usaremos el ejemplo de un automóvil.

**Paso 1: Definición de la clase Carro (Prototipo)**

```
class Carro {
  constructor(nombre, modelo) {
    this.nombre = nombre;
    this.modelo = modelo;
  }

  // ... (Métodos de la clase)
}
```

**Paso 2: Método para ajustar el nombre del carro**

```
// Método para ajustar el nombre del carro
  ajustarNombre(nombre) {
    this.nombre = nombre;
    console.log(`Nombre del carro ajustado a: ${this.nombre}`);
  }
```

**Paso 3: Método para clonar el carro (crear una copia)**

```
// Método para clonar el carro (crear una copia)
  clonar() {
    // Crear una nueva instancia de Carro con los mismos atributos
    return new Carro(this.nombre, this.modelo);
  }
```

**Paso 4: Uso del patrón Prototipo**

```
// Uso del patrón Prototipo
const carroOriginal = new Carro('Audi', 'A3');

// Clonar el carro original para crear una nueva instancia
const carroClonado = carroOriginal.clonar();
carroClonado.ajustarNombre('BMW');
```

**Paso 5: Verificar que los carros son diferentes**

```
// Verificar que los carros son diferentes
console.log('Carro Original:', carroOriginal.nombre, carroOriginal.modelo);
console.log('Carro Clonado:', carroClonado.nombre, carroClonado.modelo);
```

Este código muestra cómo usar el patrón Prototipo para crear una copia de un objeto existente (carroOriginal) y ajustar sus atributos (nombre) sin afectar al objeto original. Al final, se verifica que los dos carros sean diferentes y que el clon haya funcionado correctamente.

**Código final:**

```
// Definición de la clase Carro (Prototipo)
class Carro {
  constructor(nombre, modelo) {
    this.nombre = nombre;
    this.modelo = modelo;
}

  // Método para ajustar el nombre del carro
  ajustarNombre(nombre) {
    this.nombre = nombre;
    console.log(`Nombre del carro ajustado a: ${this.nombre}`);
  }

  // Método para clonar el carro (crear una copia)
  clonar() {
    // Crear una nueva instancia de Carro con los mismos atributos
    return new Carro(this.nombre, this.modelo);
  }
}

// Uso del patrón Prototipo
const carroOriginal = new Carro('Audi', 'A3');

// Clonar el carro original para crear una nueva instancia
const carroClonado = carroOriginal.clonar();
carroClonado.ajustarNombre('BMW');

// Verificar que los carros son diferentes
console.log('Carro Original:', carroOriginal.nombre, carroOriginal.modelo);
console.log('Carro Clonado:', carroClonado.nombre, carroClonado.modelo);

// Salida esperada:
// Nombre del carro ajustado a: BMW
// Carro Original: Audi A3
// Carro Clonado: BMW A3
```
