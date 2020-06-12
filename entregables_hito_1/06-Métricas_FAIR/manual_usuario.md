![](./images/logos_feder.png)

| Documento | [Métricas FAIR](README.md) - Manual de usuario               |
| --------- | ------------------------------------------------------------ |
| Fecha     | 25/05/2020                                                   |
| Proyecto  | [ASIO](https://www.um.es/web/hercules/proyectos/asio) (Arquitectura Semántica e Infraestructura Ontológica) en el marco de la iniciativa [Hércules](https://www.um.es/web/hercules/) para la Semántica de Datos de Investigación de Universidades que forma parte de [CRUE-TIC](http://www.crue.org/SitePages/ProyectoHercules.aspx) |
| Módulo    | Infraestructura Ontológica                                   |
| Tipo      | Manual de usuario                                            |

# Métricas FAIR - Manual de usuario

El presente documento describe en detalle el proceso de **ejecución y uso** del software para la generación de resultados gráficos del análisis de métricas FAIR.

El script `fairviz.py` se encarga de procesar el fichero CSV que contiene los resultados de la evaluación de los indicadores FAIR para generar una gráfica de barras de niveles FAIR por área, así como gráficas radar de progreso por cada indicador, agrupadas por áreas.

Para más información, consultar el documento de [Análisis de métodos FAIR](https://github.com/HerculesCRUE/ib-asio-docs-/blob/master/entregables_hito_1/05-An%C3%A1lisis_de_m%C3%A9todos_FAIR/ASIO_Izertis_AnalisisDeMetodosFAIR.md), donde se especifica la propuesta de metodología de evaluación FAIR, las referencias y el listado de indicadores, siguiendo las indicaciones del grupo de trabajo [FAIR Data Maturity Model](https://www.rd-alliance.org/groups/fair-data-maturity-model-wg) de la [RDA](https://www.rd-alliance.org/).

## Fichero de entrada

El formato del fichero de entrada requiere 6 columnas obligatorias:
* **FACET**: el tipo de faceta entre *FINDABLE*, *ACCESSIBLE*, *INTEROPERABLE* y *REUSABLE*
* **PRINCIPLE**: identificador de métrica FAIR asociada
* **INDICATOR_ID**: identificador del indicador según la RDA
* **PRIORITY**: prioridad del indicador entre *Essential*, *Important* y *Useful*
* **METRIC**: indica el nivel de implementación del indicador. Es un entero entre 0 y 4
* **SCORE**: indica si el indicador está totalmente implementado (METRIC = 4) o no (METRIC < 4)

La salida que produce el script consta de cuatro ficheros *HTML* con los gráficos, que son almacenados
en la carpeta *plots*.

## Ejecución

Para generar los resultados gráficos de la evaluación de métricas FAIR es necesario ejecutar el siguiente comando:

```bash
python fairviz.py ./data/FAIR_evaluation.csv
```