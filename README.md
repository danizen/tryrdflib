# tryrdflib

## Summary

I maintain [MeSH RDF|https://id.nlm.nih.gov/mesh/], which is an Apache Jena based SPARQL endpoint
and also has HTML landing pages for each owl:Thing in MeSH RDF.

I also develop a bunch of python, and this is my attempt to connect rdflib and Virtuoso on both
Windows and my CentOS 7 servers so that I can perhaps discover get my back-end load process
to use rdflib, and maybe even the front-end in time.

## Details

There is a support package to link rdflib and Virtuoso using pyodbc.  It
requires modifications to pyodbc because SPARQL queries return IRIs and string
literals with a language code.  We need to distinguish these to be right.

There may even be blank nodes in results - which are not strings either.

So, both of these repositories are included as sub-modules.
The way I expect this to work:


```
(cd thirdparty; mkdir wheels)
(cd thirdparty/virtuoso-python; ./setup.py bdist_wheel; cp dist/*.whl ../wheels)
(cd thirdparty/pyodbc; ./setup.py bdist_wheel; cp dist/*.whl ../wheels)
pip install -f thirdparty/wheels -r requirements.txt
```

I'll do Linux first; Windows has some challenges here.


