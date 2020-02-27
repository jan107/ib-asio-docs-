# Elección arquitectura semántica

El presente documento pretende mostrar las alternativas que existen para crear la arquitectura semántica de cara a almacenar los datos correspondientes al proyecto ASIO. Esta arquitectura debería cubrir los siguientes aspectos:

- Facilitar la generación de RDF a partir de POJOs
- Almacenamiento de la información en triple store
- Endpoint SPARQL
- Linked Data Server

Hay que tener en cuenta que uno de los requisitos que se persigue es que la arquitectura sea capaz de abstraer el triple store utilizado para que en momento dado se pueda intercambiar por otro de forma sencilla.

A groso modo, las alternativas que existirían son las siguientes:

- Implementación ad-hoc utilizando diferentes piezas que den lugar a una arquitectura completa y extensible. Para ello se puede hacer uso de diferentes frameworks
- Utilización de un Linked Data Platform, el cual por si mismo por si mismo aporta todas las piezas ya montadas y listas para su utilización

## Implementación ad-hoc

Con este modelo se pretende ir desarrollando todos los componentes que forman parte de la arquitectura de forma que permitan cumplir con los objetivos propuestos previamente a la par que aportar flexibilidad al Backend SGI para permitir ampliarlo a medida que vaya avanzando el proyecto.

En este sentido, se recomienda la utilización de un framework que ayude a generar la solución final, siendo los más usados:

