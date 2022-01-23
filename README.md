# Patrones de diseño de JavaScript.

¿Qué son los patrones de diseño?

Los patrones de diseño son unas  técnicas para resolver problemas comunes en el diseño de software y a otros ámbitos referentes al diseño de interacción o interfaces. Estos patrones son fácilmente reutilizables y son expresivos.

Un patrón de diseño resulta ser una solución a un problema de diseño. Para que una solución sea considerada un patrón debe poseer ciertas características. Una de ellas es que debe haber comprobado su efectividad resolviendo problemas similares en ocasiones anteriores. Otra es que debe ser reutilizable, lo que significa que es aplicable a diferentes problemas de diseño en distintas circunstancias.

### Tipos de patrones de diseño:

- Creacional
- Estructural
- Conductual

## Patrones de diseño creacional

Los patrones de diseño creacional crearán objetos para ti en lugar de instanciar un objeto directamente.

En ingeniería de software, los patrones de diseño creacionales son patrones de diseño que se ocupan de los mecanismos de creación de objetos, tratando de crear objetos de una manera adecuada a la situación. La forma básica de creación de objetos podría dar lugar a problemas de diseño o complejidad añadida al diseño. Los patrones de diseño creacional resuelven este problema al controlar de alguna manera la creación de este objeto.

- Método de fábrica
- Fábrica abstracta
- Constructor
- Prototipo
- Singleton

### Factory Method (método de fábrica)

En diseño de software, el patrón de diseño Factory Method consiste en utilizar una clase constructora (al estilo del Abstract Factory) abstracta con unos cuantos métodos definidos y otro(s) abstracto(s): el dedicado a la construcción de objetos de un subtipo de un tipo determinado. Es una simplificación del Abstract Factory, en la que la clase abstracta tiene métodos concretos que usan algunos de los abstractos; según usemos una u otra hija de esta clase abstracta, tendremos uno u otro comportamiento.

### Ejemplo:

Tomemos un ejemplo de un punto. Tenemos una clase de puntos y tenemos que crear un punto cartesiano y un punto polar. Definiremos una fábrica de Puntos que hará este trabajo.

```
codigo
```

Ahora crearemos una clase PuntoFactory y usaremos nuestra fábrica ahora,

```
codigo
```

### Fábrica Abstracta (abstract factory)

Crea familias o grupos de objetos comunes sin especificar sus clases concretas.

El patrón de fábrica abstracto proporciona una forma de encapsular un grupo de fábricas individuales que tienen un tema común sin especificar sus clases concretas.

### Ejemplo:

Usaremos el ejemplo de una máquina para hacer bebidas y bebidas.

```
codigo
```

### Constructor

Construye objetos complejos a partir de objetos simples.

El patrón constructor es un patrón de diseño diseñado para proporcionar una solución flexible a varios problemas de creación de objetos en la programación orientada a objetos.

### Ejemplo:

Usaremos un ejemplo ab de una clase Persona que almacena la información de una Persona.

```
codigo
```

Ahora crearemos Person Builder, Person Job Builder y Person Address Builder.

```
codigo
```

```
codigo
```

```
codigo
```

Ahora usaremos nuestro constructor:

```
codigo
```

### Prototipo

Crea nuevos objetos a partir de los objetos existentes.

El patrón prototipo es un patrón de diseño creacional en el desarrollo de software. Se utiliza cuando el tipo de objetos a crear está determinado por una instancia prototípica, que se clona para producir nuevos objetos.

### Ejemplo:

Usaremos el ejemplo de un automóvil.

```
codigo
```

### Singleton

Asegura que solo haya un objeto creado para una clase en particular.

En ingeniería de software, el patrón singleton es un patrón de diseño de software que restringe la creación de instancias de una clase a una instancia "única". Esto es útil cuando se necesita exactamente un objeto para coordinar acciones en todo el sistema.

### Ejemplo:

Creando una clase Singleton:

```
codigo
```

## Patrones de diseño estructural

Estos patrones se refieren a la composición de clases y objetos. Usan herencia para componer interfaces.

En ingeniería de software, los patrones de diseño estructural son patrones de diseño que facilitan el diseño al identificar una forma sencilla de realizar relaciones entre entidades.

- Adaptador
- Bridge
- Compuesto
- Decorador
- Facade
- Peso mosca
- Apoderado

### Adaptador

Este patrón permite que las clases con interfaces incompatibles trabajen juntas ajustando su propia interfaz alrededor de la clase existente.

En ingeniería de software, el patrón adaptador es un patrón de diseño de software que permite utilizar la interfaz de una clase existente como otra interfaz. A menudo se usa para hacer que las clases existentes funcionen con otras sin modificar su código fuente.

