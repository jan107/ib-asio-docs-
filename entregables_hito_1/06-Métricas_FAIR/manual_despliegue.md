![](./images/logos_feder.png)

| Documento | [Métricas FAIR](README.md) - Manual de despliegue            |
| --------- | ------------------------------------------------------------ |
| Fecha     | 25/05/2020                                                   |
| Proyecto  | [ASIO](https://www.um.es/web/hercules/proyectos/asio) (Arquitectura Semántica e Infraestructura Ontológica) en el marco de la iniciativa [Hércules](https://www.um.es/web/hercules/) para la Semántica de Datos de Investigación de Universidades que forma parte de [CRUE-TIC](http://www.crue.org/SitePages/ProyectoHercules.aspx) |
| Módulo    | Infraestructura Ontológica                                   |
| Tipo      | Manual de despliegue                                         |

# Métricas FAIR - Manual de despliegue

El presente documento describe en detalle el proceso de instalación del software para la generación de resultados gráficos del análisis de métricas FAIR.

## Instalación de software

Para ejecutar el software es necesario tener instalado Python en el equipo. La versión de Python con la que el software se ha desarrollado y probado es [Python v3.6](https://www.python.org/downloads/release/python-360/)

Para el entorno de desarrollo se recomienda la instalación de [PyCharm](https://www.jetbrains.com/pycharm/download/)

No existen requisitos específicos de hardware.

## Instalación de dependencias

Adicionalmente es necesario instalar varias librerías Python definidas en el fichero [requirements.txt](requirements.txt):
```
numpy==1.18.4
plotly==4.7.1
pandas==1.0.3
```
Para la instalación de las dependencias se debe ejecutar el siguiente comando en la consola del equipo destinado a realizar el proceso de generación de resultados gráficos FAIR:

```
pip install -r requirements.txt
```