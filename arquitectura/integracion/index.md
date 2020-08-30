# Integración entre la arquitectura ontológica y la arquitectura semántica

## Introducción

El objetivo de este documento es explicar el diseño arquitectónico entre la infraestructura ontológica y la infraestructura semántica, describiendo los procesos que se tienen que llevar a cabo tras los cambios que pueden surgir en la red de ontologías.

## Requisito

Se precisa que la integración entre ambas infraestructuras requieran del menor esfuerzo manual posible, automatizando la mayoría de los escenarios que surgen de los cambios en las ontologías.

> Es necesario informar que aunque se busque la máxima automatización posible, habrá puntos en los que esta no se podrá llevar acabo como por ejemplo el proceso de creación/actualización de ontologías y la adaptación de estos cambios al proceso de ETL.

## Despliegue inicial ontología (primera instalación)

dibujo de todo el proceso

- Generación de clases POJO a partir de shape expressions con la herramienta [ShEx Lite](#ShEx)

- Empaquetado de las clases java en un artefacto **dataset-domain-model-X.X.X.jar** donde X.X.X es su correspondiente versionado.

- Subida del artefacto al repositorio [MVN Central](https://mvnrepository.com/repos/central) para su posterior consumo por parte de la arquitectura semántica.

## Despligue inicial arquitectura semántica

No requiere de acciones adicionales a las ya descritas en el documento [despliegue_inicial](https://github.com/HerculesCRUE/ib-asio-docs-/tree/master/arquitectura_semantica/despliegues/entorno_desarrollo).

## Cambios en la red de ontología (sucesivas iteraciones)

### Modificaciones en la infraestructura ontológica

Cualquier modificación en la ontología implica modificaciones en las shape expressions, que son las que se encargan de validar la semántica de la ontología.

#### Procesos manuales

Estas modificaciones dan como resultado un listado de cambios a aplicar en las Shape Expressions.

| Modificación                                                                               | Protocolo a aplicar                      |
| ------------------------------------------------------------------------------------------ | ---------------------------------------- |
| Creación de nueva clase C                                                                  | Modificar directamente shape expression  |
| Borrado de clase C                                                                         | Modificar directamente shape expression  |
| Crear una propiedad p                                                                      | Modificar directamente shape expression  |
| Eliminar la propiedad p                                                                    | Modificar directamente shape expression  |
| Eliminar una propiedad p de una clase C                                                    |  Modificar directamente shape expression |
| Añadir una relación de subclase-superclase entre la subclase SubC y la superclase SuperC   | Modificar directamente shape expression  |
| Eliminar una relación de subclase-superclase entre la subclase SubC y la superclase SuperC | Modificar directamente shape expression  |
| Declarar clases C1 y C2 como disjoint                                                      | Modificar directamente shape expression  |
| Definir una propiedad p como transitiva o simétrica                                        | Modificar directamente shape expression  |
| Mover una propiedad p de una subclase a una superclase                                     | Modificar directamente shape expression  |
| Mover una propiedad p de una superclase a una subclase                                     | Modificar directamente shape expression  |
| Reducir las restricciones de una propiedad p                                               | Modificar directamente shape expression  |
| Añadir restricciones a una propiedad p                                                     | Modificar directamente shape expression  |
| Modificar la descripción de una clase (label, comment, alias)                              | Modificar directamente shape expression  |

#### Procesos automáticos

La construcción y el despligue de la ontología están controlados a traves de [workflows de integración continua](https://docs.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow) de GitHub. Son las que se encargan de mantener actualizada la ontología en Wikibase.

[PONER FOTO AQUI]

La generación de clases POJO a partir de shape expressions con la herramienta [ShEx Lite](#ShEx) se realizará de forma automática cada vez que la rama [master](https://github.com/HerculesCRUE/ib-hercules-ontology/tree/master/scripts) donde se hubican las Shape Expressions detecta que ha habido cambios.

El resultado de esta iteración es la regeneración de **todo el modelo de dominio**, posterior empaquetado y subida al repositorio [MVN Central](https://mvnrepository.com/repos/central).

> El motivo por el que es necesario la regeneración de todo el modelo de dominio es debido a que la herramienta ShEx Lite no es consciente de que ha cambiado y que no en la ontología.

### Comunicación entre la infraestructura ontológica e infraestructura semántica

Para que la infraestructura semántica sea consciente de que han habiado cambios en la red de ontologías, la infraestructura ontológica ofrece un nuevo módulo API **exchange** ofrece los métodos:

| Request type | EndPoint                                     | Description                                                                                                 |
| ------------ | -------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| GET          | `/versions`                                  | Access one or more resources and return the result as JSON.                                                 |
| GET          | `/ontology/{currentVersion}/{targetVersion}` | Return `201 Created` if the resource is successfully created and return the newly created resource as JSON. |

The following table shows the possible return codes for API requests.

| Return values            | Description                                                                                                                                                   |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `200 OK`                 | The `GET`, `PUT` or `DELETE` request was successful, the resource(s) itself is returned as JSON.                                                              |
| `204 No Content`         | The server has successfully fulfilled the request and that there is no additional content to send in the response payload body.                               |
| `201 Created`            | The `POST` request was successful and the resource is returned as JSON.                                                                                       |
| `304 Not Modified`       | Indicates that the resource has not been modified since the last request.                                                                                     |
| `400 Bad Request`        | A required attribute of the API request is missing, e.g., the title of an issue is not given.                                                                 |
| `401 Unauthorized`       | The user is not authenticated, a valid [user token](#authentication) is necessary.                                                                            |
| `403 Forbidden`          | The request is not allowed, e.g., the user is not allowed to delete a project.                                                                                |
| `404 Not Found`          | A resource could not be accessed, e.g., an ID for a resource could not be found.                                                                              |
| `405 Method Not Allowed` | The request is not supported.                                                                                                                                 |
| `409 Conflict`           | A conflicting resource already exists, e.g., creating a project with a name that already exists.                                                              |
| `412`                    | Indicates the request was denied. May happen if the `If-Unmodified-Since` header is provided when trying to delete a resource, which was modified in between. |
| `422 Unprocessable`      | The entity could not be processed.                                                                                                                            |
| `500 Server Error`       | While handling the request something went wrong server-side.                                                                                                  |

Repetición de los pasos empaquetado y subida del artefacto [Despliegue inicial (primera instalación)](Despliegue) //FIXME remove this paragraph

### Modificaciones en la infraestructura semántica

#### Procesos manuales

- Cuando se aplican las modificaciones en la red de ontologías
- Modificaciones en la ETL a partir de la generación de los ficheros DELTA

#### Procesos automáticos

### Api de comunicación entre infraestructura ontológica y infraestructura semántica

## ShEx

[ShEx Lite](https://www.weso.es/shex-lite/) es un subconjunto de una especificación de Shape Expressions que ofrece un API para generar las clases de dominio a partir de unos datos de entrada, y el resultado se enviará a donde indique el parámetro de salida de este método.
