# Validation

## About

SHACL stands for Shapes Constraint Language and is a W3C 
recommendation [https://www.w3.org/TR/shacl/](https://www.w3.org/TR/shacl/). It is a means for defining expected 
conditions in a graph.  This is done by defining a shape graph that contains these "shapes" in 
RDF.  RDF graphs that are used in this manner are called "shapes graphs" in
SHACL and the RDF graphs that are validated against a shapes graph are called "data graphs".

To process these shape and data graph tooling is required.  There are several existing tools that can be 
used for this.  The [Implementation Report](https://w3c.github.io/data-shapes/data-shapes-test-suite/) gives
a good overview of the current state of these tools.  For this documentation we will focus on the 
pySHACL implementation but much of this should run fine in any of the implementations.  

### References

| References                                                | On-Line Tools                                                   | CLI                                          | Browser Extension                                                                                                                                           | Software                                            |
|-----------------------------------------------------------|-----------------------------------------------------------------|----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| [W3C SHACL](https://www.w3.org/TR/shacl/)                 | [SHACL Playground](https://shacl.org/playground/)               | [pySHACL](https://github.com/RDFLib/pySHACL) | [Schema Builder for Structured Data](https://chrome.google.com/webstore/detail/schema-builder-for-struct/klohjdodjjeocpbpadmkcndjoadijgjg?hl=en-US)         | [Corese SHACL](http://wimmics.inria.fr/corese)      |
| [Editors Draft](https://w3c.github.io/data-shapes/shacl/) | [SHACL Playground zazuko](https://shacl-playground.zazuko.com/) |                                              | [Validate Schema in Schema Markup Validator](https://chrome.google.com/webstore/detail/validate-schema-in-schema/bambpgngabopanfbbpkknnogpomkaipp?hl=en-US) | [dotNetRDF](https://github.com/dotnetrdf/dotnetrdf) |
|                                                           | [Tangram](https://tangram.gleaner.io)                           |                                              | [Science on Schema.org](https://chrome.google.com/webstore/detail/science-on-schemaorg/blpbacopppjgpoedkiglokdheiegajpn?hl=en-US)                           | [Netage](http://www.netage.nl/)                     |
|                                                           |                                                                 |                                              |                                                                                                                                                             | [pySHACL](https://github.com/RDFLib/pySHACL)        |
|                                                           |                                                                 |                                              |                                                                                                                                                             | [RDFUnit](http://aksw.org/projects/RDFUnit)         |
|                                                           |                                                                 |                                              |                                                                                                                                                             | [shaclex](https://github.com/labra/shaclex)         |
|                                                           |                                                                 |                                              |                                                                                                                                                             | [TopBraid](https://github.com/TopQuadrant/shacl)    |
 

## In the context of Go FAIR Implementation Networks

<div>
<img src="./images/relations.png"  width="600"/>
<div>



- IMPLEMENT  clearly defined plans and deliverables to implement an element of the Internet of FAIR Data and Services (IFDS) within a defined time period;
- FOSTER  a community of harmonized FAIR practices;
- COMMUNICATE  together on critical issues on which consensus has been reached and which are of generic importance for the community.



### RDF Conceptual Model

A brief tour of RDF conceptual mode, the RDF ecosystem and SHACL (and JSON-LD) in that ecosystem.

<div>
<img src="./images/ecosystem.png"  width="600"/>
<div>

Image credit: Pierre-Antoine Champin  https://www.w3.org/Talks/2021/09-19-ddi-cdi/?full#rdf-ecosystem


### Validation Options

- [JSON Schema](https://json-schema.org/)
- [ShEx](http://shex.io/)
- [W3C SHACL](https://www.w3.org/TR/shacl/)
- Others like [Cue](https://cuelang.org/) lang and many more

### Why SHACL?

SHACL is on a W3C recommendation track while ShEx is a community project.  SHACL has also shown 
wider adoption in the JSON-LD and broader structured data on the web community including Solid.

## Severity

A brief note on severity levels.  SHACL defines [three levels of severity](https://www.w3.org/TR/shacl/#severity).  These can be useful to convey issues that are not violations for use, but are just warning and info related items.

| Severity     | Description                                                            |
|--------------|------------------------------------------------------------------------|
| sh:Info      | A non-critical constraint violation indicating an informative message. |
| sh:Warning   | A non-critical constraint violation indicating a warning.              |
| sh:Violation | A constraint violation.                                                |




## Command Line Tools

There are several CLI based tools that be used.  Most of the tools at the [Implementation Report](https://w3c.github.io/data-shapes/data-shapes-test-suite/) can
be used at the command line.  

### pySHACL Command Line Use

Full details on the command line for pySHACL can be found at the [project REDME.md](https://github.com/RDFLib/pySHACL/blob/master/README.md)


For command line use:
_(these example commandline instructions are for a Linux/Unix based OS)_
```bash
$ pyshacl -s /path/to/shapesGraph.ttl -m -i rdfs -a -j -f human /path/to/dataGraph.ttl
```
Where
- `-s` is an (optional) path to the shapes graph to use
- `-e` is an (optional) path to an extra ontology graph to import
- `-i` is the pre-inferencing option
- `-f` is the ValidationReport output format (`human` = human-readable validation report)
- `-m` enable the meta-shacl feature
- `-a` enable SHACL Advanced Features
- `-j` enable SHACL-JS Features (if `pyhsacl[js]` is installed)

System exit codes are:
`0` = DataGraph is Conformant
`1` = DataGraph is Non-Conformant
`2` = The validator encountered a RuntimeError (check stderr output for details)
`3` = Not-Implemented; The validator encountered a SHACL feature that is not yet implemented.


## Language support

Beyond the command line, several tools and libraries can be leveraged in a range of programming languages.  
These include Java, Python, DotNet, and Scala.  Also, some RDF triplestores also have support for 
processing SHACL natively.

pySHACL examples  ([https://github.com/RDFLib/pySHACL/](https://github.com/RDFLib/pySHACL/))

[kglab](https://derwen.ai/docs/kgl/) tutorial on [SHACL validation with pySHACL](https://derwen.ai/docs/kgl/ex5_0/)

```python
from pyshacl import validate
r = validate(data_graph,
      shacl_graph=sg,
      ont_graph=og,
      inference='rdfs',
      abort_on_first=False,
      allow_warnings=False,
      meta_shacl=False,
      advanced=False,
      js=False,
      debug=False)
conforms, results_graph, results_text = r
```


## Online Tools

### SHACL Playground

You can try SHACL at the [SHACL Playground](https://shacl.org/playground/)

### Tangram

Tangram [https://tangram.gleaner.io](https://tangram.gleaner.io)

```bash
curl -F 'datagraph=@./datagraphs/dataset-minimal-BAD.json-ld' -F 'shapegraph=@./shapegraphs/googleRecommended.ttl' -F 'format=machine' https://tangram.gleaner.io/uploader 
```


### A brief aside on JSON-LD Structure Validation

####  Validate the structure of the JSON-LD data graph

These test that your document is well formed but not necessarily valid against a vocabulary or profile / guidance.

* [JSON-LD Playground](https://json-ld.org/playground/)
* [Structured data Linter](http://linter.structured-data.org/)


#### Validates against Schema.org usage

This includes things like domain and range issues and predicate and type terms.

* [SDO Validator](https://validator.schema.org/)

## Browser tools

These Chrome based extensions and the author was unable to find any for FireFox.


[Schema Builder for Structured Data](https://chrome.google.com/webstore/detail/schema-builder-for-struct/klohjdodjjeocpbpadmkcndjoadijgjg?hl=en-US)
an extension that allows you to easily build validated json-ld structured data markup for any 
webpage. Based on schema.org specification it has support for many but all types.  The Dataset type is included though.  

[Validate Schema in Schema Markup Validator](https://chrome.google.com/webstore/detail/validate-schema-in-schema/bambpgngabopanfbbpkknnogpomkaipp?hl=en-US)
This is a simple Chrome extension that simply takes the 
current page and loads it into the [schema.org validator](https://validate.schema.org) mentioned earlier.  

[Science on Schema.org](https://chrome.google.com/webstore/detail/science-on-schemaorg/blpbacopppjgpoedkiglokdheiegajpn?hl=en-US)
An extension by Dave Vieglais which is open source at [soso-chrome](https://github.com/datadavev/soso-chrome)

## Other topic

### Linking Constraints to associate a data graph with a SHACL graph

Though there is no formal approach to this we can leverage the web architecture environment to do this.  One
possible approach would be to use something like the following:

The LDP specification introduces an IRI to be used to advertise any constraints on the ability of a client to create or update resources:

```
Link: <https://example.com/SpecificErrorCondition>; rel="http://www.w3.org/ns/ldp#constrainedBy"
```

```html
<link rel="http://www.w3.org/ns/ldp#constrainedBy" href="shape.jsonld">
```

This feature could potentially be used to accomplish a high level of interoperability across servers.

[https://www.w3.org/TR/ldp/#h-ldpr-gen-pubclireqs](https://www.w3.org/TR/ldp/#h-ldpr-gen-pubclireqs)

4.2.1.6 LDP servers must publish any constraints on LDP clients’ ability to create or update LDPRs, by adding a Link header with an appropriate context URI, a link relation of http://www.w3.org/ns/ldp#constrainedBy, and a target URI identifying a set of constraints [RFC5988], to all responses to requests that fail due to violation of those constraints. For example, a server that refuses resource creation requests via HTTP PUT, POST, or PATCH would return this Link header on its 4xx responses to such requests. The same Link header may be provided on other responses. LDP neither defines nor constrains the representation of the link's target resource. Natural language constraint documents are therefore permitted, although machine-readable ones facilitate better client interactions. The appropriate context URI can vary based on the request's semantics and method; unless the response is otherwise constrained, the default (the effective request URI) should be used.

Inbox URLs can announce their own constraints (e.g., SHACL, Web Annotation Protocol) via an HTTP Link header or body of the resource with a rel value of http://www.w3.org/ns/ldp#constrainedBy. Senders should comply with constraint specifications or the receiver may reject their notification and return an appropriate 4xx error code.