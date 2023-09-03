**Singleton:**

Asegura que solo haya un objeto creado para una clase en particular.

En ing  eniería de software, el patrón singleton es un patrón de diseño de software que restringe la creación de instancias de una clase a una instancia "única". Esto es útil cuando se necesita exactamente un objeto para coordinar acciones en todo el sistema.

**Ejemplo:**

**Paso 1: Definición de la clase Singleton:**

```class Singleton {
  constructor() {
    // ...
  }
  // ...
}```

***Paso 2. Comprobar si ya existe una instancia de la clase***

```const instancia = this.constructor.instancia;
if (instancia) {
  return instancia;
}```

En este paso, dentro del constructor de la clase Singleton, verificamos si ya existe una instancia de la clase utilizando this.constructor.instancia. Si existe una instancia, devolvemos esa instancia en lugar de crear una nueva.

**Paso 3: Crear instancias de la clase Singleton:**

``
let s1 = new Singleton();
let s2 = new Singleton();```

En este paso, creamos dos instancias, s1 y s2, de la clase Singleton.

***Paso 4. Verificar si s1 y s2 son la misma instancia***

```console.log('¿Son lo mismo? ' + (s1 === s2));
```

Aquí verificamos si s1 y s2 son la misma instancia utilizando (s1 === s2) y mostramos el resultado en la consola.

**Paso 5. Llamar al método decir():** En este último paso, llamamos al método decir() de la instancia s1, lo que imprimirá "Diciendo..." en la consola.

```s1.decir();```

En este último paso, llamamos al método decir() de la instancia s1, lo que imprimirá "Diciendo..." en la consola.

**Código completo:**

```// Definición de la clase Singleton
class Singleton {
  constructor() {
    // Comprobar si ya existe una instancia de la clase
    const instancia = this.constructor.instancia;
    if (instancia) {
      // Si existe, devolver la instancia existente
      return instancia;
    }
    
    // Si no existe una instancia, almacenar esta como la instancia única
    this.constructor.instancia = this;
  }
  
  // Método para mostrar un mensaje
  decir() {
    console.log('Diciendo...');
  }
}

// Crear instancias de la clase Singleton
let s1 = new Singleton();
let s2 = new Singleton();

// Verificar si s1 y s2 son la misma instancia
console.log('¿Son lo mismo? ' + (s1 === s2));

// Llamar al método decir de la instancia s1
s1.decir();`

// Salida esperada:
// ¿Son lo mismo? true
// Diciendo...
``