- Eclipse RDF4J: [https://RDF4J.org/](https://RDF4J.org/)
- Apache Jena: [https://jena.apache.org/](https://jena.apache.org/)

Para la elección de los frameworks se ha tenido en cuenta los siguientes factores claves:

- Disponibilidad de documentación
- Ampliamente acogido por la comunidad
- Posibilidad de integración con diferentes triple stores
- Posibilidad de generar un modelo RDF a partir de POJOs
- Posibilidad de generar RDF en diferentes formatos (turtle, xml-ld, json-ld, ...)

### Apache Jena

Apache Jena es un framework Java Open source para el desarrollo y construcción de aplicaciones Linked Data y web semántica. 

La arquitectura de Apache Jena se basa en diferentes elementos que todos juntos permiten procesar e interactuar con datos RDF.

![Arquitectura Apache Jena](https://jena.apache.org/images/jena-architecture.png)

Las características más destacables de Jena son las siguienes

- RDF API: Es el core de Jena, permitiendo la generación de modelos RDF 
- Ejecución de consultas SPARQL 
- TDB como triple store por defecto, pero con posibilidad de crear adaptadores para otros almacenamientos
- Exportación / importación de datos en RDF/XML, turtle, n-triples y RDFa
- Inferencia, mediante motor de reglas y otros algoritmos

#### Importación de datos

Para la importación de datos se deberán transformar los datos desde un POJO a formato RDF. Jenra en el API RDF provee de mecanismos para facilitar esta transformación. Para ello se debe crear un modelo al que posteriormente se le van añadiendo propiedades. Por ejemplo:

```java
// create an empty model
Model model = ModelFactory.createDefaultModel();

// create the resource
Resource johnSmith = model.createResource("http://example.org/JohnSmith");

// add the property
johnSmith.addProperty(VCARD.FN, "John Smith");
```

En este caso se crea un modelo para un nuevo elemento de tipo "http://example.org/JohnSmith", al cual se le añade como propiedad el nombre "John Smith".

También sería posible cargar los datos desde un fichero o un input stream en formato RDF:

```java
String inputFileName  = "vc-db-1.rdf";

// create an empty model
Model model = ModelFactory.createDefaultModel();

InputStream in = FileManager.get().open( inputFileName );
if (in == null) {
    throw new IllegalArgumentException( "File: " + inputFileName + " not found");
}

// read the RDF/XML file
model.read(in, "");
```

Sería posible exportar los datos al formato adecuado mediante el siguente código:

```java
// write it to standard out
model.write(System.out, "TURTLE");
```

#### Triple stores

Jena utiliza como triple store por defecto TDB. Para ello disponede los conectores oportunos para facilitar la utlización de este sistema. Por ejemplo

```java
String directory = "MyDatabases/DB1";
Dataset dataset = TDBFactory.createDataset(directory);
```

Un ejemplo de almacenamiento de información vía SPARQL:

```java
public static void main(String...argv) {
    String directory = "MyDatabases/DB1";
    Dataset dataset = TDBFactory.createDataset(directory);

    // Start WRITE transaction.
    // It's possible to read from the dataset inside the write transaction.

    // An application can have other Datasets, in the same JVM,
    // tied to the same TDB database performing read
    // transactions concurrently. If another write transaction
    // starts, the call of dataset.begin(WRITE) blocks until
    // existing writer finishes.
    
    // A WRITE transaction is
    // dataset.begin(ReadWrite.READ);
    // try {
    // ...
    // ... dataset.abort() or dataset.commit()
    // } finally { dataset.end();}
    //

    Txn.executeWrite(dataset, ()->{
        // Do a SPARQL Update.
        String sparqlUpdateString = StrUtils.strjoinNL
            ("PREFIX . <http://example/>"
            ,"INSERT { :s :p ?now } WHERE { BIND(now() AS ?now) }"
            );

        execUpdate(sparqlUpdateString, dataset);
    });
}

public static void execUpdate(String sparqlUpdateString, Dataset dataset) {
    UpdateRequest request = UpdateFactory.create(sparqlUpdateString);
    UpdateProcessor proc = UpdateExecutionFactory.create(request, dataset);
    proc.execute();
}
```

También sería posible utilizar otros Triple Store vía endpoint SPARQL gracias a `RDFConnection`. Por ejemplo:

```java
RDFConnectionRemoteBuilder builder = RDFConnectionRemote.create()
        .httpClient(httpClient)
        .destination(endpoint)
        // Query only.
        .queryEndpoint("sparql")
        .updateEndpoint("sparql");

Query query = QueryFactory.create("SELECT * { ?s ?p ?o } LIMIT 100");

// Whether the connection can be reused depends on the details of the implementation.
// See example 5.
try (RDFConnection conn = builder.build()) {
    conn.queryResultSet(query, ResultSetFormatter::out);
}
```

En el caso de BlazeGraph:

```java
String APIUrl = "http://192.168.222.1:9999/bigdata/sparql";
RDFConnection conn = RDFConnectionFactory.connect(APIUrl,APIUrl,APIUrl);
```

También existen providers para los TripleStores más utilizados como Virtuoso [http://vos.openlinksw.com/owiki/wiki/VOS/VirtJenaProvider](http://vos.openlinksw.com/owiki/wiki/VOS/VirtJenaProvider)

### Eclipse RDF4J

Eclipse RDF4J es un framework open source para el almacenamiento, consulta y análisis de datos RDF.

![Arquitectura RDF4J](https://rdf4j.org/images/rdf4j-architecture.svg)

En cuanto a arquitectura, al igual que Jena, se basa en una arquitectura modular que hace que se puedan ir tomando aquellas partes (APIs) que sean precisa para la aplicación.

Una de las ventajas que aporta RDF4J, es la gran documentación con la que cuenta así como una gran comunidad y proyectos desarrollados con la misma.

Las características principales son

- Rio (RDF I/O): Parser/writer API
- Model API: permite la generación de modelos a partir de los datos
- Ejecución de consultas SPARQL 
- Sesame como triple store por defecto, pero con posibilidad de crear adaptadores para otros almacenamientos
- Exportación / importación de datos RDF en numerosos formatos
- Inferencia y validación, mediante motor de reglas y otros algoritmos
- Extensiones: Full-Text Search, GeoSPARQL, FedX: Queries federadas

#### Importación de datos

La importación de datos comparte varios conceptos con Jena, ya que se basa en la confección de un modelo. Para ello se utiliza el API RIO (RDF Input/Output), la cual contiene parseadores para y writers para numerosos formatos de salida:

- RDF/XML
- Turtle
- N-Triples
- TriG
- TriX
- JSON-LD
- RDF/JSON
- N-Quads
- Binary

En cuanto a la confección de un modelo, como ejemplo podemos modelar lo siguiente: 

![Modelado de ejemplo](./images/rdf-graph-2.png)

Donde se dice que "Picasso" es de tipo "Artist" y que además tiene como nombre "Pablo" (siguiendo el vocabulario FOAF).

Llevado a RDF4J, tendría el siguiente aspecto:

```java
// We use a ValueFactory to create the building blocks of our RDF statements:
// IRIs, blank nodes and literals.
ValueFactory vf = SimpleValueFactory.getInstance();

// We want to reuse this namespace when creating several building blocks.
String ex = "http://example.org/";

// Create IRIs for the resources we want to add.
IRI picasso = vf.createIRI(ex, "Picasso");
IRI artist = vf.createIRI(ex, "Artist");

// Create a new, empty Model object.
Model model = new TreeModel();

// add our first statement: Picasso is an Artist
model.add(picasso, RDF.TYPE, artist);

// second statement: Picasso's first name is "Pablo".
model.add(picasso, FOAF.FIRST_NAME, vf.createLiteral("Pablo"));
```

Sería posible leer datos de un fichero en formato RDF (en cualquiera de los admitidos por RDF4J), por ejemplo en TURTLE:

```java
String filename = "example-data-artists.ttl";

// read the file 'example-data-artists.ttl' as an InputStream.
InputStream input = Example08ReadTurtle.class.getResourceAsStream("/" + filename);

// Rio also accepts a java.io.Reader as input for the parser.
Model model = Rio.parse(input, "", RDFFormat.TURTLE);
```

Así como exportar los datos en RDF:

```java
// Instead of simply printing the statements to the screen, we use a Rio writer to
// write the model in Turtle syntax:
Rio.write(model, System.out, RDFFormat.TURTLE);
```

#### Triple stores

RDF4J provee un conjunto de APIs que se abstraen del vendedor para el almacenamiento, razonamiento y recuperación de RDF y OWL. Las principales soluciones que implementan las APIs RDF4J son:

* **Core databases**: Este tipo de bases de datos están orientadas a dataset de tamaños medio y mediano, recomendándose otro tipo de bases de datos para proyectos más grandes. Incluye bases de datos desarrolladas por RDF4J como son 
  * **Memory Store**: base de datos RDF transaccional en memoria con persistencia a disco opcional. 
  * **Native Store**: base de datos RDF transaccional usando persistencia en disco. Se trata de una solución más escalable que la opción en memoria. Orientada para datasets de 100 millones de triples.
  * **Elasticsearch Store**: se trata de una base de datos RDF experimental que utiliza Elasticsearch como almacenamiento
* **Ontotext GraphDB**: se trata de uno de los triplestores lider del mercado construido sobre los estándares de OWL. Es capaz de manejar grandes cargas y consultas pesadas así como inferencia en tiempo real. Desde la versión 8 es completamente compatible con RDF4J.
* **Halyard**: triplestore implementado sobre Apache HBase
* **Stardog**: almacenamiento rápido, ligero y Java puro para RDF
* **Amazon Neptune**: Triple store gestionado en la nube de Amazon AWS
* **Systap Blazegraph**
* **MarkLogic RDF4J API**
* Strabon
* **Openlink Virtuoso RDF4J Provider**: proveedor para permitir a RDF4J modificar, consultar y razonar con Virtuoso

Ejemplo de persistencia de RDF en triplestore:

```java
// First load our RDF file as a Model.
String filename = "example-data-artists.ttl";
InputStream input = Example13AddRDFToDatabase.class.getResourceAsStream("/" + filename);
Model model = Rio.parse(input, "", RDFFormat.TURTLE);

// Create a new Repository. Here, we choose a database implementation
// that simply stores everything in main memory. Obviously, for most real-life applications, you will
// want a different database implementation, that can handle large amounts of data without running
// out of memory and keeps data safely on disk.
// See http://docs.rdf4j.org/programming/#_the_repository_api for more extensive examples on
// how to create and maintain different types of databases.
Repository db = new SailRepository(new MemoryStore());
db.initialize();

// Open a connection to the database
try (RepositoryConnection conn = db.getConnection()) {
  // add the model
  conn.add(model);

  // let's check that our data is actually in the database
  try (RepositoryResult<Statement> result = conn.getStatements(null, null, null);) {
    while (result.hasNext()) {
      Statement st = result.next();
      LOG.info("db contains: {}", st);
    }
  }
} finally {
  // before our program exits, make sure the database is properly shut down.
  db.shutDown();
}
```

Por ejemplo una consulta SPARQL contra un repositorio en memoria:

```java
// Create a new Repository.
Repository db = new SailRepository(new MemoryStore());
db.initialize();

// Open a connection to the database
try (RepositoryConnection conn = db.getConnection()) {
  String filename = "example-data-artists.ttl";
  try (InputStream input =
      Example15SimpleSPARQLQuery.class.getResourceAsStream("/" + filename)) {
    // add the RDF data from the inputstream directly to our database
    conn.add(input, "", RDFFormat.TURTLE );
  }

  // We do a simple SPARQL SELECT-query that retrieves all resources of type `ex:Artist`,
  // and their first names.
  String queryString = "PREFIX ex: <http://example.org/> \n";
  queryString += "PREFIX foaf: <" + FOAF.NAMESPACE + "> \n";
  queryString += "SELECT ?s ?n \n";
  queryString += "WHERE { \n";
  queryString += "    ?s a ex:Artist; \n";
  queryString += "       foaf:firstName ?n .";
  queryString += "}";

  TupleQuery query = conn.prepareTupleQuery(queryString);

  // A QueryResult is also an AutoCloseable resource, so make sure it gets closed when done.
  try (TupleQueryResult result = query.evaluate()) {
    // we just iterate over all solutions in the result...
    while (result.hasNext()) {
      BindingSet solution = result.next();
      // ... and print out the value of the variable binding for ?s and ?n
      LOG.info("?s = {}", solution.getValue("s"));
      LOG.info("?n = {}", solution.getValue("n"));
    }
  }
} finally {
  // Before our program exits, make sure the database is properly shut down.
  db.shutDown();
}
```

### Comparativa Jena vs RDF4J

Una vez visto tanto Jena como RDF4J, es hora de realizar una comparativa entre ambos. En ambos casos se trata de productos con características similares pero con ligeras diferencias:

|                     | Jena | RDF4J |
| ------------------- | :--: | :---: |
| Disponibilidad de documentación | :heavy_check_mark: | :heavy_check_mark: |
| Ampliamente acogido por la comunidad | :heavy_check_mark: | :heavy_check_mark: |
| Posibilidad de generar un modelo RDF a partir de POJOs | :heavy_check_mark: | :heavy_check_mark: |
| Posibilidad de generar RDF en diferentes formatos (turtle, xml-ld, json-ld, ...) | :heavy_check_mark: | :heavy_check_mark: |
| Soporte a la generación de RDF en más formatos | :x: | :heavy_check_mark: |
| Posibilidad de integración con diferentes triple stores | :heavy_check_mark: | :heavy_check_mark: |
| Conexión mediante endpoint SPARQL | :heavy_check_mark: | :heavy_check_mark: |
| Conectores ya desarrollados para los principales triple stores | :x: | :heavy_check_mark: |
| API Linked Data | :x: | :x: |
| Endpoint SPARQL | :x: | :x: |

Viendo los resultados anteriores, aunque ambos podrían utilizarse para el mismo cometido, parece que RDF4J aporta más valor al soportar más formatos RDF y al tener mayor compatibilidad con diferentes triplestores.

## Linked data platform (LDP)

Una plataforma Linked Data es aquella que abarca desde el almacenamiento de los datos en triple store (u otro sistema) a la exposición de APIs siguiendo los estándares LDP y endpont SPARQL. En este caso se ha valorado la utilización de [Trellis](https://github.com/trellis-ldp/trellis/wiki)

### Trellis

#### General

Es un servidor LDP Modular que soporta el escalado horizontal y redundancia.

Soporta bases de datos relacionales y triples stores.

##### Uso

Puede instalarse en maquinas Linux , dockenizarse o extenderse con Maven

```xml
<dependency>
    <groupId>org.trellisldp</groupId>
    <artifactId>trellis-api</artifactId>
    <version>0.8.3</version>
</dependency>
```

 ##### Objetivo

Ofrecer API Rest según especificaciones de de LDP para interactuar con los datos (métodos de creación, modificación, borrado).

Puede recuperarse un dato histórico (versionado y auditoria de cambios) en cualquier instante de tiempo siguiendo las especificaciones de  [Memento specification](https://tools.ietf.org/html/rfc7089 "Title"). ([ejemplos](https://github.com/trellis-ldp/trellis/wiki/Resource-Versioning "Title"))

Proporciona un mecanismo de detección de corrupción de recursos.

Proporciona integración con Kafka, de modo que es fácilmente integrable en un sistema distribuido

**Autentificación y Autorización **

Permite controlar la [autentificación](https://github.com/trellis-ldp/trellis/wiki/Authentication) por JWT o acceder públicamente, controlado ambos accesos por configuración en tiempo de ejecución

Después de la autentificación se asigna un WebID. El modulo de WebAC regula la [autorización](https://github.com/trellis-ldp/trellis/wiki/Authorization) para acceso a el recurso para cada WebID, por medio de el uso de RDFs para definir e acceso.

```
@prefix acl: <http://www.w3.org/ns/auth/acl#>.

<#authorization> a acl:Authorization ;
    acl:mode acl:Read, acl:Write ;
    acl:accessTo <https://example.org/repository/resource> ;
    acl:agent <https://example.org/users/1>, <https://example.org/users/2> .
```

##### Integraciones

Se integra con una base de datos relacional o un triple store. También publica notificaciones al añadir, modificar o eliminar un recurso conforme a [Activity Stream 2.0 specification](https://www.w3.org/TR/activitystreams-core/)

#### Guía de configuración

La aplicación Web Dropwizard.io permite manejar un amplio conjunto de opciones de configuración que pueden definirse también por un fichero en la ruta `/opt/trellis/etc/config.yml`.

#### Arquitectura

![arquitectura](https://github.com/trellis-ldp/trellis-deployment/raw/master/docs/TrellisLDPDiagram.png)

Los métodos get y replace son idempotentes y aplicables a un único recurso. Los métodos no idempotentes POST y PATCH, se descomponen en get y replace, que son idempotentes.

La arquitectura de Trellis, permite tratar el recurso como una clave opaca, independiente de su jerarquía, de forma que se permita el  escalado horizontal.

##### Consistencia

Dado que es un sistema distribuido, que potencialmente accede a distintas fuentes, ofrece consistencia eventual.

##### Recursión

No hay soporte para la recursión, por lo tanto los PUT y DELETE recursivos no son posibles. Por ejemplo para crear /foo/bar/baz, es necesario crear todos los contenedores.

Del mismo modo al borrar un raiz (foo), no borramos la jerarquía, por lo que debemos borrarlo explícitamente.

 ##### Asincronía

Todas las operaciones se realizan de forma asíncrona, lo que implica que pueden no ser visibles por los clientes inmediatamente

#### Prueba de Concepto

Se realizan dos pruebas de concepto:

##### Trellis sobre BBDD Relacional (postgresql)

- Arquitectura:

  - Servidor postgres:9.4
  - trellisldp/trellis-ext-db:latest

- docker-compose:

  ```yml
  version: "3"
  services:
    trellis:
      image: trellisldp/trellis-ext-db:latest
      environment:
        TRELLIS_DB_USERNAME: hercules
        TRELLIS_DB_PASSWORD: h3rcul3s
        TRELLIS_DB_URL: jdbc:postgresql://db/hercules-db
      ports:
        - 80:8080
      depends_on:
        - db
      volumes:
        - /local/trellis/data:/opt/trellis/data
        - /local/trellis/log:/opt/trellis/log
        # Please see note below about the ./etc directory
        # - /local/trellis/etc:/opt/trellis/etc
    db:
      image: postgres:9.4
      environment:
        POSTGRES_DB: hercules-db
        POSTGRES_PASSWORD: h3rcul3s
        POSTGRES_USER: hercules
        PGDATA: /var/lib/postgresql/data
      ports:
        - 5432:5432
      volumes:
        - postgres:/var/lib/postgresql/data
  volumes:
    postgres: 
  ```

##### Trellis sobre Triple Store (BlazeGraph)

- Arquitectura:

  - nawer/blazegraph:2.1.5
  - trellisldp/trellis:latest

- docker-compose:

  ```yml
  version: "3.1"
  services:
    trellis:
      image: trellisldp/trellis:latest
      environment:
        JAVA_OPTS: "-Xms250m -Xmx1024m"
      ports:
        - 8080:8080
      depends_on:
        - db
      volumes:
        #  file-based resources (e.g. binaries and mementos), application logs and configuration files
        - ./trellis/data:/opt/trellis/data
        - ./trellis/log:/opt/trellis/log
        # Please see note below about the ./etc directory
        - ./trellis/config:/opt/trellis/etc
    db:
      # Blazegraph Triplestore
      # Endpoint at http://db:9999/blazegraph/namespace/kb/sparql
      # Docs at https://github.com/nawerprod/blazegraph
      image: nawer/blazegraph:2.1.5
      environment:
        JAVA_XMS: 512m
        JAVA_XMX: 1g
      volumes:
        - ./blazegraph/data:/var/lib/blazegraph
      ports:
        - "9999:9999"
  ```

- fichero de configuración trellis **config.yml** en ruta **./trellis/config**

  ```yml
  binaries: /opt/trellis/data/binaries
  
  mementos: /opt/trellis/data/mementos
  
  namespaces: /opt/trellis/data/namespaces.json
  
  # This may refer to a static base URL for resources. If left empty, the
  # base URL will reflect the Host header in the request.
  baseUrl:
  
  # This configuration will enable a WebSub "hub" header.
  hubUrl:
  
  auth:
      adminUsers: []
      webac:
          enabled: true
      jwt:
          enabled: false
          key: changeme
      basic:
          enabled: true
          usersFile: /opt/trellis/etc/users.auth
  
  cors:
      enabled: true
      allowOrigin:
          - "*"
      maxAge: 180
  
  cache:
      maxAge: 86400
      mustRevalidate: true
  
  notifications:
      enabled: false
      type: JMS
      topicName: "trellis"
      connectionString: "tcp://localhost:61616"
  
  # JSON-LD configuration
  jsonld:
      cacheSize: 10
      cacheExpireHours: 24
      contextWhitelist: []
      contextDomainWhitelist: []
  ```

##### Prueba de concepto

###### BlazeGraph

Es el triple store seleccionado para la realizar la PoC. Merece especial atención por las siguientes características:

- Expone un endpoint Sparql (http://localhost:9999/blazegraph/#query), en apariencia, bastante completo

  ![image-20200226104816659](https://i.ibb.co/WH1KMYP/blazegraph-endpoint.png)

  - Ejemplo de query de obtención de datos 

    ```sql
    SELECT ?subject ?predicate ?object
    WHERE {<http://www.hercules.fake/data/Researcher/1> ?predicate ?object} 
    LIMIT 100
    ```

  - Ejemplo de query de inserción en formato RDF/XML

    ```xml
    <?xml version="1.0"?>
    <rdf:RDF
    xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#" 
    xmlns:cd="http://www.hercules.fake/data/Researcher#"> 
    <rdf:Description
     rdf:about="http://www.hercules.fake/data/Researcher/1">
      <cd:name>Daniel Ruiz Santamaría</cd:name>
      <cd:country>Spain</cd:country>
      <cd:company>Izertis</cd:company>
      <cd:rol>Software Architech</cd:rol>
      <cd:year>2019</cd:year>
    </rdf:Description>
    <rdf:Description
     rdf:about="http://www.hercules.fake/data/Researcher/2">
      <cd:name>Rubén Gavilán Fernandez</cd:name>
      <cd:country>Spain</cd:country>
      <cd:company>Izertis</cd:company>
      <cd:rol>Software Architech</cd:rol>
      <cd:year>2019</cd:year>
    </rdf:Description>
    </rdf:RDF>  
    ```
  
- Despliega un [NanoSparqlServer](https://github.com/blazegraph/database/wiki/NanoSparqlServer), (http://localhost:9999/bigdata/sparql) para actuar como API Rest LDP. ¿Puede realizar una función similar a Trellis?
- Alto rendimiento, soporta 50 Billones de nodos en una sola nodo
- Usado en producción en clientes Fortune 500 como Autodesk, EMC y otros

###### Trellis

Se realizan pruebas mínimas como la creación de contenedores y recursos. La documentación de Trellis parece no estar actualizada (no funciona), y por lo tanto, se realizan las pruebas, siguiendo las especificaciones de la [LDP](https://www.w3.org/TR/ldp-primer/). No todas las operaciones funcionan correctamente, por ejemplo, es necesario sustituir las operaciones POST, indicadas en la LDP, por operaciones PUT

- Creación de del contenedor researcher (PUT)

```
PUT /researcher/ HTTP/1.1
Host: localhost:8080/researcher
Content-Type: text/turtle
Link: <http://www.w3.org/ns/ldp/BasicContainer>; rel="type"

@prefix ldp: <http://www.w3.org/ns/ldp#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
 
<> a ldp:Container, ldp:BasicContainer;
   dcterms:title "Researcher" ; 
   dcterms:description "This container will contain Researchers" . 
```

* Visualización del nuevo contenedor, sobre ruta raíz 

  * Petición

    ```
    GET / HTTP/1.1
    Host: localhost:8080
    Host: localhost:8080/researcher
    ```

  * Respuesta

    ```
    @prefix ldp:  <http://www.w3.org/ns/ldp#> .
    @prefix dcterms:  <http://purl.org/dc/terms/> .
    @prefix foaf:  <http://xmlns.com/foaf/0.1/> .
    
    <http://localhost:8080/>
            <http://www.w3.org/1999/02/22-rdf-syntax-ns#type>  ldp:BasicContainer ;
            ldp:contains  <http://localhost:8080/researcher> .
    ```

- Visualización del nuevo contenedor, sobre ruta **/researcher**, donde podemos ver los atributos del contenedor
  - Petición

    ```
    GET /researcher HTTP/1.1
    Host: localhost:8080
    Host: localhost:8080/researcher
    Content-Type: text/turtle
    Link: <http://www.w3.org/ns/ldp/BasicContainer>; rel="type"
    ```

  - Respuesta

    ```
    @prefix ldp:  <http://www.w3.org/ns/ldp#> .
    @prefix dcterms:  <http://purl.org/dc/terms/> .
    @prefix foaf:  <http://xmlns.com/foaf/0.1/> .
    
    <http://localhost:8080/researcher>
            dcterms:description  "This container will contain Researchers" ;
            dcterms:title        "Researcher" ;
            <http://www.w3.org/1999/02/22-rdf-syntax-ns#type>  ldp:RDFSource .
    ```

- Crear un nuevo recurso dentro del contenedor
  - Petición

    ```
    PUT /researcher? HTTP/1.1
    Host: localhost:8080
    Host: localhost:8080/researcher
    Link: <http://www.w3.org/ns/ldp#Resource>; rel = "type" 
    Slug: r2
    Content-Type: text/turtle
    
    @prefix dc: <http://purl.org/dc/terms/> .
    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    
    <> a foaf:account;
        foaf:primaryTopic <#r2> ;
        dc:title 'Data of researcher 2' .
    
    <#r2> a foaf:Person;
        foaf:name 'Researcher 2'  ;
        foaf:title 'Doctor 2'  ;
        foaf:age 40  .
    ```

- Visualización del nuevo recurso, sobre ruta **/researcher/#2**, donde podemos ver los atributos del recurso

  - Petición

    ```
    GET /researcher HTTP/1.1
    Host: localhost:8080
    Host: localhost:8080/researcher
    Content-Type: text/turtle
    Link: <http://www.w3.org/ns/ldp/BasicContainer>; rel="type"
    Slug: r2
    ```

  - Respuesta

    ```
    @prefix ldp:  <http://www.w3.org/ns/ldp#> .
    @prefix dcterms:  <http://purl.org/dc/terms/> .
    @prefix foaf:  <http://xmlns.com/foaf/0.1/> .
    
    <http://localhost:8080/researcher>
            <http://www.w3.org/1999/02/22-rdf-syntax-ns#type>  foaf:account ;
            foaf:primaryTopic  <http://localhost:8080/researcher#r2> ;
            dcterms:title      "Data of researcher 2" .
    
    <http://localhost:8080/researcher#r2>
            <http://www.w3.org/1999/02/22-rdf-syntax-ns#type>  foaf:Person ;
            foaf:age    40 ;
            foaf:name   "Researcher 2" ;
            foaf:title  "Doctor 2" .
    
    <http://localhost:8080/researcher>
            <http://www.w3.org/1999/02/22-rdf-syntax-ns#type>  ldp:RDFSource .
    ```



##### Comentarios sobre la prueba de concepto

###### Ventajas

Trellis conceptualmente, tiene un enfoque muy atractivo por los siguientes motivos:

- Por un lado, facilita la integración de múltiples bases de datos ya sean relacionales ya sean triples stores
- Por otro lado facilita una capa de autentificación con JWT y de autorización con el módulo WebAC
- Además es fácilmente integrable con sistemas distribuidos o microservicios debido a su integración  con kafka, publicando en los topics establecidos el resultado de cualquier interacción con su API.
- Su API sigue el standard  expuesto por la [LDP](https://www.w3.org/TR/ldp-primer/)
- Recuperable cualquier versión de un contenedor o recurso por medio del uso de memento

###### Desventajas

Se trata de una herramienta con muchas posibilidades pero poco madura:

- Apenas existe documentación al respecto, y la que hay no esta actualizada. Sobre la última versión de Trellis (0.10.0), las operaciones sobre el API descritas en la documentación no funcionan (funcionan en su mayor parte las descritas por la [LDP](https://www.w3.org/TR/ldp-primer/)) .
- La propia versión del proyecto (0.10.0), habla de su estado de inmadurez.
- No se encuentran ejemplos de uso, por lo que se infiere que la permeabilidad en proyectos reales es muy baja.
- Dada la escasez de documentación, el número de horas destinadas a inferir su correcto uso serán elevadas, y la probabilidad de cometer errores alta.
- Es precisa la generación previa de RDF a partir de los POJOs, teniendo que utilizar para ello algún framework

#### Conclusión

Debido a su estado de inmadurez, y que probablemente obtener un conocimiento apropiado sobre el uso de la herramienta (dada la escasa documentación), requiera un alto coste en horas de trabajo, con una gran incertidumbre sobre el resultado final  y que aparentemente las ventajas que aporta, podrían resolverse con otras herramientas o desarrollos a medida, se recomienda por el momento no usar esta herramienta. Probablemente Apache Jena pueda ser una mejor alternativa dado que su estado de madurez es superior, y su arquitectura modular, probablemente permita usar aquellos módulos que sirvan a nuestros propósitos y desechar el resto. 

Otra conclusión que se puede obtener en la presente prueba de concepto, es que el triple store Blazegraph, parece cumplir con ciertas garantías con algunos de los requisitos demandados por el cliente, tal como el endpoint SPARQL, aunque probablemente  sea necesario introducir un proxy, para manejar los temas relativos a la seguridad.

  ## Conclusión

Tras analizar tanto una solución ad-hoc y una solución tipo LDP, se observa que esta última a pesar de ofrecer varias ventajas en un primer lugar ya que aportaría bastante componentes ya de fábrica, como por ejemplo cumplimiento de estándares LDP, no se trata de una alternativa lo suficientemente flexible de acuerdo a los requisitos de la aplicación, ya que uno de ellos exige que la aplicación sea transparente a un eventual cambio de triple store y con este tipo de plataformas es muy complicado conseguirlo.

Se recomienda la utilización de una solución ad-hoc apoyada en un framework RDF, supliendo aquellos que no provea con desarrollo custom, como es el caso de las APIs Linked Data y endpoint SPARQL.