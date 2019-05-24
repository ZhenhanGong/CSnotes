# Wukong

## RDF
RDF graph belongs to knowledge graph
RDF triples
<Subject, Predicate, Object>
e.g. Haibo mo IPADS

## SPARQL
SPARQL is a standard query language for RDF
e.g. SELEZCT ?Y WHERE {
       ?X mo IPADS .
       ?X to ?Y .
       }

Graph Analyze vs Graph Query

## Existing Solutions
Triple Store & Triple Join
Store RDF data as a set of triples in RDBMS
Costly distributed join
Large intermediate results
intermediate results need to pass around machines


Graph Store & Graph Exploration
Store RDF data in a native graph model
Costly final join
Synchronized execution


## Wukong: A distributed in-memory RDF store

## Graph Model and Indexes


## Differiated partition

## store predicate in the key

## Query processing



Locality: where data stores, where computation goes.
Parallelism:



## fork-join vs in-place
