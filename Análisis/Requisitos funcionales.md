# Requisitos funcionales



## Subsistema de Autentificación



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | Un usuario público podrá registrarse en la aplicación a través del sistema SIR (Servicio de Identidad de RedIRIS) únicamente. |           |
|        | El sistema SIR devolverá algunos datos del usuario a la aplicación, al menos un identificador para identificar el usuario y guardarlo en el sistema. |           |
|        | Un usuario podrá loguearse en la aplicación a través del sistema SIR (Servicio de Identidad de RedIRIS) |           |
|        | La aplicación ASIO ofrecerá un enlace para acceder a través de el sistema SIR, de forma que al acceder mediante este sistema pueda volver a la aplicación de forma automática. |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |





## Subsistema de administración de la aplicación y roles



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | La aplicación constará de una serie de roles predefinidos:<br />- *Gestor ASIO*: Es el administrador del sistema. Podrá administrar roles y modificar la frecuencia de los procesos automáticos de carga de datos. <br />- *Administrador de universidad*: Podrá crear y modificar ontologías relativas a su universidad y les asignará roles, cargar datos relativos a esa universidad y modificar los roles de los datos<br />- *Investigador de universidad*: Podrá ver los datos asignados a su rol, y los datos de usuario para consultas.<br />- *Usuario para consultas de universidad*: Podrá ver datos asignados a este rol.<br />- *Ministerio (ministerio, FECYT agencia de ciencia):* Podrá ver los datos asignados a su rol, ejecutar consultas SparQL personalizadas y dispondrán de un mecanismo para añadir/borrar consultas.<br />- *Gobierno regional*: Podrá ver los datos asignados a su rol.<br />- *Agencia Española de investigación*: Podrá ver los datos asignados a su rol. |           |
|        | Cuando el usuario se registra a través de SIR, si este sistema devuelve su rol y hay una equivalencia con los roles existentes en la aplicación, se le asignará su rol automáticamente. |           |
|        | Cuando el usuario se registra a través de SIR, si este sistema devuelve su rol y no hay una equivalencia con los roles existentes en la aplicación, se creará su usuario pero sólo podrá acceder al contenido público del portal. |           |
|        | Los usuarios con rol gestor ASIO podrán crear roles mediante una pantalla. |           |
|        | Los usuarios con rol gestor ASIO podrán modificar roles mediante una pantalla. |           |
|        | Los usuarios con rol gestor ASIO podrán borrar roles mediante una pantalla. |           |
|        | Los usuarios con rol gestor ASIO podrán modificar el rol de un usuario haciendo una búsqueda previa de ese usuario en la aplicación web. |           |
|        | Los usuarios con rol Gestor ASIO podrán configurar en la aplicación web la frecuencia con la que la aplicación lanzará los procesos automáticos para cargar y actualizar los datos. |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |



## Subsistema de administración de contenidos



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | Los usuarios con rol administrador de una universidad podrán crear nuevas ontologías usando ficheros como CSV, XML, Json a través de la web con ficheros con un límite de tamaño. |           |
|        | Los usuarios con rol administrador de una universidad podrán crear nuevas ontologías usando ficheros como CSV, XML, Json a través de un Servicio Rest. |           |
|        | Los usuarios con rol administrador de una universidad podrán modificar  ontologías usando ficheros como CSV, XML, Json a través de la web. |           |
|        | Los usuarios con rol administrador de una universidad podrán modificar  ontologías usando ficheros como CSV, XML, Json a través de un Servicio Rest. |           |
|        | Al importar ontologías por primera vez, a través de cualquier medio, se guardarán los datos, pero las siguientes veces se actualizarán esos datos. |           |
|        | Al crear o modificar ontologías, los campos por defecto tendrán visualización publica, es decir, cualquier usuario, tanto registrados como no registrados, podrán ver los datos de esa ontología. |           |
|        | Los usuarios con rol administrador de una universidad podrán modificar los roles permitidos para visualizar los campos de una ontología a través de una sección en la aplicación web. |           |
|        | Los datos se cargarán de forma inicial con un proceso que los importará de la Universidad de Murcia, SGI Hércules, CVN y dos formatos adicionales que serán proporcionados por la universidad de Murcia para su implementación durante el hito 2. |           |
|        | Los usuarios con rol administrador de una universidad podrán actualizar los datos de las ontologías usando ficheros como CSV, XML, Json a través de la web con ficheros con un límite de tamaño. |           |
|        | Los usuarios con rol administrador de una universidad podrán actualizar los datos de las ontologías usando ficheros como CSV, XML, Json a través de un Servicio Rest. |           |
|        | El sistema dispondrá de un sitio FTP para poder almacenar ficheros de actualización y creación de ontologías. |           |
|        | El sistema dispondrá de un sitio FTP para poder almacenar ficheros de actualización de datos. |           |
|        | El sistema dispondrá de un sistema automático, cuya frecuencia podrá ser configurada por los usuarios con rol Gestor ASIO, que actualizará o creará las ontologías con los ficheros del FTP. |           |
|        | El sistema dispondrá de un sistema automático, cuya frecuencia podrá ser configurada por los usuarios con rol Gestor ASIO, que actualizará o creará los datos de las ontologías con los ficheros del FTP. |           |
|        | Se realizarán actualizaciones increméntales de datos consultando a los distintos SGIs de las universidades que se harán de forma automática. |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |



