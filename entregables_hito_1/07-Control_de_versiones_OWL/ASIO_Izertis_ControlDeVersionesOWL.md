![](./resources/logos_feder.png)

| Entregable     | Control de versiones sobre ontologías OWL                    |
| -------------- | ------------------------------------------------------------ |
| Fecha          | 25/05/2020                                                   |
| Proyecto       | [ASIO](https://www.um.es/web/hercules/proyectos/asio) (Arquitectura Semántica e Infraestructura Ontológica) en el marco de la iniciativa [Hércules](https://www.um.es/web/hercules/) para la Semántica de Datos de Investigación de Universidades que forma parte de [CRUE-TIC](http://www.crue.org/SitePages/ProyectoHercules.aspx) |
| Módulo         | Infraestructura Ontológica                                   |
| Tipo           | Método y Software |
| Objetivo       | El objetivo de este documento es la especificación de las decisiones tomadas para intentar solucionar los problemas que emergen cuando se intenta mantener un control de versiones efectivo durante el desarrollo de ontologías. |
| Estado         | **100%** Se han analizado y aplicado ya varias soluciones para los problemas que emergen al mantener un control de versiones sobre ontologías OWL. Se han definido 5 niveles de soluciones, de los cuales 3 se encuentran ya en funcionamiento, mientras que los últimos 2 se encuentran en fase de implementación. También se ha definido un sistema de integración continua en el que se validan automáticamente los cambios producidos en la ontología a partir de una serie de Shape Expressions. Este sistema se encuentra implementado y en funcionamiento; los siguientes esfuerzos consistirán en la definición de shapes adicionales a las ya existentes. Por último se ha implementado un sistema de sincronización de cambios de la ontología con un triplestore. Este sistema se encuentra en una fase de mejoras. Todos los objetivos del Hito 1 se encuentran cumplidos, y se espera una evolución para el Hito 2 con las mejoras descritas previamente. |
| Próximos pasos | Los siguientes pasos son el estudio e implementación de los niveles 4 y 5 definidos en este documento. Tras esto, se actualizará el documento con las decisiones tomadas y resultados obtenidos. |
| Documentación adicional | [Manual de usuario integración continua](01_ontology_continuous_integration/user_manual.md)<br />[Especificación del sistema de integración continua](01_ontology_continuous_integration/system_specification.md)<br />[Documentación del sistema de sincronización (incluye manuales y especificación del sistema)](02_hercules_synchronization/hercules_sync_doc.md) |

# Control de versiones sobre ontologías OWL.
Este documento se centra en explicar las decisiones tomadas para intentar solucionar los problemas que emergen cuando se intenta mantener un control de versiones efectivo durante el desarrollo de ontologías.

## Introducción
Una problemática conocida de las ontologías es su serialización no determinista. Esto implica que realizar un control de versiones efectivo sobre ellas sea imposible. En el siguiente [artículo](https://rd.springer.com/chapter/10.1007/978-3-319-99701-8_10) se puede ver más en detalle la problemática descrita.

Sin embargo existen distintas metodologías y procesos que se pueden aplicar para paliar este problema. De forma que se puede a llegar a desarrollar una ontología bajo un control de versiones en el que los cambios realizados queden registrados de forma unívoca.

## Solución planteada
A continuación describiremos la solución que hemos planteado para solucionar la problemática descrita previamente. Nuestra solución se divide en cinco niveles ortogonales y totalmente complementarios, con distintos niveles de completitud actualmente. La primera es una solución sintáctica, mientras que el resto serían soluciones a nivel semántico. Estos niveles se describirán a continuación.

### Nivel 1: Ontología
A nivel de la ontología, planteamos una solución sintáctica que es obligar el uso del editor [Protégé](https://protege.stanford.edu) por parte de los contribuidores de la ontología. En las últimas versiones de Protégé, basado en OWLAPI, se mantiene un orden determinista en la serialización de las ontologías que permite un mayor seguimiento de las diferencias entre versiones. Información adicional sobre el algoritmo implementado para mantener un orden determinista puede ser consultada a través del [siguiente issue](https://github.com/owlcs/owlapi/issues/273) del repositorio de OWLAPI. Además, en el [siguiente artículo](https://cgi.csc.liv.ac.uk/~valli/OWLED2015/OWLED_2015_paper_12.pdf) se especifica en detalle las optimizaciones llevadas a cabo en los algoritmos de serialización de ontologías.

### Nivel 2: Sistema de control de versiones
El propio sistema de control de versiones (en nuestro caso GitHub, basado en Git) también hay bastantes soluciones dispobibles para el problema presente.

Una de las soluciones que hemos llevado a cabo es el almacenamiento de forma independiente de cada una de las versiones de la ontología a traves de la rama donde ésta se encuentra publicada (gh-pages). Cada vez que se crea una nueva release en GitHub, se lanza un sistema de scripts que se encarga de mergear cada uno de los grafos procedentes de la ontología (core + módulos verticales + alignments) y de serializar el grafo mergeado en la rama gh-pages, junto con la información del día en el que se produjo esa versión. Esta serialización se lleva a cabo con la librería [rdflib](https://rdflib.readthedocs.io/en/stable/) de Python, y está implementada de forma determinista.

Por último, la organización de carpetas correspondientes a la publicación de la ontología sigue un criterio de nombrado ya utilizado por ejemplo en las [SPAR Ontologies](https://sparontologies.github.io/article/spar-iswc2018/), que facilita el acceso y uso de cada una de las versiones por parte de los consumidores.

### Nivel 3: Wikibase
A nivel de Wikibase, el propio software tiene un sistema de control de cambios que nos permite obtener información adicional sobre los cambios que se han realizado. Estos cambios incluyen un timestamp, información sobre la cuenta que los ha realizado, así como la opción de poder revertir los cambios que sean necesarios. En la siguiente imagen se puede observar a modo de ejemplo este sistema de versiones que ofrece Wikibase:
![](./resources/wikidata_recent_changes.png)

Aunque este sistema fue originalmente diseñado como medida para evitar posibles actos de vandalismo a nivel de datos por parte de contribuyentes externos, creemos que nos puede ofrecer una gran base para poder manejar el control de versiones y cambios que se realicen en la ontología, la cuál se encontrará publicada en este sistema.

### Nivel 4: Sincronización a wikibase
Actualmente Wikibase ya ofrece información sobre la evolución de los datos que guarda y por tanto se puede seguir el rastro de las distintas versiones de los componentes de una ontología. Sin embargo, el sistema de propagación de cambios diseñado permitiría enriquecer aún más esta información.

Desde este sistemas sería posible añadir metadatos adicionales en el momento de la sincronización de la ontología con Wikibase. Estos metadatos pueden incluir por ejemplo el fichero original a través del cual se realizó la sincronización, y otros datos procedentes del propio sistema de control de versiones, como puede ser el issue o el pull request relacionado con el cambio.

Actualmente este nivel todavía no se encuentra implementado en el sistema de sincronización, pero es algo que tenemos contemplado y nuestra idea es implementar este nivel de cara a futuras versiones del sistema de sincronización.

### Nivel 5: Sincronización desde Wikibase
Este nivel se correspondería con la sincronización de cambios que se produzcan en Wikibase al sistema de control de versiones donde se almacena la ontología (sincionización hacia atrás).

Por ejemplo, sería posible añadir metadatos a la propia ontología indicando la versión y la procedencia de estos cambios.

Dado que la sincronización hacia atrás todavía es una funcionalidad que no se encuentra disponible en el sistema de sincronización, este nivel todavía se encuentra en una fase de análisis y exploración por nuestra parte. A medida que se vaya avanzando en la funcionalidad, se irían concretando las medidas adicionales que podrían llevarse a cabo en este nivel.

## Validación de los cambios en el sistema de control versiones
Una vez se han producido cambios sobre la ontología y por tanto en el control de versiones es necesario validar que estos cambios no tienen un efecto negativo sobre las versiones ya existentes de la ontología. Esto es, que por ejemplo no se empleé un prefijo que no ha sido definido con anterioridad, algo que sintácticamente es posible pero semánticamente produciría un error en los sistemas que consuman la ontología en el futuro.

Para ver como se soluciona este problema se ha diseñado e implementado un sistema de integración continua que se ejecuta cada vez que se produce un cambio en la ontología dentro del sistema de control de versiones. Toda la documentación referente a este sistema se encuentra dentro de la carpeta `01_ontology_continuous_integration` de este mismo directorio.

## Propagación de los cambios al triplestore
Una vez los cambios en la ontología han pasado el proceso de validación, y los administradores de ésta consideran que se puede crear una nueva versión estable, se procederá a la sincronización de los cambios producidos en la ontología a Wikibase.

Estos cambios se realizarán de forma automática cada vez que se realice una nueva [release](https://help.github.com/en/enterprise/2.13/user/articles/creating-releases) en el repositorio donde la ontología se encuentra almacenada. Toda la documentación sobre este sistema se encuentra dentro de la carpeta `02_hercules_synchronization` de este directorio.