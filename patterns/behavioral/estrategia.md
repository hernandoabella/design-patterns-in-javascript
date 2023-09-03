### Estrategia

Permite seleccionar uno de los algoritmos en determinadas situaciones.

El patrón de estrategia es un patrón de diseño de software de comportamiento que permite seleccionar un algoritmo en tiempo de ejecución. En lugar de implementar un solo algoritmo directamente, el código recibe instrucciones en tiempo de ejecución sobre cuál usar en una familia de algoritmos.

**Ejemplo:**

Tomaremos un ejemplo en el que tenemos un procesador de texto que mostrará datos en función de la estrategia (HTML o Markdown).

El patrón de diseño de estrategia permite seleccionar un algoritmo en tiempo de ejecución. Aquí está el ejemplo paso a paso:

**1.Definición de Formatos de Salida:** Se define un objeto FormatoSalida que enumera los formatos de salida disponibles, en este caso, Markdown y HTML.

**2.Clase Abstracta EstrategiaDeLista:** Se crea una clase abstracta llamada EstrategiaDeLista que define métodos abstractos iniciar, finalizar, y agregarElementoLista. Estos métodos serán implementados por estrategias específicas.

```
class EstrategiaDeLista {
  iniciar(buffer) {}
  finalizar(buffer) {}
  agregarElementoLista(buffer, elemento) {}
}

```

**3. Estrategias de Lista Específicas:**
Se crean dos clases que heredan de EstrategiaDeLista para implementar estrategias específicas: MarkDownEstrategiaLista y EstrategiaListaHTML. Cada una implementa los métodos abstractos de la estrategia base según su formato específico.

```
class MarkDownEstrategiaLista extends EstrategiaLista {
  agregarElementoLista(buffer, elemento) {
    buffer.push(` * ${elemento}`);
  }
}

class EstrategiaListaHTML extends EstrategiaLista {
  iniciar(buffer) {
    buffer.push("<ul>");
  }

  finalizar(buffer) {
    buffer.push("</ul>");
  }

  agregarElementoLista(buffer, elemento) {
    buffer.push(` <li>${elemento}</li>`);
  }
}

```

**4.Clase ProcesadorTexto:** Se crea una clase ProcesadorTexto que acepta un formato de salida y utiliza una estrategia de lista específica en función del formato seleccionado.

```
class ProcesadorTexto {
  constructor(formatoSalida) {
    this.buffer = [];
    this.ajustarFormatoSalida(formatoSalida);
  }

  ajustarFormatoSalida(formato) {
    switch (formato) {
      case FormatoSalida.markdown:
        this.estrategiaLista = new MarkDownEstrategiaLista();
        break;
      case FormatoSalida.html:
        this.estrategiaLista = new EstrategiaListaHTML();
        break;
    }
  }

  agregarLista(elementos) {
    this.estrategiaLista.iniciar(this.buffer);
    for (let elemento of elementos) {
      this.estrategiaLista.agregarElementoLista(this.buffer, elemento);
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

**5.Uso del Procesador de Texto:** Se crea una instancia de ProcesadorTexto, se ajusta el formato de salida y se agrega una lista. Luego, se muestra el resultado.

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

**Código final:**

```
// Enumeración de formatos de salida
let FormatoSalida = Object.freeze({
  markdown: 0,
  html: 1,
});

// Clase abstracta EstrategiaDeLista
class EstrategiaDeLista {
  iniciar(buffer) {}
  finalizar(buffer) {}
  agregarElementoLista(buffer, elemento) {}
}

// Estrategia específica para formato Markdown
class MarkDownEstrategiaLista extends EstrategiaDeLista {
  agregarElementoLista(buffer, elemento) {
    buffer.push(` * ${elemento}`);
  }
}

// Estrategia específica para formato HTML
class EstrategiaListaHTML extends EstrategiaDeLista {
  iniciar(buffer) {
    buffer.push("<ul>");
  }

  finalizar(buffer) {
    buffer.push("</ul>");
  }

  agregarElementoLista(buffer, elemento) {
    buffer.push(` <li>${elemento}</li>`);
  }
}

// Clase ProcesadorTexto
class ProcesadorTexto {
  constructor(formatoSalida) {
    this.buffer = [];
    this.ajustarFormatoSalida(formatoSalida);
  }

  ajustarFormatoSalida(formato) {
    switch (formato) {
      case FormatoSalida.markdown:
        this.estrategiaLista = new MarkDownEstrategiaLista();
        break;
      case FormatoSalida.html:
        this.estrategiaLista = new EstrategiaListaHTML();
        break;
    }
  }

  agregarLista(elementos) {
    this.estrategiaLista.iniciar(this.buffer);
    for (let elemento of elementos) {
      this.estrategiaLista.agregarElementoLista(this.buffer, elemento);
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

// Crear una instancia del procesador de texto
let pt = new ProcesadorTexto();

// Configurar el formato de salida a Markdown
pt.ajustarFormatoSalida(FormatoSalida.markdown);

// Agregar una lista de elementos
pt.agregarLista(["uno", "dos", "tres"]);

// Mostrar la salida en formato Markdown
console.log("Salida en formato Markdown:");
console.log(pt.toString());

// Limpiar el procesador de texto
pt.limpiar();

// Configurar el formato de salida a HTML
pt.ajustarFormatoSalida(FormatoSalida.html);

// Agregar una lista de elementos
pt.agregarLista(["uno", "dos", "tres"]);

// Mostrar la salida en formato HTML
console.log("\nSalida en formato HTML:");
console.log(pt.toString());

```

**Salida esperada en formato HTML:**

```
<ul>
 <li>uno</li>
 <li>dos</li>
 <li>tres</li>
</ul>

```

Este código muestra cómo se puede cambiar fácilmente entre diferentes estrategias de formato de salida (Markdown y HTML) en tiempo de ejecución utilizando el patrón de diseño de estrategia.