## Subsistema de consulta de datos



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | La aplicación tendrá una parte pública, los usuarios públicos y todos los usuarios registrados podrán ver estos contenidos públicos. |           |
|        | La aplicación dispondrá de una pantalla de consultas SPARQL que será visible de forma pública y permitirá escribir en texto libre. |           |
|        | En la pantalla de consultas SPARQL se propondrán unas consultas predefinidas en función del rol de los usuarios. |           |
|        | Las consultas predefinidas para los usuarios de ministerios se podrán añadir/borrar mediante una pantalla y un usuario con un rol predeterminado. |           |
|        | Se facilitará la edición de las consultas predefinidas en la pantalla de consulta SPARQL |           |
|        | Se harán sugerencias en la pantalla de consulta SPARQL como pueden ser autocomplete de variables, de entidades almacenadas, de prefijos y vocabularios. |           |
|        | LA pantalla de consultas SPARQL mostrará los datos en distintos formatos como timeline, mapa, y gráficos estadísticos. |           |
|        | La pantalla de consultas SPARQL constará de un asistente de consultas SPARQL. |           |
|        | Una vez realizada la consulta en la pantalla de consultas SPARQL, se mostrarán los datos visibles para el usuario en función de rol o de si son públicos. |           |
|        | En la pantalla de consultas SPARQL, un usuario podrá ver el resultado de las consultas de agregación de los campos que no son visibles para él, por ejemplo, una suma, pero no podrá ver estos datos en detalle. |           |
|        | Se dispondrá de un servicio donde las máquinas puedan hacer consultas mediante GET/POST, con negociación de contenido: En el caso de que una máquina haga un GET con cabeceras Accept de HTML, esa consulta aparecerá ejecutada en el formulario web y con resultado. Por ejemplo: https://query.wikidata.org/#SELECT%20%2a%0AWHERE%20%7B%0A%20%3Fs%20%3Fp%20%3Fo%0A%7D%0ALIMIT%ste |           |
|        | El servicio para que las máquinas realicen consultas describirá el endpoint de la manera más rica posible, utilizando vocabularios como VoID y SPARQL Service Description, para que el endpoint sea lo más “descubrible” posible (Aranda 2013). |           |
|        | La aplicación web tendrá la opción de ver estadísticas generales sobre los datos. |           |
|        | La aplicación web tendrá la opción de realizar dumps de datos para descargar. |           |
|        | La aplicación web tendrá la opción de mostrar para cada Named Graph, una renderización de sus metadatos: DCAT, VoID,PROV, y cualquier otro metadato destacable. |           |
|        | La aplicación web tendrá la opción de ver ejemplos de consultas SPARQL sobre los datos almacenados y cómo ejecutarlas. |           |
|        | La aplicación web tendrá un URI Lookup Service (desarrollado en otro proyecto) para buscar URIs de entidades, a través del contenido de las URIs y a través del contenido de propiedades como rdfs:label o rdfs:comment (Las propiedades a usar serán configurables). |           |
|        | Existirá un URI Lookup Service con interfaz para máquinas para buscar URIs de entidades, a través del contenido de las URIs y a través del contenido de propiedades como rdfs:label o rdfs:comment (Las propiedades a usar serán configurables). |           |
|        | La aplicación web tendrá enlaces a repositorios GitHub (Plataforma Backend SGI, módulos, Test suites, Datasets, especificaciones). |           |
|        | La aplicación web tendrá enlaces a validadores y a resultados de validación: validación de datos y validación de principios FAIR (Infraestructura Ontológica). |           |
|        | La aplicación web tendrá una lista de los backends SGI en activo |           |
|        | Se podrán consultar los datos de contacto en la aplicación web. |           |
|        | La aplicación web mostrará la información del contrato de URIs. |           |
|        | La aplicación web mostrará información sobre el proyecto Hércules y sus objetivos. |           |
|        | Los anteriores 10 requisitos se intentarán generar de la forma más automática posible. |           |
|        |                                                              |           |



## Datos



| Código | Requisito                                                    | Prioridad |
| ------ | ------------------------------------------------------------ | --------- |
|        | Los datos dispondrán de un identificador único y persistente |           |
|        | Los datos deben ser descritos con metadatos descriptivos     |           |
|        | Los metadatos incluyen clara y explícitamente el identificador de los datos que describen. |           |
|        | Los datos se registran o indexan en un recurso con capacidad búsqueda. |           |
|        | Los metadatos serán accesibles incluso cuando los datos ya no se encuentren disponibles |           |
|        | Los (Meta) datos usan un lenguaje formal, accesible, compartido y ampliamente aplicable para la representación del conocimiento. |           |
|        | Los (Meta) datos usan vocabularios que siguen los principios FAIR |           |
|        | Los (Meta) datos incluyen referencias calificadas a otros (Meta) datos. |           |
|        | Los (meta) datos se publican con una licencia de uso de datos clara y accesible. |           |
|        | Los (Meta) datos están asociados con información detallada sobre procedencia. |           |
|        | Los (Meta) datos cumplen con los estándares de la comunidad relevantes para el dominio. |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |
|        |                                                              |           |