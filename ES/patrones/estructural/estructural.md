# Patrones de Diseño Estructurales

Los patrones de diseño estructurales se centran en la composición de clases y objetos para formar estructuras más complejas. Utilizan la herencia y la composición de interfaces para crear relaciones entre entidades de manera eficiente y flexible.

A continuación, se presentan los patrones de diseño estructurales más comunes en JavaScript:

## 1. Adaptador

El patrón **Adaptador** permite que interfaces incompatibles trabajen juntas. Convierte la interfaz de una clase en otra que el cliente espera. Es útil cuando necesitas que objetos con interfaces diferentes colaboren.

- [Más sobre el Adaptador](/patron/estructural/adaptador.md)

## 2. Puente

El patrón **Puente** separa una abstracción de su implementación, lo que permite que ambas evolucionen independientemente. Es útil cuando deseas evitar una unión permanente entre una abstracción y su implementación.

- [Más sobre el Puente](/patron/estructural/puente.md)

## 3. Compuesto

El patrón **Compuesto** compone objetos en estructuras de árbol para representar jerarquías de parte-todo. Permite tratar objetos individuales y composiciones de objetos de manera uniforme.

- [Más sobre el Compuesto](/patron/estructural/compuesto.md)

## 4. Decorador

El patrón **Decorador** agrega funcionalidad a objetos existentes dinámicamente sin modificar su estructura. Es útil cuando deseas extender la funcionalidad de un objeto de manera flexible.

- [Más sobre el Decorador](/patron/estructural/decorador.md)

## 5. Fachada

El patrón **Fachada** proporciona una interfaz simplificada para un conjunto de interfaces en un subsistema. Facilita el uso de sistemas complejos al proporcionar una interfaz más fácil de usar.

- [Más sobre la Fachada](/patron/estructural/facade.md)

## 6. Peso Mosca

El patrón **Peso Mosca** minimiza el uso de la memoria o el almacenamiento en disco al compartir lo más posible con objetos similares. Es útil cuando necesitas gestionar un gran número de objetos con uso eficiente de recursos.

- [Más sobre el Peso Mosca](/patron/estructural/peso-mosca.md)

## 7. Proxy

El patrón **Proxy** proporciona un sustituto o representante de otro objeto para controlar el acceso a él. Puede utilizarse para agregar funcionalidad adicional, como el control de acceso o la carga perezosa.

- [Más sobre el Proxy](/patron/estructural/proxy.md)

Cada uno de estos patrones de diseño estructurales ofrece soluciones eficientes y flexibles para crear relaciones entre clases y objetos en proyectos de JavaScript. Al comprender estos patrones, podrás diseñar sistemas más modularizados y fáciles de mantener.