**Multilingüismo (y *multiescriptalismo*) en las ontologías ASIO**

Introducción 
============

Este informe documenta los casos de uso y contextos que se utilizarán en el proyecto Hércules para poner a prueba modelos multilingües (y de multiescriptalismo).

 FIXME

# Reglas del modelo de multilingüismo

Todas las ontologías que se desarrollen estarán planteadas bajo un modelo de multilingüismo. Algunas de las reglas de este modelo se aplican a los siguientes aspectos:

- URIs
- Etiquetas léxicas
- Propiedades de documentación
- Otros metadatos lingüísticos

que analizaremos con algo más de detalle en las subsecciones siguientes.



URIs
----

Preferencia por la utilización de URIs opacas[^1], especialmente para identificadores. Las URIs opacas permiten separar el identificador de la representación en lenguaje natural del recurso. Esta separación se
considera una mejor práctica en entornos multilingües dado que las representaciones textuales deberían obtenerse a partir de las etiquetas multilingües (`rdfs:label`) en lugar del identificador del recurso.

Un ejemplo concreto de URI opaca es el uso de códigos ISO para crear recursos que tienen que ver con países, lenguas o incluso áreas científicas.

Véamos un ejemplo concreto extraído de uno de los módulos verticales que describiremos en una sección posterior:

```
LET ?regionResource = resource(concat("ES_DIVISION_LEVEL_1_",replace(?regionCode,"-","_")),asioModules)
```

En este ejemplo, perteneciente a uno de los programas de transformación de datos tabulares a RDF, podemos *traducir* que el recurso de una Comunidad Autónoma cualquiera del Estado se crea a partir del [código ISO](https://www.iso.org/obp/ui/#iso:code:3166:ES) de tales entidades.

Así por ejemplo, en el caso de la Región de Murcia, el recurso se crearía a partir del código composicional **ES-MC**, cuya primera parte, **ES**, indica el país (España) y la segunda, **MC**, la subdivisión administrativa de primer nivel, en el caso español la *comunidad autónoma*: Región de Murcia.

Una vez creado el recurso a partir de ese código ISO, inserto en la URI y opaco respecto al lenguaje natural, ese recurso puede ya recibir un tratamiento multilingüe, sin causar problemas de codificación, por medio de etiquetas `xml:lang` o `skos:prefLabel`:

```
skos:prefLabel "Región de Murcia"@es ;
skos:prefLabel "Região de Múrcia"@pt ;
skos:prefLabel "Region of Murcia"@en ;
skos:prefLabel "Région de Murcie"@fr ;
skos:prefLabel "Regió de Múrcia"@ca ;
skos:prefLabel "Región de Murcia"@gl ;
skos:prefLabel "Murtziako Eskualdea"@eu ;
skos:prefLabel "Мурсийский Регион"@ru ;
skos:prefLabel "Rexón de Murcia"@ast ;
skos:prefLabel "Регион Мурсија"@sr-Latn ;
skos:prefLabel "Region Mursija"@sr-Cyrl ;
skos:prefLabel "re'xjon̪ de 'muɾθja"@es-ES-fonipa ;
skos:prefLabel "re'xjon̪ de 'muɾθja"@es-ES-fonipa ;
```

que son capas multilingües 