### Proxy (Proxy)

El patrón Proxy permite que una clase represente la funcionalidad de otra clase, actuando como un intermediario o "proxy" entre el cliente y el objeto real. Esto puede ser útil para controlar el acceso al objeto real, realizar operaciones adicionales antes o después de acceder al objeto real o incluso reemplazar el objeto real por completo.

**Ejemplo:**

Imaginemos un ejemplo de un objeto Proxy llamado Porcentaje que se utiliza para representar porcentajes. Este Proxy permitirá manipular los valores de porcentaje y realizar operaciones matemáticas en ellos.

```
class Porcentaje {
  constructor(porcentaje) {
    this.porcentaje = porcentaje;
  }
  
  toString() {
    return `${this.porcentaje}%`;
  }
  
  valueOf() {
    return this.porcentaje / 100;
  }
}

// Utilicemos el objeto Proxy Porcentaje
let porcentajeCinco = new Porcentaje(5);
console.log(porcentajeCinco.toString()); // Salida: "5%"
console.log(`El 5% de 50 es ${50 * porcentajeCinco}`); // Salida: "El 5% de 50 es 2.5"
```

En este ejemplo, Porcentaje actúa como un proxy que permite representar valores de porcentaje y realizar cálculos con ellos. El Proxy Porcentaje facilita la manipulación de los valores de porcentaje y su uso en operaciones matemáticas.