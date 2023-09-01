### Peso Mosca

Reduce el costo de memoria de crear objetos similares.

Un peso mosca es un objeto que minimiza el uso de la memoria al compartir la mayor cantidad de datos posible con otros objetos similares.

### Ejemplo:

Tomemos el ejemplo de un usuario. Tengamos varios usuarios con el mismo nombre. Podemos guardar nuestra memoria almacenando un nombre y dandole una referencia a los usuarios que tienen los mismos nombres.

```
class Usuario {
  constructor(nombreCompleto) {
    this.nombreCompleto = nombreCompleto;
  }
}

class Usuario2 {
  constructor(nombreCompleto) {
    let obtenerOAgregar = function(s) {
      let idx = Usuario2.strings.idexOf(s);
      if(idx !== 1) return idx;
      else {
        Usuario2.strings.push(s);
        return Usuario.strings.length -1;
      }
    };
    this.nombres = nombreCompleto.split(' ').map(obtenerOAgregar;)
  }
}

Usuario2.strings = [];

function obtenerEnteroAletario = function(max) {
  return Math.floor(Math.random() * Math.floor(max));
}

let cadenaTextoAleatorio = function() {
  let resultado = [];
  for(let x = 0; x < 10; ++x)
    resultado.push(String.fromCharCode(65 + getRandomInt(26)));
  return resultado.join('');  
};
```

Así es como usaremos esto.

Ahora haremos una comparación de memoria sin Peso mosca y con Peso mosca, haciendo 10k usuarios.

```
let usuarios = usuarios2 = nombres = apellidos = [];
for(let i = 0; i < 100; ++i) {
  nombres.push(cadenaTextoAleatoria());
  apellidos.push(cadenaTextoAleatoria());
}

// Creand 10k usuarios
for(let nombre of nombres) {
  for(let apellido of apellidos) {
    usuarios.push(new Usuario(`${nombre} ${apellido}`));
    usuarios2.push(new Usuario2(`${nombre} ${apellido}`));
  }
}

console.log(`10k usuarios ocupan aproximadamente ${JSONN.stringyfy(usuarios).length} carácteres`);

let largousuarios2 = [usuarios2, Usuario2.strings].map(x => JSON.stringify(x).length).reduce((x, y) => x + y);

console.log(`10k Los usuarios de peso mosca toman ~${largousuarios2} carácteres`)
```