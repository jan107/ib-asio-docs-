# Esquema de URIs

Siguiendo las recomendaciones citadas en  [Buenas prácticas para URIs Hércules.md](../09-Buenas_prácticas_para_URIs_Hércules.md)  el esquema de URIs que se plantea es el siguiente:

**http://{dominio}/{tipo}/{concepto}/{referencia}**

Donde:

\-   *{dominio}* es una combinación del host y del sector relevante. El sector puede ser un subdominio o el primer componente del path

\-   *{tipo}* debería ser un valor entre un conjunto pequeño de valore que declaren el tipo de recurso que se está identificando. Ejemplos típicos pueden ser:

​				o  'id' ó 'item' para valores del mundo real

​				o  'doc' para documentos

​				o  'def' para definiciones de conceptos

​				o  'set' para conjuntos de datos

\-   *{concepto}* podría ser una colección, el tipo de objeto del mundo real identificado, el nombre del esquema de conceptos, etc.

\-   *{referencia}* es un ítem, concepto o término específico