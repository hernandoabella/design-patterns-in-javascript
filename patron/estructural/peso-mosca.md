**Peso Mosca (Flyweight)**

El patrón Peso Mosca es utilizado para minimizar el uso de memoria al crear objetos similares compartiendo la mayor cantidad de datos posible entre ellos. Esto significa que, en lugar de crear múltiples instancias de objetos con datos idénticos, se utiliza una instancia compartida para representar esos datos en común. Esto reduce significativamente la cantidad de memoria utilizada, especialmente cuando se trabaja con grandes cantidades de objetos similares.

**Ejemplo:**

**Paso 1: Definición de las Clases Usuario y Usuario2**: En este paso, definimos dos clases: Usuario y Usuario2. La primera representa un usuario simple con un nombre completo, mientras que la segunda implementa el patrón Peso Mosca para reducir el uso de memoria al compartir nombres completos similares.

```
// Definición de la clase Usuario
class Usuario {
  constructor(nombreCompleto) {
    this.nombreCompleto = nombreCompleto;
  }
}

// Definición de la clase Usuario2 que implementa el patrón Peso Mosca
class Usuario2 {
  constructor(nombreCompleto) {
    let obtenerOAgregar = function(s) {
      let idx = Usuario2.strings.indexOf(s);
      if (idx !== -1) return idx;
      else {
        Usuario2.strings.push(s);
        return Usuario2.strings.length - 1;
      }
    };
    this.nombres = nombreCompleto.split(' ').map(obtenerOAgregar);
  }
}

Usuario2.strings = [];
```

**Paso 2: Funciones Auxiliares:** En este paso, creamos dos funciones auxiliares: obtenerEnteroAleatorio para obtener números enteros aleatorios y cadenaTextoAleatoria para generar cadenas de texto aleatorias.

```
// Funciones auxiliares
function obtenerEnteroAleatorio(max) {
  return Math.floor(Math.random() * Math.floor(max));
}

function cadenaTextoAleatoria() {
  let resultado = [];
  for (let x = 0; x < 10; ++x)
    resultado.push(String.fromCharCode(65 + obtenerEnteroAleatorio(26)));
  return resultado.join('');
}
```

**Paso 3: Creación de Nombres Aleatorios:** En este paso, creamos dos arreglos, nombres y apellidos, que contienen nombres y apellidos generados aleatoriamente que servirán para crear los usuarios.

```
// Creación de Nombres Aleatorios
let nombres = apellidos = [];
for (let i = 0; i < 100; ++i) {
  nombres.push(cadenaTextoAleatoria());
  apellidos.push(cadenaTextoAleatoria());
}
```

**Paso 4: Creación de Usuarios:** En este paso, creamos dos arreglos, usuarios y usuarios2, que contendrán los usuarios creados. Recorremos los arreglos de nombres y apellidos para crear 10,000 usuarios tanto sin el patrón Peso Mosca como con él.

```
let usuarios = [];
let usuarios2 = [];

// Creación de Usuarios
for (let nombre of nombres) {
  for (let apellido of apellidos) {
    usuarios.push(new Usuario(`${nombre} ${apellido}`));
    usuarios2.push(new Usuario2(`${nombre} ${apellido}`));
  }
}
```

**Paso 5: Comparación de Uso de Memoria:** En este paso, comparamos el uso de memoria entre los usuarios sin el patrón Peso Mosca y los usuarios con él utilizando JSON.stringify. Imprimimos los resultados en la consola.

```
// Comparación de Uso de Memoria
console.log(`10,000 usuarios ocupan aproximadamente ${JSON.stringify(usuarios).length} caracteres`);
let largoUsuarios2 = [usuarios2, Usuario2.strings].map(x => JSON.stringify(x).length).reduce((x, y) => x + y);
console.log(`10,000 usuarios con Peso Mosca ocupan ~${largoUsuarios2} caracteres`);
```

**Código final:**

```
// Definición de la clase Usuario
class Usuario {
  constructor(nombreCompleto) {
    this.nombreCompleto = nombreCompleto;
  }
}

// Definición de la clase Usuario2 que implementa el patrón Peso Mosca
class Usuario2 {
  constructor(nombreCompleto) {
    let obtenerOAgregar = function(s) {
      let idx = Usuario2.strings.indexOf(s);
      if (idx !== -1) return idx;
      else {
        Usuario2.strings.push(s);
        return Usuario2.strings.length - 1;
      }
    };
    this.nombres = nombreCompleto.split(' ').map(obtenerOAgregar);
  }
}

Usuario2.strings = [];

// Funciones auxiliares
function obtenerEnteroAleatorio(max) {
  return Math.floor(Math.random() * Math.floor(max));
}

function cadenaTextoAleatoria() {
  let resultado = [];
  for (let x = 0; x < 10; ++x)
    resultado.push(String.fromCharCode(65 + obtenerEnteroAleatorio(26)));
  return resultado.join('');
}

// Creación de Nombres Aleatorios
let nombres = apellidos = [];
for (let i = 0; i < 100; ++i) {
  nombres.push(cadenaTextoAleatoria());
  apellidos.push(cadenaTextoAleatoria());
}

let usuarios = [];
let usuarios2 = [];

// Creación de Usuarios
for (let nombre of nombres) {
  for (let apellido of apellidos) {
    usuarios.push(new Usuario(`${nombre} ${apellido}`));
    usuarios2.push(new Usuario2(`${nombre} ${apellido}`));
  }
}

// Comparación de Uso de Memoria
console.log(`10,000 usuarios ocupan aproximadamente ${JSON.stringify(usuarios).length} caracteres`); // 10,000 usuarios ocupan aproximadamente 1720001 caracteres
let largoUsuarios2 = [usuarios2, Usuario2.strings].map(x => JSON.stringify(x).length).reduce((x, y) => x + y);
console.log(`10,000 usuarios con Peso Mosca ocupan ~${largoUsuarios2} caracteres`); // 10,000 usuarios con Peso Mosca ocupan ~838602 caracteres
```
