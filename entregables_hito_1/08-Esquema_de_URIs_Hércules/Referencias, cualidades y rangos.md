# Referencias, cualidades y rangos

Wikidata permite la utilización homogénea de un sistema de reificación que permite cualificar las declaraciones. En dicho modelo, todo enunciado puede tener asociadas una serie de declaraciones que permiten cualificar lo que se está afirmando. A modo de ejemplo, la declaración de que Murcia (wd:Q12225) tiene una población (propiedad P1082) de 447182 habitantes puede realizarse de forma directa como:

wd:Q12225 wdt:P1082 447182 . 

La declaración anterior se puede tomar como declaración por defecto, sin embargo, si se desea mantener una base de conocimiento fiable que evolucione con el tiempo es necesario añadir **cualificadores** a dicha afirmación. Por ejemplo, se puede indicar que la fuente o referencia a partir de la cual se ha obtenido el valor es el Registro Municipal de España (wd:Q17597568) y que el valor se refiere al año 2018. Esa información se representa como:

`wd:Q12225 p:P1082 [` 

 `wikibase:rank    wikibase:PreferredRank ;`

 `ps:P1082       "447182"^^xsd:**decimal** ;`

 `prov:wasDerivedFrom wd:Q17597568 ;`

 `pq:P585       "2018-01-01"^^xsd:**date**`

`] .` 

El modelo de reificación de Wikidata está predefinido en el sistema de forma homogénea y permite realizar consultas enriquecidas y mantener un grafo de conocimiento que evoluciona a lo largo del tiempo. 

La ventaja de dicho sistema es la adaptabilidad a la propia evolución de los datos, al permitir disponer de datos históricos de investigación.