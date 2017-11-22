# tryrdflib

## Summary

I maintain [MeSH RDF|https://id.nlm.nih.gov/mesh/], which is an Apache Jena based SPARQL endpoint
and also has HTML landing pages for each owl:Thing in MeSH RDF.

I also develop a bunch of python, and this is my attempt to connect rdflib and Virtuoso on both
Windows and my CentOS 7 servers so that I can perhaps discover get my back-end load process
to use rdflib, and maybe even the front-end in time.

## Objective

We wish to be able to query Virtuoso with a DESCRIBE or CONSTRUCT query to build a new graph object.
This can then be compared against another graph object loaded from an N-Triples file:

```
from rdflib import Graph
from rdflib.compare import to_isomorhpic

# ... some statements

iso1 = to_isomorphic(gfrom_ntriples)
iso2 = to_isomorhpic(gfrom_virtuoso)

if iso1.graph_digest() != iso2.graph_digest():
    # Now do some stuff, maybe update queries

```

Eventually, this will probably involve maintaining a trie that maps from the IRI of the owl:Thing to its digest


## How to build and test

There is a package required to link rdflib and Virtuoso using pyodbc.  It
requires modifications to pyodbc because SPARQL queries return IRIs and special
literals containing additional semantics (a language code).  We need to
distinguish these to be right.  There may also be blank nodes in the result; not
with MeSH RDF, but with other Semantic datasets.

So, virtuoso-python is a git sub-module.   


```
cd thirdparty/virtuoso-python
pip install -r requirements.txt
./setup.py bdist_wheel
pip install dist/*.whl
cd ../..
pip install -r requirements_extra.txt
```



