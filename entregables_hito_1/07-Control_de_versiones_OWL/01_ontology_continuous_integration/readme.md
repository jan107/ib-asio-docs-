![](assets/logos_feder.jpg)

| Entregable     | Control de versiones sobre ontologías OWL                    |
| -------------- | ------------------------------------------------------------ |
| Fecha          | 22/05/2020                                                   |
| Proyecto       | [ASIO](https://www.um.es/web/hercules/proyectos/asio) (Arquitectura Semántica e Infraestructura Ontológica) en el marco de la iniciativa [Hércules](https://www.um.es/web/hercules/) para la Semántica de Datos de Investigación de Universidades que forma parte de [CRUE-TIC](http://www.crue.org/SitePages/ProyectoHercules.aspx) |
| Módulo         | Infraestructura Ontológica                                   |
| Tipo           | Método y Software |
| Objetivo       | El objetivo de este documento representa la estructura documental del sistema de integración continua que se ejecuta sobre la ontología cada vez que se produce un cambio. |
| Estado         | **100%** Se han analizado y aplicado ya varias soluciones para los problemas que emergen al mantener un control de versiones sobre ontologías OWL. Se han definido 5 niveles de soluciones, de los cuales 3 se encuentran ya en funcionamiento, mientras que los últimos 2 se encuentran en fase de implementación. También se ha definido un sistema de integración continua en el que se validan automáticamente los cambios producidos en la ontología a partir de una serie de Shape Expressions. Este sistema se encuentra implementado y en funcionamiento; los siguientes esfuerzos consistirán en la definición de shapes adicionales a las ya existentes. Por último se ha implementado un sistema de sincronización de cambios de la ontología con un triplestore. Este sistema se encuentra en una fase de mejoras. |
| Próximos pasos | Los siguientes pasos son el estudio e implementación de los niveles 4 o 5 definidos en este documento. Tras esto, se actualizará el documento con las decisiones tomadas y resultado obtenidos. |

# Hercules Ontology Continuous Integration Folder Description
This folder includes the following documents, and we recomend the lecture in the next order:

* **system_specification.md:** Constains the system specification and design.
* **user_manual.md:** Constains a user manual to use and modify the system.
* **javadoc/index.html:** Contains all java auto-generated documentation for the system.
