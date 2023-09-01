### Prototipo

Crea nuevos objetos a partir de los objetos existentes.

El patrón prototipo es un patrón de diseño creacional en el desarrollo de software. Se utiliza cuando el tipo de objetos a crear está determinado por una instancia prototípica, que se clona para producir nuevos objetos.

### Ejemplo:

Usaremos el ejemplo de un automóvil.

```
class Carro {
  constructor(nombre, modelo) {
    this.nombre = nombre;
    this.modelo = modelo;
  }
  
  ajustarNombre(nombre) {
    console.log(`${nombre}`)
  }
  
  clonar(){
    return new Carro(this.nombre, this.modelo)
  }
  
// Y así es como lo usamos
let carro = new Carro();
carro.ajustarNombre('Audi');

let carro2 = carro.clonar();
carro2.ajustarNombre('BMW');
}
```