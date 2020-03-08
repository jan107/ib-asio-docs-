![](./images/logos_feder.png)

# Alineación con FAIR

Los principios FAIR (Findable, Accessible, Interoperable, Reusable) fueron propuestos en el ámbito científico para mejorar la calidad de los datos científicos, promoviendo que dichos datos fuesen fácilmente encontrables, accesibles, interoperables y reutilizables.

**FINDABLE** (Encontrables): Los datos y metadatos pueden ser encontrados por la comunidad después de su publicación, mediante herramientas de búsqueda.

- [ ] F1. Asignarles un identificador único y persistente a los datos y los metadatos
- [ ] F2. Describir los datos con metadatos de manera prolija
- [ ] F3. Registrar/Indexar los datos y los metadatos en un recurso de búsqueda
- [ ] F4. En los metadatos se debe especificar el identificador de los datos que se describen.

**ACCESSIBLE** (Accesibles): Los datos y metadatos están accesibles y por ello pueden ser descargados por otros investigadores utilizando sus identificadores.

- [ ] A1 Los datos y los metadatos pueden ser recuperados por sus identificadores mediante protocolos estandarizados de comunicación
- [ ] A1.1 Los protocolos tienen que ser abiertos, gratuitos e implementados universalmente
- [ ] A1.2 El protocolo debe de permitir procedimientos para la autentificación y la autorización (por si fuera necesario).
- [ ] A2 Los metadatos deben de estar accesibles, incluso cuando los datos ya no estuvieran disponibles.

**INTEROPERABLE** (Interoperables): Tanto los datos como los metadatos deben de estar descritos siguiendo las reglas de la comunidad, utilizando estándares abiertos, para permitir su intercambio y su reutilización.

- [ ] I1. Los datos y los metadatos deben de usar un lenguaje formal, accesible, compartible y ampliamente aplicable para representar el conocimiento
- [ ] I2. Los datos y los metadatos usan vocabularios que sigan los principios FAIR
- [ ] I3. Los datos y los metadatos incluyen referencias cualificadas a otros datos o metadatos

**REUSABLE** (Reutilizables): Los datos y los metadatos pueden ser reutilizados por otros investigadores, al quedar clara su procedencia y las condiciones de reutilización.

- [ ] R1. Los datos y los metadatos contienen una multitud de atributos precisos y relevantes
- [ ] R1.1. Los datos y los metadatos se publican con una licencia clara y accesible sobre su uso y reutilización
- [ ] R1.2. Los datos y los metadatos se asocian con información sobre su procedencia
- [ ] R1.3. Los datos y los metadatos siguen los estándares relevantes que usa la comunidad del dominio concreto

En general, el uso de datos enlazados favorece el cumplimiento de los principios FAIR. Por ejemplo, el uso de URIs para identificar recursos encaja con el principio F1 de que los metadatos tengan asignados identificadores únicos y persistentes. Los enunciados RDF permiten enlazar permiten asociar datos con metadatos (principio F3). La utilización del protocolo http en linked data encaja con los principios A1, RDF puede considerarse un lenguaje formal, accesible, compartido y ampliamente aplicable para la representación del conocimiento (principio I1), linked data permite la asociación entre conceptos de diferentes vocabularios (principio I2) así como entre diferentes datos y metadatos (principio I3). 