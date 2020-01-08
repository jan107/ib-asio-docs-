# Arquitectura ASIO - UM

El presente documento parte de la arquitectura descrita en los documentos Estudio de viabilidad y especialmente el anexo anex3_AnyDisBackendSGI.docx.
Se propone esta arquitectura como base sobre la que iterar, incorporando a la misma, necesidades que pudiesen surgir bien en la fase de implementación, bien en base a las necesidades del equipo de WESO.  

## Arquitectura preliminar

![Arquitectura preliminar](./images/arquitectura-preliminar.jpg)

Se recomienda construir cada bloque funcional, de acuerdo con una arquitectura orientada a microservicios, ya que esto ofrece las siguientes ventajas:

* Proporciona Flexibilidad, en la implementación, siendo la solución global agnóstica a la implementación, lo que permite desarrollar cada bloque funcional usando el lenguaje de programación, librerías o framework que más convenga para su resolución.
* Facilita el escalado, pudiendo replicar un bloque funcional tantas veces como sea necesario para optimizar la tarea.
* Facilita el mantenimiento, pudiendo cambiar la lógica en un bloque funcional, sin afectar al resto.
* El desarrollo independiente de los microservicios, proporciona capacidad para desarrollarlos de forma concurrente.

Dentro de cada microservicio, se recomienda siempre que sea posible una el patrón de diseño clean arquitecture, de forma que:

* Aumenta la mantenibilidad
* Aumenta la testeabilidad
* Facilita el mantenimiento

Como lenguaje base para el desarrollo de microservicios (puede cambiar en algún microservicio, por razones de idoneidad del lenguaje, framework o librería a la función que se desea realizar), se recomiendan lenguajes basados en Java Virtual Machine, bien Java, bien Scala, por los siguientes motivos:

* Existen múltiples librerías desarrolladas en Java, en el contexto de la Web Semántica (Apache Jena, Shaclex, ShEx for Java), que pueden facilitar en gran medida el desarrollo de funcionalidades
* Lenguajes propicios para el desarrollo de microservicios.
* Lenguajes fuertemente tipados, que favorecen la detección de fallos en fase de compilación, frente a fallos en fase de ejecución.
* Fácil de encontrar expertise en dichos lenguajes, por lo tanto, fácil de mantener.

## Arquitectura alto nivel

Con el fin de facilitar la visión de cómo está planteada la aplicación, es recomendable visualizar desde un punto de vista de alto nivel, los principales módulos que la forman, sin entrar en el detalle.

![Arquitectura alto nivel](./images/high-level.png)

A alto nivel, la arquitectura se divide en varias partes:

* Backend: Módulo encargado de la ingesta de datos desde un origen, procesando la información e insertándola en los diferentes almacenamientos
* Gestión: Módulo backoffice encargado de la gestión del sistema
* Servicio de publicación web: Servicio encargado de la consulta de datos por parte de los usuarios / máquinas
* API Rest LDP
* Autorización y autenticación

También formarán parte de esta visión general:

* Orígenes de datos
* Almacenamientos de datos RDF
* Sistema de logging y monitorización
* Bus de servicio general de la aplicación
* Base de datos de gestión

## Arquitectura Backend

El módulo de backend es el encargado de la ingesta de datos desde un origen, procesando la información e insertándola en los diferentes almacenamientos.

![Arquitectura backend alto nivel](./images/backend.png)

Este módulo estará formado por varias piezas:

* Entrada de datos: módulo encargado de obtener los datos de una entrada de datos (fuentes externas), haciendo las adaptaciones necesarias para que conciliarlos con entides internas e ingesta en bus de servicio general
* Sistema de gestión: servicio encargado de consumir los eventos del bus de servicio y decidir si deben ir al módulo de gestión de eventos
* Gestión de eventos: módulo encargado de procesar los eventos generados por el módulo de entrada, permitiendo almacenar los datos en los diferntes sistemas de almacenamiento
* Bus de servicio general (kafka): cola de mensajes utilizada para la comunicación asíncrona entre los módulos

### Entrada de datos

El sistema de entrada de datos, tiene como función, procesar los datos de fuentes externas (Bases de datos, Repositorios de ficheros, …), conciliarlos con entidades internas, e introducirlos al sistema.

![Arquitectura entrada de datos](./images/input.png)

**Implementación:** Para su implementación se desarrollarán una serie de microservicios. Potencialmente hay servicios que estarán muy acoplados a cliente (importadores) y otros menos, por lo que será conveniente que cada componente realice las operaciones de la forma más atómica y desacoplada posible.

**Lenguaje:** Para la implementación de los microservicios involucrados en este módulo se recomienda lenguaje de la JVM, por compatibilidad con librerías, principalmente Java o Scala.

#### Importadores

Se trata de N microservicios, uno por cada fuente de datos, que se encargarán de procesar las fuentes externas y adaptar los datos recuperados al formato establecido en la aplicación.

Por ejemplo, en el caso de una fuentes de datos vía FTP, el importador correspondientes se encargaría de recuperar los ficheros vía FTP, procesar los ficheros y extraer los datos. 

**Implementación:** Existen librerías que podrían facilitar la implementación: 

* ShExML : Librería desarrollada por WESO, que permite mapear datos.
* RML : Lenguaje que permite definir el mapeo de forma escalable y reutilizable con distintas fuentes, orientado a generar documentos RDFs.

**Input:** Fuente de datos externa
**Output:** Evento publicado en Service Bus interno del módulo de entrada

#### Procesador

Obtiene los datos desde el importador y realiza tareas de conciliación y descubrimiento de entidades de otras fuentes de datos enlazados y genera las URIs de los recursos de acuerdo con la política establecida.

**Implementación:** Se apoyará en las siguientes librerías:
* Factoría de URIs
* Librería de descubrimiento.

**Input:** Evento recibido desde el service bus interno del módulo de entrada
**Output:** Evento publicado en Service Bus general

#### Service bus interno del módulo de entrada

Se trata de una cola Kafka para garantizar que el procesamiento de los datos de entrada de forma asíncrona, para evitar sobrecargas del procesador.

### Gestión de eventos

El módulo de gestión de eventos se encargará de recoger los eventos generados por el sistema de entrada y procesarlos, hasta su guardado en los diferentes sistemas de almacenamiento que se definan.

![Arquitectura gestión de eventos](./images/event-management.png)

**Implementación:** Para su implementación se desarrollarán una serie de microservicios. Se debería disponer de unos servicios lo más atómico posible, sobre todo en el caso de los microservicios dedicados a interacturar con los sistemas de almacenamiento, los cuales van a estar muy ligados a las APIs provistas por estos.

**Lenguaje:** Para la implementación de los microservicios involucrados en este módulo se recomienda lenguaje de la JVM, por compatibilidad con librerías, principalmente Java o Scala.

#### Sisstema de gestión

El sistema de gestión se encargará de decidir qué eventos enviar a los procesadores de datos y bajo qué condiciones. Se encargará de consumir los eventos del bus de servicio general del sistema e ingestar en el bus de servicio de gestión aquellos eventos que se deban procesar.

**Input:** Evento recibido desde el service bus general del sistema
**Output:** Evento publicado en Service Bus de gestión

#### 

### APIs / Web

![Arquitectura APIs / Web](./images/apis-web.png)

## Arquitectura aplicación de gestión

![Arquitectura aplicación de gestión](./images/management-app.png)

## Autenticación y autorización

### SIR

## Procesamiento asíncrono

## Plataforma de despliegue

### Microservicios

### Entorno docker

### Kubernetes

### Service Mesh

#### Istio
