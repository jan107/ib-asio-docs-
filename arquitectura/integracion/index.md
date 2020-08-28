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

#### Implicaciones

Cualquier modificación en la ontología implica modificaciones en las shape expressions, que son las que se encargan de validar la semántica de la ontología.

#### Procesos automáticos

Generación de clases POJO a partir de shape expressions con la herramienta [ShEx Lite](#ShEx Lite)

#### Procesos manuales

### Modificaciones en la infraestructura semántica

#### Procesos automáticos

#### Procesos manuales

- Cuando se aplican las modificaciones en la red de ontologías
- Modificaciones en la ETL

## ShEx

[ShEx Lite](https://www.weso.es/shex-lite/)