### Ejemplo:

Estamos usando un ejemplo de una calculadora. Calculadora1 es una interfaz antigua y Calculadora2 es una interfaz nueva. Construiremos un adaptador que envolverá la nueva interfaz y nos dará resultados usando sus nuevos métodos.

```
codigo
```

```
codigo
```

```
codigo
```

### Bridge (Puente)

Separa la abstracción de la implementación para que las dos puedan variar de forma independiente.

Puente es un patrón de diseño estructural que le permite dividir una clase grande o un conjunto de clases estrechamente relacionadas en dos jerarquías separadas, abstracción e implementación, que se pueden desarrollar de forma independiente.

### Ejemplo:

Crearemos clases de Renderer para renderizar múltiples formas geométricas:

```
codigo
```

```
codigo
```

### Decorador

Agrega o anula dinámicamente el comportamiento de un objeto.

El patrón decorador es un patrón de diseño que permite agregar comportamiento a un objeto individual, de forma dinámica, sin afectar el comportamiento de otros objetos de la misma clase.

### Ejemplo:

Tomaremos el ejemplo del color y las formas. Si tenemos que dibujar un círculo crearemos métodos y dibujaremos un círculo. Si tenemos que dibujar un círculo rojo. Ahora el comportamiento se agrega a un objeto y el patrón Decorator (decorador) me ayudará en eso.

```
codigo
```

```
codigo
```

### Facade (fachada)

Proporciona una interfaz simplificada para código complejo.

El patrón de fachada (también deletreado fachada) es un patrón de diseño de software comúnmente utilizado en la programación orientada a objetos. De manera análoga a una fachada en arquitectura, una fachada es un objeto que sirve como una interfaz frontal que enmascara un código subyacente o estructural más complejo.

### Ejemplo:

Tomemos un ejemplo de un cliente que interactúa con la computadora.

```
codigo
```

```
codigo
```

### Peso Mosca

Reduce el costo de memoria de crear objetos similares.

Un peso mosca es un objeto que minimiza el uso de la memoria al compartir la mayor cantidad de datos posible con otros objetos similares.

### Ejemplo:

Tomemos el ejemplo de un usuario. Tengamos varios usuarios con el mismo nombre. Podemos guardar nuestra memoria almacenando un nombre y dandole una referencia a los usuarios que tienen los mismos nombres.

```
codigo
```

```
codigo
```

Así es como usaremos esto.

Ahora haremos una comparación de memoria sin Peso mosca y con Peso mosca, haciendo 10k usuarios.

```
codigo
```

### Proxy

Al usar Proxy, una clase puede representar la funcionalidad de otra clase.

El patrón proxy es un patrón de diseño de software. Un proxy, en su forma más general, es una clase que funciona como una interfaz para otra cosa.

### Ejemplo:

Tomemos el ejemplo del valor de proxy.

## Patrones de diseño de comportamiento

Los patrones de diseño de comportamiento se ocupan específicamente de la comunicación entre objetos.

En ingeniería de software, los patrones de diseño de comportamiento son patrones de diseño que identifican patrones de comunicación comunes entre objetos. Al hacerlo, estos patrones aumentan la flexibilidad en la realización de la comunicación.

- Cadena de responsabilidad
- Comando
- Iterador
- Mediador
- Memento
- Observador
- Visitante
- Estrategia
- Estado
- Método de plantilla

### Cadena de responsabilidad

Crea una cadena de objetos. Partiendo de un punto, se detiene hasta encontrar una determinada condición.

En el diseño orientado a objetos, el patrón de cadena de responsabilidad es un patrón de diseño que consta de una fuente de objetos de comando y una serie de objetos de procesamiento.

### Ejemplo:

Usaremos un ejemplo de un juego que tiene una criatura. La criatura aumentará su defensa y ataque cuando llegue a cierto punto. Creará una cadena y el ataque y la defensa aumentarán y disminuirán.

```
codigo
```

```
codigo
```

Aumentar el ataque

```
codigo
```

Aumentar la defensa

```
codigo
```

Así es como usaremos esto

```
codigo
```

### Command (Comando)

En la programación orientada a objetos, el patrón de comando es un patrón de diseño de comportamiento en el que se utiliza un objeto para encapsular toda la información necesaria para realizar una acción o desencadenar un evento en un momento posterior. Esta información incluye el nombre del método, el objeto que posee el método y los valores de los parámetros del método.

### Ejemplo:

Estaremos tomando un ejemplo sencillo de una cuenta bancaria en la que damos una orden si tenemos que depositar o retirar una determinada cantidad de dinero.

