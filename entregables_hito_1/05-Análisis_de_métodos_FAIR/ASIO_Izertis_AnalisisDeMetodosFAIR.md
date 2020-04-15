![](./images/logos_feder.png)

# Análisis de métodos FAIR

Los principios FAIR (Findable, Accesible, Interoperable, Reusable) surgieron como una iniciativa para **mejorar la interoperabilidad de los datos científicos publicados** [Wilkinson, 2016; Wilkinson, 2016b; Rodriguez Iglesias, 2016; Mons, 2017]. 

El uso de principios FAIR está teniendo una rápida expansión en los últimos años [Mons 2017]. En Europa, la Comisión Europea pide que los [Data Management Plans de los proyectos financiados se guíen por los principios FAIR](http://ec.europa.eu/research/participants/data/ref/h2020/grants_manual/hi/oa_pilot/h2020-hi-oa-data-mgt_en.pdf). En Estados Unidos, la iniciativa [Big Data to Knowledge (BD2K)](https://commonfund.nih.gov/bd2k), del National Institute of Health, tiene como objetivo en su segunda fase publicar los resultados obtenidos en la primera de acuerdo a los principios FAIR y [todos los recursos desarrollados por BD2K](https://commonfund.nih.gov/bd2k/resources) se publican de forma abierta para la comunidad investigadora. Incluso el G20, en su [encuentro de 2016 en Hangzhou (China)](http://europa.eu/rapid/press-release_STATEMENT-16-2967_en.htm), mencionó los principios FAIR. 

Además, revistas de gran prestigio como [Nature Genetics](https://www.nature.com/ng/) o [Scientific Data](https://www.nature.com/sdata/) promueven el uso de principios FAIR en los datasets que reciben [Nature Genetics, 2017] . A su vez, hay cada vez más, proyectos que se rigen por principios FAIR [Wilkinson 2016]: [Dataverse](https://dataverse.org/), [FAIRDOM](https://fair-dom.org/), [ISA](https://www.isacommons.org/), [Open Phacts](https://www.openphacts.org/), [wwPDB](http://www.wwpdb.org/), [UniProt](http://insideuniprot.blogspot.com/2016/11/being-fair-at-uniprot.html), [DataGraft](https://datagraft.io/) y [BlueBrain](https://bluebrainnexus.io/) entre otros.

Los principios FAIR **no son un estándar, ni una especificación, y tampoco definen una implementación tecnológica concreta**; más bien, los principios FAIR son una guía general de cómo deberían publicarse los datos (los datos no *cumplen* con FAIR, siempre se puede mejorar en la escala FAIR). 

Dicho esto, hoy en día, **la mejor manera de publicar datos FAIR es hacerlo mediante Linked Data**, teniendo especial cuidado de generar datos y metadatos de alta calidad, mejorando así la reusabilidad de los datos para máquinas, y, como consecuencia y en última instancia, para humanos. 

La utilización de research objects está también muy alineada con los principios FAIR y un objetivo del presente proyecto será profundizar en esta línea. De hecho, actualmente se está desarrollando la herramienta [Ro-curate]([https://github.com/ResearchObject/ro-curate) para validar *research objects* utilizando Shapes.

## Principios FAIR

A continuación se describen los principios FAIR en detalle:

**FINDABLE** (encontrable): Los datos y metadatos pueden ser encontrados por la comunidad después de su publicación, mediante herramientas de búsqueda.

-  F1. Asignarles un identificador único y persistente a los datos y los metadatos.
-  F2. Describir los datos con metadatos de manera prolija (*rich metadata*).
-  F3. Registrar/Indexar los datos y los metadatos en un recurso de búsqueda.
-  F4. En los metadatos se debe especificar el identificador de los datos que se describen.

**ACCESSIBLE** (accesible): Los datos y metadatos están accesibles y por ello pueden ser descargados por otros investigadores utilizando sus identificadores.

-  A1 Los datos y los metadatos pueden ser recuperados por sus identificadores mediante protocolos estandarizados de comunicación.
-  A1.1 Los protocolos tienen que ser abiertos, gratuitos e implementados universalmente.
-  A1.2 El protocolo debe de permitir procedimientos para la autentificación y la autorización.
-  A2 Los metadatos deben de estar accesibles, incluso cuando los datos ya no estuvieran disponibles.

**INTEROPERABLE** (interoperable): Tanto los datos como los metadatos deben de estar descritos siguiendo las reglas de la comunidad, utilizando estándares abiertos, para permitir su intercambio y su reutilización.

-  I1. Los datos y los metadatos deben de usar un lenguaje formal, accesible, compartible y ampliamente aplicable para representar el conocimiento.
-  I2. Los datos y los metadatos usan vocabularios que sigan los principios FAIR.
-  I3. Los datos y los metadatos incluyen referencias cualificadas a otros datos o metadatos.

**REUSABLE** (reutilizable): Los datos y los metadatos pueden ser reutilizados por otros investigadores, al quedar clara su procedencia y las condiciones de reutilización.

-  R1. Los datos y los metadatos contienen una multitud de atributos precisos y relevantes.
-  R1.1. Los datos y los metadatos se publican con una licencia clara y accesible sobre su uso y reutilización.
-  R1.2. Los datos y los metadatos se asocian con información sobre su procedencia.
-  R1.3. Los datos y los metadatos siguen los estándares relevantes que usa la comunidad del dominio concreto.

## Metodología de evaluación de principios FAIR

Los principios se refieren a tres tipos de entidades: **datos** (o cualquier objeto digital), **metadatos** (información sobre ese objeto digital) e **infraestructura**. Por ejemplo, el principio F4 define que tanto los metadatos como los datos se registran o indexan en un recurso de búsqueda (el componente de infraestructura).

En general, el **uso de datos enlazados favorece el cumplimiento de los principios FAIR**. Por ejemplo, el uso de URIs para identificar recursos encaja con el principio F1 de que los metadatos tengan asignados identificadores únicos y persistentes. Los enunciados RDF permiten enlazar permiten asociar datos con metadatos (F3). La utilización del protocolo HTTP en Linked Data encaja con los principios A1, RDF puede considerarse un lenguaje formal, accesible, compartido y ampliamente aplicable para la representación del conocimiento (I1), Linked Data permite la asociación entre conceptos de diferentes vocabularios (I2) así como entre diferentes datos y metadatos (I3).

Los principios FAIR **no deben considerarse como algo binario que se cumplen o no se cumplen**, sino como un espectro a lo largo del cual hay sistemas que ofrecerán un mayor grado de cumplimiento que otros [Wilkinson, 2016]. En [Wilkinson, 2018], se propone un marco para la creación de métricas FAIR en el que se define una plantilla de métricas y la [Research Data Alliance (RDA)](https://www.rd-alliance.org/about-rda) ha establecido un grupo de trabajo específico para el análisis y evaluación de métricas FAIR denominado [FAIR data maturity model Working Group](https://www.rd-alliance.org/groups/fair-data-maturity-model-wg).

Un aspecto interesante es considerar la diferencie entre datos FAIR, datos abiertos y datos enlazados. Aunque una gran cantidad de datos FAIR sean abiertos, pueden existir datos de experimentos científicos que deban estar protegidos por temas de privacidad. **Los principios FAIR no están en contradicción con el acceso controlado a ese tipo de datos**, restringido a personas o instituciones que sí puedan manipular dichos datos. 

El informe "*Turning FAIR into reality*" [Collins, 2018] tiene una serie de consejos para la adopción de FAIR en la Unión Europea, cabe destacar la inclusión de Wikidata como un ejemplo a seguir en cuanto al cumplimiento de los principios FAIR (p.42). Siguiendo esa línea, **se recomienda la utilización de un modelo similar al de Wikidata en este proyecto**.

**Todos los proyectos de la iniciativa Hércules se orientan hacia el cumplimiento de los principios FAIR**, ya que estos principios ofrecen un incentivo para publicar datos de la manera más interoperable posible. Por lo tanto, todo el trabajo realizado en este proyecto también irá en esa dirección. En el caso de las ontologías de la ROH, no sólo conforman un elemento esencial para implementar principios FAIR de cara a la publicación de datos (F2, F3, F4, A1, A2, I1, I3, R1), sino que además la publicación de las ontologías también debe seguir los principios FAIR (I2).

Como objetivo principal, se realizará un **análisis detallado de los procedimientos a seguir para publicar las ontologías de la ROH de acuerdo a los principios FAIR**, incluyendo la implementación de dichos métodos o la extensión de los métodos descritos en el Anexo V del PPT para cumplir tal fin. 

Adicionalmente, se implementará un **método de evaluación automatizado de los recursos** que se publiquen, sean éstos ontologías de la Infraestructura Ontológica o datos de la Arquitectura Semántica de Datos, para concluir el nivel FAIR de los recursos92, basado en las métricas FAIR descritas en el [proyecto FAIR Metrics](https://github.com/FAIRMetrics/Metrics) [Wilkinson, 2016; 2016b, 2018], y en las posibles métricas adicionales definidas por el equipo del proyecto y/o la UM. 

**Los resultados de la evaluación serán a su vez ser publicados cumpliendo los principios FAIR** e incluirán versión y sello de tiempo; proveyendo documentación de cómo añadir nuevas métricas y ejecutar los test automáticos para obtener las métricas, por ejemplo, siguiendo las líneas descritas en el proyecto [FAIR Metrics Evaluator](https://www.slideshare.net/markmoby/fair-metrics-presentation-to-nih-kc1), la iniciativa [GO FAIR](https://www.go-fair.org/) y su [RDM Starter Kit](https://www.go-fair.org/resources/rdm-starter-kit/), u otros proyectos afines.

### Modelo de madurez FAIR

El modelo de madurez FAIR propuesto por la RDA establece una serie de **criterios esenciales para evaluar el nivel de implementación de los principios FAIR**. En particular, se define un modelo genérico y extensible para la auto-evaluación del nivel de madurez de un conjunto de datos.

**El objetivo no es redefinir los criterios ya establecidos**, si no desarrollar el modelo sobre las iniciativas existentes, buscando elementos comunes e identificando los criterios clave para la evaluación FAIRness. De este modo se aumenta la coherencia y la interoperabilidad entre iniciativas y frameworks de validación, favoreciendo la compatibilidad y la comparación de resultados.

El grupo de trabajo se compone de participantes de diferentes disciplinas científicas, empresas, sector público y otros interesados o contribuidores proactivos en los principios FAIR, en especial con respecto a los **criterios y la metodología de evaluación** del nivel de madurez o implementación de los mismos. 

Para la unificación de criterios y como foro de discusión de indicadores se emplea un [repositorio GitHub](https://github.com/RDA-FAIR/FAIR-data-maturity-model-WG/issues), y se realizan workshops de forma periódica. El resultado principal de esta iniciativa es un [informe comparativo de diferentes herramientas de auto-evaluación](https://www.rd-alliance.org/system/files/Results%20Analysis%20of%20FAIR%20assessment%20tools%20v3.pdf), todas de tipo cuestionario manual o semi-automatizado, que en la actualidad no han sido automatizadas o que previsiblemente no puedan automatizarse al 100%.


## Referencias. 

**FIXME** Unificar formato de referencias

[Collins, 2018] Collins S., et al. (2018). Turning FAIR into a reality, Final Report and Action Plan on FAIR Data. European Commission, Directorate General  for Research and Innovation, Bruselas, 2018. 
https://ec.europa.eu/info/sites/info/files/turning_fair_into_reality_1.pdf

[Nature Genetics, 2017] Nature Genetics, (2017). Data models to GO-FAIR. Nature Genetics, 49, p. 971. 
https://doi.org/10.1038/ng.3910

[Mons, 2017] B. Mons, C. Neylon, J. Velterop, M. Dumontier, L.O.B. da Silva Santos, M.D. Wilkinson (2017). Cloudy, increasingly FAIR; revisiting the FAIR Data guiding principles for the European Open Science Cloud. Information Services & Use, 37 (1), pp. 49-56

[Rodríguez-Iglesias, 2016] Rodríguez-Iglesias A, Rodríguez-González A, Irvine AG, Sesma A, Urban M, Hammond-Kosack KE, Wilkinson MD (2016). Publishing FAIR Data: An Exemplar Methodology Utilizing PHI-Base. Front Plant Science, 7 (641).
https://doi.org/10.3389/fpls.2016.00641

[Wilkinson, 2016] M. D. Wilkinson, M. Dumontier, I. Aalbersberg, G. Appleton and E. Al (2016). The FAIR Guiding Principles for scientific data management and stewardship. Scientific Data, 3. 
https://www.nature.com/articles/sdata201618

[Wilkinson, 2016b] Wilkinson, Mark D., Verborgh, Ruben, da Silva Santos, Luiz Olavo Bonino, Clark, Tim, Swertz, Morris A., Kelpin, Fleur D. L., Gray, Alasdair J. G., Schultes, Erik A., van Mulligen, Erik M., Ciccarese, Paolo, Thompson, Mark, Kaliyaperumal, Rajaram, Bolleman, Jerven T. Dumontier, Michel (2016). Interoperability and FAIRness through a novel combination of Web technologies, Tech report, PeerJ Inc.

[Wilkinson, 2018] Wilkinson, Mark D., Sansone, Susanna-Assunta, Schultes, Erik, Doorn, Peter, Bonino da Silva Santos, Luiz O. Dumontier, Michel (2018). A design framework and exemplar metrics for FAIRness. Scientific Data, 5.
https://doi.org/10.1038/sdata.2018.118.





