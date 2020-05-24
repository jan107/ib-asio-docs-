![](./images/logos_feder.png)

| Documento | [Métricas FAIR](README.md) - Documentación técnica           |
| --------- | ------------------------------------------------------------ |
| Fecha     | 25/05/2020                                                   |
| Proyecto  | [ASIO](https://www.um.es/web/hercules/proyectos/asio) (Arquitectura Semántica e Infraestructura Ontológica) en el marco de la iniciativa [Hércules](https://www.um.es/web/hercules/) para la Semántica de Datos de Investigación de Universidades que forma parte de [CRUE-TIC](http://www.crue.org/SitePages/ProyectoHercules.aspx) |
| Módulo    | Infraestructura Ontológica                                   |
| Tipo      | Documentación técnica                                        |

# Métricas FAIR - Documentación técnica

El presente documento describe en detalle el proceso de desarrollo del software para la generación de resultados gráficos del análisis de métricas FAIR.
## Entorno de desarrollo
Ver [manual de despliegue](manual_despliegue.md).
## Pruebas unitarias
Para generar los resultados de la evaluación de pruebas unitarias del software de métricas FAIR es necesario ejecutar el siguiente comando:

```
python unit_test.py
```

### Definición de casos de prueba

```
------------------------------TEST1------------------------------
FINDABLE -> ningún esencial -> 0
ACCESSIBLE -> tiene todos los importantes y útiles, pero ningún esencial -> 0
INTEROPERABLE -> tiene  menos del 50 % de los importantes y todos los útiles -> 1
REUSABLE -> tiene todos los esenciales y todos los útiles, pero menos de la mitad de los importantes -> 1

------------------------------TEST2------------------------------
FINDABLE -> todos los esenciales -> 5
ACCESSIBLE -> tiene todos los esenciales, más de la mitad de los importantes y ningún útil -> 2
INTEROPERABLE -> tiene  todos los importantes y ningún útil -> 3
REUSABLE -> tiene todos los esenciales, todos los importantes y ningún útil -> 3

------------------------------TEST3------------------------------
FINDABLE -> ningún esencial -> 0
ACCESSIBLE -> tiene todos los esenciales, todos los importantes y ningún útil -> 3
INTEROPERABLE -> tiene todos los importantes y más de la mitad de útiles -> 4
REUSABLE -> tiene todos los esenciales, todos los importantes y todos los útiles -> 5

------------------------------TEST4------------------------------
FINDABLE -> todos los esenciales -> 5
ACCESSIBLE -> tiene todos los esenciales, todos los importantes y todos los útiles -> 5
INTEROPERABLE -> tiene todos los importantes y todos los útiles -> 5
REUSABLE -> tiene todos los esenciales, todos los importantes y todos los útiles -> 5
```

### Resultados obtenidos

```bash
Ran 4 tests in 0.427s
OK
```