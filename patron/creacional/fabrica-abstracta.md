### Fábrica Abstracta (abstract factory)

Crea familias o grupos de objetos comunes sin especificar sus clases concretas.

El patrón de fábrica abstracto proporciona una forma de encapsular un grupo de fábricas individuales que tienen un tema común sin especificar sus clases concretas.

### Ejemplo:

Usaremos el ejemplo de una máquina para hacer bebidas y bebidas.

```
class Bebida {
  consumir() {
  
  }
}

class Tea extends Bebida {
 consumir() {
  console.log('Esto es Tea');
 }
}

class Cafe extends Bebida {
  consumir() {
    console.log('Esto es Café');
  }
}

class FabricaBebidas {
  preparar(cantidad)
}

class FabricaTea extends FabricaBebidas {
  hacerTea() {
    console.log('Tea creado');
    return new Tea();
  }
}

class FabricaCafe extends FabricaBebidas {
  hacerCafe() {
    console.log('Cafe creado');
    return new Cafe();
  }
}

// Y así es como podemos usarlo

let fabricaBebidaTea = FabricaTea();
let tea  fabricaBebidaTea.hacerTea();
tea.consumir()
```