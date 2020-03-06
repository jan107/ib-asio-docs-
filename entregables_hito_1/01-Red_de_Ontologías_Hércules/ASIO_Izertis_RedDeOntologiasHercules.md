# 0. About this document

This document reports the current status of the ASIO ontology files and more specifically it describes *grosso modo* three of the files currently available in our repositories, namely:

- [asio-demo.ttl](https://git.izertis.com/universidaddemurcia/semantmurc/asio-docs/blob/master/entregables_hito_1/01-Red_de_Ontolog%C3%ADas_H%C3%A9rcules/asio-demo.owl)
- [asio-dcat-mappings.ttl](https://git.izertis.com/universidaddemurcia/semantmurc/asio-docs/blob/master/entregables_hito_1/01-Red_de_Ontologías_Hércules/asio-dcat-mappings.ttl)
- [asio-vertical-module-geopolitical.ttl](https://git.izertis.com/universidaddemurcia/semantmurc/asio-docs/blob/master/entregables_hito_1/01-Red_de_Ontologías_Hércules/asio-vertical-module-geopolitical.ttl)

The first one is the ***core*** ontology and the second one corresponds to the class-by-class ***alignements*** towards external vocabularies

In addition to these two files, a number of ***vertical modules*** are going to be released little by little. An early release is the **geopolitical module** (the third file listed above) including so far just the geopolitical entities of Andorra, Spain and Portugal (France is the other country to be taken into account in this vertical module in the next update). At the moment of this writing, three more vertical modules are almost ready to be released, as we will see in the section devoted to these modules.

Keep in mind that both this document and the ontology files are a work in progress and the deadline to deliver the 80% of the specification is mid May.



# 1. Introduction

The ASIO ontology design is loosely inspired in the principles of informational encapsulation and domain specificity 

Fodor's the modularity of mind ->

**FIXME** The second can be described as a "vertical" view because it claims that our mental faculties are domain specific, genetically determined, associated with distinct neurological structures, and so on. 

[...]

Two properties of modularity in particular, *informational encapsulation* and *domain specificity*, make it possible to tie together questions of functional architecture with those of knowledge content. The ability to elaborate information independently from the background knowledge that these two properties allow us to give an atomistic and causal account of the notion of knowledge content. The main idea, in other words, is that the properties of the contents of mental states can depend, rather than exclusively on the internal relations of the system of which they are a part, also on their causal relations with the external world. **FIXME**



In the second section we consider Fodor’s famous proposal for understanding the large-scale organization of the mind. We need to distinguish, he argues, between two fundamentally different types of cognition. On the one hand, there are highly specialized information-processing tasks, such as identifying the outlines of objects in the immediate environment, or working out where the gaps between words come in a stream of sound. These tasks are carried out automatically, and involve only a limited amount of information. In his influential book The Modularity of Mind (1983) Fodor argues that tasks of this first kind are carried out by dedicated cognitive systems that he called modules. These modules are domain-specific – that is, they are responsible only for tasks falling in particular domains. On the other hand, there are tasks, such as deciding where to have dinner or how to plant the front garden, that involve much more complex and wide-ranging inferences and to which an indefinite amount of background information is potentially relevant. The information processing involved in carrying out these tasks is domaingeneral (the opposite of domain-specific). On the basis of this analysis, Fodor develops a picture of the organization of the mind as involving both specialized modules and what he calls domain-general, non-modular cognition. In the final section I look at the relation between these two claims. There



# 2. Core ontology

## 2.1. prolegomena

This first version of the core ontology ([asio-demo.ttl](https://git.izertis.com/universidaddemurcia/semantmurc/asio-docs/blob/master/entregables_hito_1/01-Red_de_Ontolog%C3%ADas_H%C3%A9rcules/asio-demo.owl)) is chiefly focused on addressing the competence questions provided by the University of Murcia and it includes already all the high-level classes necessary to deal with them.



## 2.2. the core ontology at a glance

To guide the reader in the understanding of this core ontology it may be useful to take into account some of the competence questions relying under the ontology modelling. Let's have a look at some of the most representative and/or easy-to-grasp:



example of competence question 1 here

corresponding diagram here

![1st-example](./images/glance1.png)



example of competence question 2 here

corresponding diagram here







## 2.3. imported vocabularies

Two external vocabularies are imported to deal with specific-knowledge domains of relevance for the project:

- [Research object](https://wf4ever.github.io/ro/2016-01-28/)

- [SWEET Ontology Human Technology Readiness](https://esipfed.github.io/stc/sweet_lode/humanTechReadiness.html)

These two vocabularies are used by the ASIO ontology to relate the core ontology and its clases to two  entities that currently are pivotal to university research projects. 

**Research objects** aggregate a number of resources that are used and/or produced in a given scientific research and in the ASIO ontology are linked to the scientific domains described in the eponymous, ad hoc vertical module described later on.

The **technology readiness levels (TRLs)**, initially developed at NASA during the 1970s and from there included by the European Commission's EU Horizon 2020 program (Mihaly, 2017), are a method for estimating the maturity of technologies during the acquisition phase of a program. They condition therefore any European project proposal and development and are currently a critical factor for research projects. The ASIO ontology takes advantage of this mini-ontology part of the SWEET ontology family by importing it.



## 2.4. multilingualism in the core ontology

The entire list of classes in the core ontology is enriched multilingually via the data property `rdfs:label` and, besides the two obvious working languages (English, Spanish), three more languages are included: Catalan, French and Portuguese, as corresponding to the three other countries that we take into account in addition to Spain: Andorra, France and Portugal.

The motivation of this choice is, on the one hand, geopolitical, as Catalan, French and Portuguese are languages in contact with Spanish through land and/or maritime borders (Andorra, France, Portugal) and, on the other hand, practical, as those three languages are more or less mastered by members of the development team, something that ensures a direct multilingual treatment. Note also that Catalan is also a coofficial language in some Autonomous Communities of Spain.

The Iberian peninsula as a *multilingual* whole, besides English as a *lingua franca* and French as a relevant neighboring language, is taken hence as a *scale model* of the multilingual nature of the European Union, and *exploited* as an intuitive advancement from the ultralocal reality to the global context, something that the British sociologist Roland Robertson coined *glocalization* (Kumaravadivelu, 2008:45).



# 3. Alignements with other vocabularies

In addition to reusing specific classes and properties or importing full external vocabularies of interest, as described above, the ASIO ontology also provides mappings to classes considered equivalent to the ones defined in the specification.

To do so, the second file ([asio-dcat-mappings.ttl](https://git.izertis.com/universidaddemurcia/semantmurc/asio-docs/blob/master/entregables_hito_1/01-Red_de_Ontologías_Hércules/asio-dcat-mappings.ttl)) gathers together a thorough study of equivalent classes belonging to related vocabularies and maps them to the ASIO vocabulary via the OWL property `owl:equivalentClass`. This property is safer than the *risky* property `owl:sameAs`, which logical implications might wreak havoc because of undesired inheritances and collateral damages.

The same applies to relevant properties belonging to concurrent vocabularies, which are being mapped in this file using `owl:equivalentProperty`.

More details about these alignments will be provided in more consolidated documentation to be generated soon, but right now it suffices to access the file using a source code editor and have a look at the large list of equivalences, chiefly focusing on concomitant vocabularies such as CERIF, VIVO or the SPAR family of ontologies but also going beyond these ones.



# 4. Vertical modules

As we have already aforementioned, following loosely the influence of Fodor's in addition to the core ontology and complementary to it.



and the alignment of the two files, a number of *vertical modules* are going to be released little by little. Currently, there are four final candidates:



As far as the **vertical modules** are concerned another three final candidates are being implemented so far, in particular:

- administrative entities
- scientific domains
- Spain's university staffing

However, in this first version of the document we describe with some detail just the first and the third vertical modules (*geopolitical entities* and *scientific domains*).



Ideal playground for multilingualism and multiscriptalism





## 4.1. geopolitical entities

As we mentioned at the beginning of this document, the more advanced vertical module so far, already released in an early version, is the geopolitical one. It covers at the moment the geopolitical subdivisions of:

- Andorra: implementing just the first-level subdivisions (*parròquies*)
- Portugal: implementing both the first (*distritos e regiões*) and the second-level (*municípios*) subdivisions.
- Spain: covering the first (*comunidades autónomas*), the second (*provincias*) and the third-level subdivisions (*municipios*).

At the moment of this writing France and its subdivisions (*régions*  and *départements*) are being transformed and is expected to be released in the next weeks, linked to the other datasets.

SKOS-Core was also chosen to model a clearly hierarchical domain and the dataset is massively enriched multilingually and ponderously linked to relevant national and international vocabularies. 

The main goal of this vertical module, which is in a way also transversal, is to geopolitically *locate* agents, organizations and other resources included in the ASIO ontology with an encompassing granularity.



## 4.2. administrative entities

This vertical module is designed to encompass all the relevant entities belonging to Spain's *administración autonómica* related to the geopolitical subdivisions of the previous vertical module, to which they are going to be seamlessly linked.

It is, at the moment of this writing, a work in progress but the implementation so far includes the first-level bodies of *administración autonómica* (*conserjerías*), as available at Spain's administration portal [[1]](https://administracion.gob.es/pagFront/espanaAdmon/directorioOrganigramas/comunidadesAutonomas/comunidadesAutonomas.htm?idCCAA=14), and the second-level [[2]](https://administracion.gob.es/pagFront/espanaAdmon/directorioOrganigramas/fichaUnidadOrganica.htm?idUnidOrganica=123276&origenUO=comunidadesAutonomas&volver=comunidadesAutonomas&idCCAA=14), mainly *direcciones generales* and *consorcios*.

The implementation of this vertical module is carried out using SKOS-Core.



## 4.3. scientific domains

**Note** that this vertical module is being implemented at the moment and it is not included in this release but, as it is already designed, we include already documentation about it. The transformation of the tabular data will be carried out in the next weeks to be be *plugged in* as vertica module.

### 4.3.1 prolegomena

The [Spain's Ministry of Science, Innovation and Universities](http://www.ciencia.gob.es/), through its [State Research Agency](http://www.ciencia.gob.es/portal/site/MICINN/menuitem.8d78849a34f1cd28d0c9d910026041a0/?vgnextoid=664cfb7e04195510VgnVCM1000001d04140aRCRD), published a document featuring a number of [**Scientific domains**](http://www.ciencia.gob.es/stfls/MICINN/Ayudas/PE_2013_2016/PE_Promocion_e_Incorporacion_Talento_y_su_Empleabilidad/FICHEROS/SE_Incorporacion/Ayudas_contratos_RYC_2016/Clasificacion_areas_cientificas_2016_AEI.pdf) which are the basis for several ones among the competence questions provided by the University of Murcia in order to model the ontology.

### 4.3.2. modelling & transformation

After a thorough analysis of that document, a clear hierarchical structure of domains and subdomains was identified and it was deemed as seamlessly fitting a thesaurus-like structure and hence suitable to be ontologically transformed using the W3C's standard for controlled vocabularies: [SKOS-Core](https://www.w3.org/TR/swbp-skos-core-spec/).

SKOS-Core is not just the most appropriate solution for such a document featuring a level-structure thesaurus-like fully exploiting its classes `skos:Concept` (for *agglutinating* concepts) and `skos:ConceptScheme` (in order to arrange concepts *knitting* them together into schemes of concepts), but it also provides means to include models densely multilingual, as checkable with some European thesauri such as [GEMET]([ttps://www.eionet.europa.eu/gemet/en/about/](https://www.eionet.europa.eu/gemet/en/about/)) or [EuroVoc](https://data.europa.eu/euodp/en/data/dataset/eurovoc).

### 4.3.3. added value

Hence, besides being able to seamlessly *assimilate* these **Scientific domains** within the ASIO ontology through an *ad hoc*, vertical module, we have improved the Ministry's document in a number of ways:

- processing and transforming it from an only-reading format (PDF), which would be categorised as simply [linked data](https://www.w3.org/DesignIssues/LinkedData.html) of low-quality or 1-star ("Available on the web (whatever format) *but with an open licence, to be Open Data*"), to a high-quality, or [5-star quality](https://www.w3.org/community/webize/2014/01/17/what-is-5-star-linked-data/), linked data format ("non-proprietary format (e.g. CSV instead of excel), open standards from W3C (RDF and SPARQL) to identify things and link your data to other people’s data to provide context").
- exploiting the full possibilities of multiligualism provided by SKOS with the aim of internationalising and localising the dataset, understanding here *internationalising* and *localising* as the processes to design an IT resource as fully adaptable to different languages and regions without later having to reengineering or changing the code. This way, the language labels for the scientific domains, originally just in Spanish, have been adapted to a multilingual context which not only English as *lingua franca* but also three languages in contact with Spanish through land borders (Catalan, French and Portuguese) and a number of cooficial regional languages (the aforementioned Catalan but also Basque and Galician) and even some linguistic varieties with a certain recognition at regional level (Aragonese, Asturian, Occitan).

In addition to the ontological possibilities offered by SKOS, which is itself an ad hoc ontology, with respect to the ASIO core ontology, these mentioned multilingual labels provide idoneous raw materials to carry out extensively testing with respect to multilingualism, as detailed in the previous section and in a complementary deliverable (*ModeloMultilinguismo*).



## 4.4. Spain's university staffing

Finally, all the specificities of the teaching-and-research positions in the universities of Spain are dealt with in this vertical module, which is still a working progress.



# 5. References

Fodor, J. A. (1983). *The modularity of mind*. Bradford/MIT Press, Cambride, Mass. 

Kumaravadivelu, B. (2008). *Cultural Globalization and Language Education*. Yale University Press.

Mihaly, Heder (2017). "From NASA to EU: the evolution of the TRL scale in Public Sector Innovation". *The Innovation Journal*. 22: 1–23.



