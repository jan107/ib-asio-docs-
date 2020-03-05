# About this document

This document reports the current status of the ASIO ontology files and more specifically it describes *grosso modo* three of the files currently available in our repositories, namely:

- [asio-demo.owl](https://git.izertis.com/universidaddemurcia/semantmurc/asio-docs/blob/master/entregables_hito_1/01-Red_de_Ontolog%C3%ADas_H%C3%A9rcules/asio-demo.owl)
- [asio-dcat-mappings.ttl](https://git.izertis.com/universidaddemurcia/semantmurc/asio-docs/blob/master/entregables_hito_1/01-Red_de_Ontologías_Hércules/asio-dcat-mappings.ttl)
- [asio-vertical-module-geopolitical.ttl](https://git.izertis.com/universidaddemurcia/semantmurc/asio-docs/blob/master/entregables_hito_1/01-Red_de_Ontologías_Hércules/asio-vertical-module-geopolitical.ttl)

The first one is the ***core*** ontology and the second one corresponds to the class-by-class ***alignements*** towards external vocabularies

In addition to these two files, a number of ***vertical modules*** are going to be released little by little and the third file listed above is an early release of the **geopolitical module**.

As far as the **vertical modules** are concerned another three final candidates are being implemented so far, in particular:

- administrative entities
- scientific domains
- Spain's university staffing

However, in this first version of the document we describe with some detail just the first and the third vertical modules (*geopolitical entities* and *scientific domains*).

These vertical modules will be dealt with later on.

FIXME

# Introduction

FIXME

Fodor's the modularity of mind ->

**FIXME** The second can be described as a "vertical" view because it claims that our mental faculties are domain specific, genetically determined, associated with distinct neurological structures, and so on.[[21\]](https://en.wikipedia.org/wiki/Jerry_Fodor#cite_note-FF-21) 

[...]

Two properties of modularity in particular, *informational encapsulation* and *domain specificity*, make it possible to tie together questions of functional architecture with those of mental content. The ability to elaborate information independently from the background beliefs of individuals that these two properties allow Fodor to give an [atomistic](https://en.wikipedia.org/wiki/Atomism) and causal account of the notion of mental content. The main idea, in other words, is that the properties of the contents of mental states can depend, rather than exclusively on the internal relations of the system of which they are a part, also on their causal relations with the external world.[[22\]](https://en.wikipedia.org/wiki/Jerry_Fodor#cite_note-Fodor2-22)  **FIXME**

# Core ontology

This early version of the core ontology is focused on addressing the competence questions provided by the University of Murcia and it includes already all the high-level classes necessary to deal with them and the queries thereof.



## imported vocabularies

Two external vocabularies are imported to deal with specific-knowledge domains interesting for the project:

Research object

SWEET Ontology Human Technology Readiness





en el primero se incluyen ya todas las clases de alto nivel que necesitan ser modeladas y se va descendiendo en el modelado con mayor o menor profundidad dependiendo del área. todas esas entidades están documentadas con comments y también incluyen etiquetas multilingües, a saber:

## multilingualism in the core ontology

The entire list of classes in the core ontology is enriched multilingually via the data property `rdfs:label` and besides the two obvious working languages (English, Spanish), three more languages are included: Catalan, French and Portuguese.

The motivation of this choice is on the one hand geopolitical as Catalan, French and Portuguese are languages in contact with Spanish through land and/or maritime borders (Andorra, France, Portugal) and, on the other hand, practical, as those three languages are more or less mastered by members of the development team.

The Iberian peninsula (and some of its neighboring languages) is taken hence as a scale model of the European as a very intuitive advancement from the ultralocal to the global context.

inglés

# Alignements

FIXME

el segundo es el fichero de mapeos hacia otros vocabularios, utilizando la propiedad de OWL "equivalentClass", que es mucho menos arriegada lógicamente y más funcional que la tan vituperada "sameAs".



# Vertical modules

FIXME

As we have already aforementioned, in addition to the core ontology and complementarily thereof



and the alignmente two files, a number of *vertical modules* are going to be released little by little. Currently, there are four final candidates:

## geopolitical entities

FIXME

TO BE TRANSLATED:

El otro módulo vertical ya avanzado en diseño aunque aún no totalmente implementado es el correspondiente al modelo geopolítico. En una primera fase, el módulo se limitará a España y sus niveles administrativos (nación, comunidad autónoma, provincia y municipio) y con futuras implementaciones que incluirán en principio países limítrofes (Andorra, Francia, Portugal) y tal vez alguno más cuyas etiquetas lingüísticas incluyan otros sistemas de escritura dentro de la Unión Europea, como Grecia o Bulgaria, estos últimos con el fin de testear el citado *multiescriptalismo*.

También se eligió SKOS para la modelización de este módulo dado el modelo jerárquico obvio de las entidades geopolíticas.

## administrative entities

FIXME

## scientific domains

The [Spain's Ministry of Science, Innovation and Universities](http://www.ciencia.gob.es/), through its [State Research Agency](http://www.ciencia.gob.es/portal/site/MICINN/menuitem.8d78849a34f1cd28d0c9d910026041a0/?vgnextoid=664cfb7e04195510VgnVCM1000001d04140aRCRD), published a document featuring a number of [**Scientific domains**](http://www.ciencia.gob.es/stfls/MICINN/Ayudas/PE_2013_2016/PE_Promocion_e_Incorporacion_Talento_y_su_Empleabilidad/FICHEROS/SE_Incorporacion/Ayudas_contratos_RYC_2016/Clasificacion_areas_cientificas_2016_AEI.pdf) which are the basis for several among the competence questions provided by the University of Murcia in order to model the ontology.

After a thorough analysis of that document, a clear hierarchical structure of domains and subdomains was identified and it was deemed as seamlessly fitting a thesaurus-like structure and hence suitable to be transformed into the W3C's standard for controlled vocabularies [SKOS-Core](https://www.w3.org/TR/swbp-skos-core-spec/).

SKOS_core is not just the most appropriate solution for such a document featuring a level-structure thesaurus-like fully exploiting its classes `skos:Concept` (for *agglutinating* concepts) and `skos:ConceptScheme` (in order to arrange concepts *knitting* them together into concept schemes), but it also provides means to include models densely multilingual, as checkable with some European thesauri such as [GEMET]([ttps://www.eionet.europa.eu/gemet/en/about/](https://www.eionet.europa.eu/gemet/en/about/)) or [EuroVoc](https://data.europa.eu/euodp/en/data/dataset/eurovoc).

Hence, besides being able to seamlessly *assimilate* these **Scientific domains** within the ASIO ontology through an *ad hoc*, vertical module, we have improved the Ministry's document in a number of ways:

- processing and transforming it from an only-reading format (PDF), which would be categorised as simply [linked data](https://www.w3.org/DesignIssues/LinkedData.html) of low-quality or 1-star ("Available on the web (whatever format) *but with an open licence, to be Open Data*"), to a high-quality, or 5-star, linked data format ("non-proprietary format (e.g. CSV instead of excel), open standards from W3C (RDF and SPARQL) to identify things and link your data to other people’s data to provide context").
- exploiting the full possibilities of multiligualism provided by SKOS 
- 
- exploitation to the dataset.













- el segundo paso fue explotar plenamente las posibilidades de multilingüismo de SKOS con el fin de internacionalizar y localizar el *dataset*, entendiendo *internacionalizar* y *localizar* como los procesos de diseñar recursos informáticos de manera tal que puedan adaptarse a diferentes idiomas y regiones sin la necesidad de realizar cambios de ingeniería ni en el código porteriores. De esta forma, las etiquetas lingüísticas de las áreas científicas, en el original únicamente disponibles en español, han sido adaptadas un contexto multilingüe que incluye el inglés como *lingua franca*, dos lenguas en contacto con el español por frontera directa, el portugués y el francés, lenguas cooficiales de España como el catalán, el vasco y el gallego, y otras variedades con cierto reconocimiento a nivel regional, como el occitano, el aragonés o el asturiano, estas últimas con un menor desarrollo.

Además de las posibilidades de explotación ontológica que proporciona SKOS, que no deja de ser una ontología a su vez, con respecto al *core* de ASIO, las etiquetas multilingües suponen una materia prima interesante para llevar a cabo muchas pruebas *lingüísticas*.

## Spain's university staffing

FIXME

# References

FIXME

## Web references

FIXME

## Bibliographical references

FIXME

Fodor, J. A. (1983). *The modularity of mind*. Bradford/MIT Press, Cambride, Mass. 



