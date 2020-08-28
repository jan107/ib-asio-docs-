# Integración entre la arquitectura ontológica y la arquitectura semántica

## Introducción

El objetivo de este documento es explicar el diseño arquitectónico entre la infraestructura ontológica y la infraestructura semántica, describiendo los procesos que se tienen que llevar a cabo tras los cambios que pueden surgir en la red de ontologías.

## Requisito

Se precisa que la integración entre ambas infraestructuras requieran del menor esfuerzo manual posible, automatizando la mayoría de los escenarios que surgen de los cambios en las ontologías.

> Es necesario informar que aunque se busque la máxima automatización posible, habrá puntos en los que esta no se podrá llevar acabo como por ejemplo el proceso de creación de ontologías y la adaptación de estos cambios al proceso de ETL.

## Despliegue inicial (primera instalación)

dibujo de todo el proceso

- Generación de clases POJO a partir de shape expressions con la herramienta [ShEx Lite](#ShEx)

- Empaquetado de las clases java en un artefacto **dataset-domain-model-X.X.X.jar** donde X.X.X es su correspondiente versionado.

- Subida del artefacto al repositorio [MVN Central](https://mvnrepository.com/repos/central) para su posterior consumo por parte de la arquitectura semántica.

## Cambios en la red de ontología (sucesivas iteraciones)

### Modificaciones en la infraestructura ontológica

Cualquier modificación en la ontología implica modificaciones en las shape expressions, que son las que se encargan de validar la semántica de la ontología.

#### Procesos manuales

Estas modificaciones dan como resultado un listado de cambios a aplicar en las Shape Expressions. Por ejemplo:

| Operación                               | Efecto en las instancias                                                                     |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| Creación de nueva clase C               | No habría ningún tipo de problema para las instancias existentes.                            |
| Borrado de clase C                      | Las instancias de clase C quedarían en un estado inconsistente.                              |
| Crear una propiedad p                   | No habría ningún tipo de problema para las instancias existentes.                            |
| Eliminar la propiedad p                 | Los valores de la propiedad p para todas las instancias que la utilicen se perderían.        |
| Eliminar una propiedad p de una clase C |  Los valores de la propiedad p para las instancias que pertenecen a la clase C se perderían. |

Ver [aquí](https://github.com/HerculesCRUE/ib-asio-docs-/blob/master/entregables_hito_1/07-Control_de_versiones_OWL/ASIO_Izertis_ControlDeVersionesOWL.md) una descripción completa de todas las operaciones.

#### Procesos automáticos

La construcción y el despligue de la ontología están controlados a traves de workflows de integración continua de gitHub. Son las que se encargan de mantener actualizada la ontología en Wikibase.

[PONER FOTO AQUI]

La generación de clases POJO a partir de shape expressions con la herramienta [ShEx Lite](#ShEx) se realizará de forma automática cada vez que la rama [master](https://github.com/HerculesCRUE/ib-hercules-ontology/tree/master/scripts) donde se hubican las Shape Expressions detecta que ha habido cambios.

El resultado de esta iteración es la regeneración de **todo el modelo de dominio**, posterior empaquetado y subida al repositorio [MVN Central](https://mvnrepository.com/repos/central).

> El motivo por el que es necesario la regeneración de todo el modelo de dominio es debido a que la herramiento ShEx Lite no es consciente de que ha cambiado y que no en la antología.

Repetición de los pasos empaquetado y subida del artefacto [Despliegue inicial (primera instalación)](Despliegue)

### Modificaciones en la infraestructura semántica

#### Procesos automáticos

#### Procesos manuales

- Cuando se aplican las modificaciones en la red de ontologías
- Modificaciones en la ETL

## ShEx

[ShEx Lite](https://www.weso.es/shex-lite/) es un subconjunto de una especificación de Shape Expressions que ofrece un API para generar las clases de dominio a partir de unos datos de entrada, y el resultado se enviará a donde indique el parámetro de salida de este método.
