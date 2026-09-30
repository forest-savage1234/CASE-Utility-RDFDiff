# Cyber-investigation Analysis Standard Expression (CASE)

_Read the [CASE Wiki tab](https://github.com/casework/CASE/wiki) to learn **everything** you need to know about the Cyber-investigation Analysis Standard Expression (CASE) ontology._
_For learning about the Unified Cyber Ontology, CASE's parent, see [UCO](https://github.com/ucoProject/UCO)._

# RDFDiff
An RDF and ontology trouble shooter for CASE and UCO.

### Validation scope

The `-g` glossary selects the vocabulary for term-membership checks. These checks
do not run SHACL constraints or establish CASE/UCO conformance. Select a glossary
for the ontology version used by your application.

### What it does
RDFDiff reads an input RDF graph and a glossary using RDFlib. With `--verify`,
it reports whether the collected input predicates occur in the glossary.
The `--debug` option enters the debugger when a predicate is not found.


### How it works
The implementation builds subject, predicate and object lists for each graph.
`verify_object_existance` compares the collected input predicates against all
three glossary lists.
It does not check the input subjects or objects for membership, nor evaluate
class membership, property ranges or other ontology constraints.


### Why not SPARQL?
In order to facilitate a broad range of ontologies and custom tool outputs,
SPARQL queries are not used for verification. CASE and UCO allow for robust
flexibility and this tool  aims to compliment this approach.


### Installation
```
sudo pip install -r requirements.txt 
```

### Unit Tests
The ontology validator
is heavily reliant on 3rd pary libraries, primarily RDFlib.
RDFLib is under heavy development. To ensure compatability with new releases
unit tests have been written to check for consistency.

Run unit tests:
```
cd tests;
python test_verifier.py;
```

### CLI Usage

* ``` -g ```: Define the RDF schema (aka glossary) in use for your ontology.
* ``` -gf ```: Define the format the schema is in. By default validator.py
will try to auto-guess based on extension. However, if additional plugins are
installed it is best practice to manually specify it.

* ``` -i ```: The external tool's output you want to verify the ontology 
against.

* ```-if```: Define RDF schema for tool data that's being injested.
* ```--debug```: Break on errors that occur within ```--verify```.
* ```-tg```: Print subject, predicate, object for each graph within tool schema.
* ```-gg```: Print subject, predicate, object for each graph within glossary
* schema.


### CLI Example


* Check for inconsistencies between graphs:

```
rdfdiff.py -g case.ttl -gf turtle -i output.json-ld -if json-ld --verify=1
```

* Check for inconsistencies between graphs with color output:
```
rdfdiff.py -g case.ttl -gf turtle -i output.json-ld -if json-ld --verify=1
--color=1
```

* Enter debug mode. This will cause a PDB session to open when an inconsistency
* is met. This can be useful for manually navigating the RDF graph in Python.:
```
rdfdiff.py -g case.ttl -gf turtle -i output.json-ld -if json-ld --verify=1
--debug=1

```

* Print all graphs for tool's schema.

```
rdfdiff.py -g case.ttl -gf turtle -i output.json-ld -if json-ld -tg=1
```

* Print all graphs for ontology's schema.

```
rdfdiff.py -g case.ttl -gf turtle -i output.json-ld -if json-ld -gg=1
```

# I have a question!

Before you post a Github issue or send an email ensure you've done this checklist:

1. [Determined scope](https://caseontology.org/ontology/start.html#scope) of your task. It is not necessary for most parties to understand all aspects of the ontology, mapping methods, and supporting tools.

2. Familiarize yourself with the [labels](https://github.com/casework/RDFDiff/labels) and search the [Issues tab](https://github.com/casework/RDFDiff/issues). Typically, only light-blue and red labels should be used by non-admin Github users while the others should be used by CASE Github admins.
*All but the red `Project` labels are found in every [`casework`](https://github.com/casework) repository.*

3. If/when you run into an issue with a given RDF schema format or the verifier.py script, please open an issue with the error and as much technical detail as you can provide.
