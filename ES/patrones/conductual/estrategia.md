### Estrategia

Permite seleccionar uno de los algoritmos en determinadas situaciones.

El patrón de estrategia es un patrón de diseño de software de comportamiento que permite seleccionar un algoritmo en tiempo de ejecución. En lugar de implementar un solo algoritmo directamente, el código recibe instrucciones en tiempo de ejecución sobre cuál usar en una familia de algoritmos.

**Ejemplo:**

Tomaremos un ejemplo en el que tenemos un procesador de texto que mostrará datos en función de la estrategia (HTML o Markdown).

```
let FormatoSalida = Object.freeze({
  markdown: 0,
  html: 1,
});

class EstrategiaDeLista {
  iniciar(buffer) {}
  finalizar(buffer) {}
  agregarElementoLista(buffer, elemento) {}
}

class MarkDownEstrategiaLista extends EstrategiaLista {
  agregarElementoLista(buffer, elemento) {
    buffer.push(' * ${elemento}');
  }
}

class EstrategiaListaHTML extends EstrategiaLista {
  iniciar(buffer){
    buffer.push("<ul>");
  }
  
  finalizar(buffer){
    buffer.push("</ul>");
  }
  
  agregarElementoLista(buffer, elemento) {
    buffer.push(' <li>${item}</li>');
  }
}
```

Creando la clase ProcesadorTexto:

```
class ProcesadorTexto {
  constructor(FormatoSalida) {
    this.buffer = [];
    this.ajustarFormatoSalida(formatoSalida);
  }
  
  ajustarFormatoSalida(formatoSalida);

  ajustarFormatoSalida(formato) {
    switch (formato) {
      case FormatoSalida.markdown:
        this.estrategiaDeLista = new MarkDownEstrategiaLista();
        break;
      case FormatoSalida.html:
        this.estrategiaLista = new HTMLEstrategiaLista();
        break;
    }
  }

  agregarLista(elementos) {
    this.estrategiaLista.iniciar(this.buffer);
    for(let articulo of articulos) {
      this.estrategiaLista.agregarElementoLista(this.buffer, item);
    }
    this.estrategiaLista.finalizar(this.buffer);
  }
  
  limpiar() {
    this.buffer = [];
  }
  
  toString() {
    return this.buffer.join("\n");
  }

}
```

Así es como usaremos esto,

```
let pt = new ProcesadorTexto();

pt.ajustarFormatoSalida(FormatoSalida.markdown);
pt.agregarLista(["uno", "dos", "tres"]);
console.log(pt.toString());

pt.limpiar();
pt.ajustarFormatoSalida(FormatoSalida.html);
pt.agregarLista(["uno", "dos", "tres"]);
console.log(pt.toString());
```