### Composite (Compuesto)

Compone objetos para que puedan ser manipulados como objetos individuales.

El patrón compuesto describe un grupo de objetos que se tratan de la misma manera que una sola instancia del mismo tipo de objeto.

### Ejemplo:

Usaremos ejemplos de trabajo:

```
class Empleador {
  constructor(nombre, rol) {
    this.nombre = nombre;
    this.rol = rol;
  }
  
  imprimir() {
    console.log("nombre": + this.nombre + "tiempo relajado: ");
  }
}

// Creando un grupo de empleados
class GrupoEmpleados {
  constructor(nombre, compuesto = []) {
    console.log(nombre);
    this.nombre = nombre;
    this.compuesto = compuesto;
  }
  
  imprimir() {
    console.log(this.nombre);
    this.compuesto.forEach(emp => {
      emp.imprimir();
    })
  }
}

// Usemos estas clases
let hernando = new Empleador("hernando", "desarollador")
let albert = new Empleador("albert", "desarrollador")
let grupoDesarrolador = new GrupoEmpleados("Desarrolladores", [hernando, albert]);
```