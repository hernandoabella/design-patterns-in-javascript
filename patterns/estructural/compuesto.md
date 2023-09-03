**Composite (Compuesto)**

El patrón Composite se utiliza para componer objetos en estructuras de árbol para representar jerarquías de objetos. Esto permite que los objetos individuales y las composiciones de objetos sean tratados de la misma manera, lo que facilita su manipulación.

**Ejemplo:**

**1. Definición de Clases:** En este ejemplo, creamos dos clases: Empleador para representar a los empleados individuales y GrupoEmpleados para representar grupos de empleados.

```
class Empleador {
  constructor(nombre, rol) {
    this.nombre = nombre;
    this.rol = rol;
  }
  
  imprimir() {
    console.log("Nombre: " + this.nombre + ", Rol: " + this.rol);
  }
}

class GrupoEmpleados {
  constructor(nombre, compuesto = []) {
    this.nombre = nombre;
    this.compuesto = compuesto;
  }
  
  imprimir() {
    console.log("Grupo: " + this.nombre);
    this.compuesto.forEach(emp => {
      emp.imprimir();
    })
  }
}
```

**2. Creación de Empleados y Grupos:** Creamos instancias de empleados individuales y luego los agrupamos en un GrupoEmpleados.

```
// Creando empleados individuales
let hernando = new Empleador("Hernando", "Desarrollador");
let albert = new Empleador("Albert", "Desarrollador");

// Creando un grupo de empleados y agregando empleados individuales
let grupoDesarrolladores = new GrupoEmpleados("Desarrolladores", [hernando, albert]);
```

**3. Imprimir la Estructura Jerárquica:** Utilizamos el método imprimir() para mostrar la estructura jerárquica, que incluye tanto empleados individuales como grupos de empleados.

```
// Imprimir la estructura jerárquica
grupoDesarrolladores.imprimir();
```

**Código final:**

```
class Empleador {
  constructor(nombre, rol) {
    this.nombre = nombre;
    this.rol = rol;
  }
  
  imprimir() {
    console.log(`Nombre: ${this.nombre}, Rol: ${this.rol}`);
  }
}

class GrupoEmpleados {
  constructor(nombre, compuesto = []) {
    this.nombre = nombre;
    this.compuesto = compuesto;
  }
  
  imprimir() {
    console.log(`Grupo: ${this.nombre}`);
    this.compuesto.forEach(emp => {
      emp.imprimir();
    })
  }
}

// Creando empleados individuales
let hernando = new Empleador("Hernando", "Desarrollador");
let albert = new Empleador("Albert", "Desarrollador");

// Creando un grupo de empleados y agregando empleados individuales
let grupoDesarrolladores = new GrupoEmpleados("Desarrolladores", [hernando, albert]);

// Imprimir la estructura jerárquica
grupoDesarrolladores.imprimir();
// Salida Esperada:
// Grupo: Desarrolladores
// Nombre: Hernando, Rol: Desarrollador
// Nombre: Albert, Rol: Desarrollador
```
