### Proxy

Al usar Proxy, una clase puede representar la funcionalidad de otra clase.

El patrón proxy es un patrón de diseño de software. Un proxy, en su forma más general, es una clase que funciona como una interfaz para otra cosa.

### Ejemplo:

Tomemos el ejemplo del valor de proxy.

```
class Porcentaje {
  constructor(porcentaje) {
    this.porcentaje = porcentaje;
  }
  
  toString() {
    return `${this.porcentaje}&`';
  }
  
  valueOf() {
    return this.porcentae / 100;
  }
}

// Usemos este ejemplo de Porcentaje
let porcentajeCinco = new Porcentaje(5);
console.log(porcentajeCinco.toString());
console.log(`El 5% de 50% es ${50 * porcentajeCinco}`);
```