```
codigo
```

Creando nuestros comandos,

```
codigo
```

Así es como usaremos esto,


```
codigo
```

### Iterador

Iterator accede a los elementos de un objeto sin exponer su representación subyacente.

En la programación orientada a objetos, el patrón de iterador es un patrón de diseño en el que se utiliza un iterador para atravesar un contenedor y acceder a los elementos del contenedor.

### Ejemplo:

Tomaremos el ejemplo de un arreglo en el que imprimimos los valores de un arreglo y luego, mediante el uso de un iterador, imprimimos sus valores hacia atrás.

```
codigo
```

Así es como usaremos esto,

```
codigo
```

### Mediador

El patrón mediador agrega un objeto de terceros para controlar la interacción entre dos objetos. Permite un acoplamiento flexible entre clases al ser la única clase que tiene un conocimiento detallado de sus métodos.

El patrón mediador define un objeto que encapsula cómo interactúa un conjunto de objetos. Este patrón se considera un patrón de comportamiento debido a la forma en que puede alterar el comportamiento de ejecución del programa. En la programación orientada a objetos, los programas a menudo constan de muchas clases.

Usaremos un ejemplo de una persona que usa una sala de chat. Aquí, una sala de chat actúa como mediador entre dos personas que se comunican entre sí.

```
codigo
```

Crear sala de chat,

```
codigo
```

Así es como usamos esto,

```
codigo
```

### Memento

Memento restaura un objeto a su estado anterior.

El patrón memento es un patrón de diseño de software que brinda la capacidad de restaurar un objeto a su estado anterior. El patrón memento se implementa con tres objetos: el originador, un cuidador y un recuerdo.

### Ejemplo:

Estaremos tomando un ejemplo de una cuenta bancaria en la que almacenamos nuestro estado anterior y tendrá la funcionalidad de deshacer.

```
codigo
```

```
codigo
```

### Observador

Permite que varios objetos observadores vean un evento.

El patrón de observador es un patrón de diseño de software en el que un objeto, llamado sujeto, mantiene una lista de sus dependientes, llamados observadores, y les notifica automáticamente cualquier cambio de estado, generalmente llamando a uno de sus métodos.

### Ejemplo:

Tomaremos un ejemplo de una persona en la que si una persona se enferma, mostrará una notificación.

```
codigo
```

```
codigo
```

Así es como usaremos esto,

```
codigo
```

### Visitante

Agrega operaciones a los objetos sin tener que modificarlos.

El patrón de diseño del visitante es una forma de separar un algoritmo de una estructura de objeto en la que opera. Un resultado práctico de esta separación es la capacidad de agregar nuevas operaciones a estructuras de objetos existentes sin modificar las estructuras.

### Ejemplo:

Tomaremos un ejemplo de la clase ExpresionNumerica en el que nos da el resultado de la expresión dada.

```
codigo
```

```
codigo
```

### Estrategia

Permite seleccionar uno de los algoritmos en determinadas situaciones.

El patrón de estrategia es un patrón de diseño de software de comportamiento que permite seleccionar un algoritmo en tiempo de ejecución. En lugar de implementar un solo algoritmo directamente, el código recibe instrucciones en tiempo de ejecución sobre cuál usar en una familia de algoritmos.

### Ejemplo:

Tomaremos un ejemplo en el que tenemos un procesador de texto que mostrará datos en función de la estrategia (HTML o Markdown).

```
codigo
```

```
codigo
```

Creando la clase ProcesadorTexto:

```
codigo
```

Así es como usaremos esto,

```
codigo
```

### Estado

Altera el comportamiento de un objeto cuando cambia su estado interno.

El patrón de estado es un patrón de diseño de software de comportamiento que permite que un objeto altere su comportamiento cuando cambia su estado interno. Este patrón está cerca del concepto de máquinas de estados finitos.

### Ejemplo:

Estaremos tomando un ejemplo de un interruptor de luz en el que si encendemos o apagamos el interruptor, su estado cambia.

```
codigo
```

Vamos a crear una clase Switch para usar estos estados de encendido y apagado.

```
codigo
```

```
codigo
```

### Método de plantilla

Define el esqueleto de un algoritmo como una clase abstracta, cómo debe realizarse.

Template Method (método de plantilla) es un método en una superclase, generalmente una superclase abstracta, y define el esqueleto de una operación en términos de una serie de pasos de alto nivel.

### Ejemplo:

Tomaremos un ejemplo de un juego de ajedrez,

```
codigo
```

Creando nuestra clase Ajedrez,

```
codigo
```

Así usaremos esto:

```
codigo
```






