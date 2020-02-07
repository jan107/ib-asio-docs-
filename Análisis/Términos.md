UM. Universidad de Murcia
CRUE. Conferencia de Rectores de las Universidades Españolas
SGI. Sistema de Gestión de Investigación
SUE. Sistema Universitario Español
RDF (Resource Description Framework). RDF es un lenguaje para representar datos en Grafos.
Para ello, RDF ofrece un modelo de datos denominado Tripleta, compuesto por un sujeto, un
predicado y un objeto (“Facultad de Informática”; “es parte de”; “Universidad de Murcia”). El
predicado (“es parte de”) y el objeto (“Universidad de Murcia”) describen una propiedad del
sujeto(“Facultad de Informática”). Uniendo varias tripletas, se obtiene un Grafo. En un Grafo
RDF, todas las entidades (sujetos, predicados, u objetos) están identificadas mediante URIs.
Las bases de datos especializadas en almacenar RDF se denominan Triple Stores. RDF es un
estándar23 del WWW Consortium24 (W3C) cuyo objetivo es ofrecer un lenguaje simple para
representar datos de manera estándar, como en su día lo hizo HTML para los documentos
Web. RDF sería, por así decirlo, “el HTML de los datos”. Es importante subrayar que RDF es
un modelo de datos abstracto que puede ser serializado en diferentes sintaxis (RDF/XML,
JSON-LD, Turtle, etc.).
SHACL (SHApes Constraint Language). SHACL es un lenguaje para validar Grafos RDF contra una
serie de condiciones, o “Shapes”. SHACL es un estándar25 del W3C.
SPARQL (SPARQL Protocol and RDF Query Language). SPARQL es un lenguaje de consulta para
extraer datos de Grafos RDF. SPARQL también es un protocolo Web estándar, de modo que
cualquier Triple Store que implemente SPARQL mediante un SPARQL endpoint ofrece los
mismos servicios. SPARQL es un estándar26 del W3C.
RDFS (RDF Schema). RDFS ofrece un mayor nivel de expresividad que RDF, ya que permite
describir propiedades generales de las entidades RDF. Por ejemplo, se pueden definir clases de
entidades (“Universidad”, “Persona”) con propiedades compartidas. RDFS es un estándar27 del
W3C. Todas las entidades en RDFS están identificadas mediante URIs.
OWL (Web Ontology Language). OWL es un lenguaje de representación de conocimiento que añade
más expresividad a RDFS, ya que se basa en Lógica Descriptiva. OWL es un lenguaje para crear
ontologías: una ontología es una descripción computacionalmente explícita de un dominio de
conocimiento, a la que se puede aplicar razonamiento automático. OWL es un estándar28 del
W3C. Todas las entidades en una ontología OWL (Clases, Individuos, Propiedades) están identificadas mediante URIs.

LOD. Linked Open Data
FAIR (Findable, Accesible, Interoperable, Reusable) 
ROH. Red de Ontologías Hércules. Crearlo es el objetivo del proyecto