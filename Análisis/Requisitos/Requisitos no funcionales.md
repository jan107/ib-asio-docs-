# Requisitos no funcionales



## Generales



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | El software debe garantizar el acceso al sistema de las personas autorizadas en cada parte. |           |
|        | El protocolo a usar será abierto.                            |           |
|        | El protocolo permitirá autenticación y autorización.         |           |
|        | El software estará preparado para su recuperación ante fallos de conexión. |           |
|        | El software estará codificado de manera limpia y clara para garantizar su comprensibilidad. |           |
|        | Se dotará al producto de la documentación necesaria para facilitar el mantenimiento y actualización. |           |
|        | El software debe ser compatible con el framework y stack tecnológico de la Universidad de Murcia. |           |
|        | Estabilidad: el desarrollo debe mantenerse estable ante un incremento en el número de usuarios simultáneos |           |
|        | Escalabilidad de los datos: el sistema debe garantizar que los datos a manejar pueden alcanzar volúmenes importantes y deben ser soportados por la arquitectura prevista. Se debe plantear arquitecturas escalables. |           |
|        | Facilidad para integración de nuevas fuentes de datos: el software debe estar preparado para incorporar nuevas fuentes de datos no contempladas en este punto. Debe ser sencilla la incorporación de nuevos módulos que permitan la comunicación con otros sistemas |           |
|        | El interfaz de usuario del sistema gestor de datos será lo más usable y ligero posible, y estará orientado a que los expertos del dominio GI puedan realizar la gestión y publicación de datos. |           |
|        |                                                              |           |



## Front



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | Se usará el logo y la tipografía de Hercules para crear un diseño a partir de estos datos. |           |
|        | El interfaz del software debe encajar con el aspecto y grado de accesibilidad y usabilidad del resto de herramientas software desplegadas en el framework de la Universidad de Murcia. |           |
|        | Las páginas web de documentación se intentarán generar de la forma más automática posible. |           |
|        |                                                              |           |



## Backend



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | Se dispondrá de un Triple-store para almacenar y consultar la información de forma semántica |           |
|        | El acceso a los datos del triple-store  estará restringido y solamente se podrá realizar a través del componente  gestor de datos, el cual contiene una gestión de usuarios y control de acceso |           |
|        | Logging: el software ofrecerá  herramientas para detectar anomalías en el funcionamiento del sistema |           |
|        |                                                              |           |

## Ontologías



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | Los datos dispondrán de un identificador único y persistente |           |
|        | Los datos deben ser descritos con metadatos descriptivos     |           |
|        | Los metadatos incluyen clara y explícitamente el identificador de los datos que describen. |           |
|        | Los metadatos serán accesibles incluso cuando los datos ya no se encuentren disponibles |           |
|        | Los metadatos serán accesibles incluso cuando los datos ya no se encuentren disponibles |           |
|        | Los (Meta) datos usan un lenguaje formal, accesible, compartido y ampliamente aplicable para la representación del conocimiento. |           |
|        | Los (Meta) datos usan vocabularios que siguen los principios FAIR |           |
|        | Los (Meta) datos incluyen referencias calificadas a otros (Meta) datos. |           |
|        | Los (meta) datos se publican con una licencia de uso de datos clara y accesible. |           |
|        | Los (Meta) datos están asociados con información detallada sobre procedencia. |           |
|        | Los (Meta) datos cumplen con los estándares de la comunidad relevantes para el dominio. |           |
|        | Las URIs de la ontología deberán respetar el Esquema de URIs Hércules definido en Arquitectura Semántica de Datos del SUE. |           |
|        |                                                              |           |
|        |                                                              |           |



## Validación de publicación de datos



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | Se crearán un Test Suite que consistirá en una serie de peticiones HTTP a ejecutar contra el sistema con una casuística lo más diversa y exhaustiva posible. |           |
|        | Se crearán y realizarán pruebas de carga (Peticiones simúltaneas, consultas complejas, etc.) |           |
|        | En los test se intentarán comprobar los requisitos del sistema. |           |
|        | Los test se realizarán con los datos de Datasets de referencia Hércules. |           |
|        | El Test suite ha de ser fácil de modificar y configurar, para que los técnicos de la UM puedan ejecutarlo, añadir tests nuevos o modificar tests existentes con datos y configuraciones nuevas |           |
|        | El Test Suite constará de documentación para facilitar su extensión y modificación. |           |
|        | Se pueden usar como referencia para algunos test *Linked Data Platform Test Suite*:<br />- https://github.com/w3c/ldp-testsuite<br />- https://github.com/opendata-euskadi/LinkedDataTestSuite |           |



## Generador de URIS



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | Existirá un URI Lookup Service (desarrollado en otro proyecto) con interfaz para máquinas (Rest services) para buscar URIs de entidades, a través del contenido de las URIs y a través del contenido de propiedades como rdfs:label o rdfs:comment (Las propiedades a usar serán configurables). |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |