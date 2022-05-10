# Messages


## About

This document provides short descriptions of constraints defined 
by the SHACL files.  The SHACL files provide references when a 
constraint fails and those references point here.  

### @id should be provided

A JOSN-LD document requires an @id value

### DataDownload validation set

The set of validations related to data download

### DataDownload: contentURL missing

Content URL missing for the data download.  This would be a URL that
downloads the subject of the metadata.  It applies to things such as 
data or creative works.  

### DataDownload: encodingFormat is required

The encodingFormat of the described resource.

### OIH Dataset Resource validation set

The set of validations related to some generally related checks

### distribution required

A schema:Distribution is required

### Included variableMeasured, if available

If available the measured variables in a file should be enumerated using
schema:variableMeasured 

### Name is required

A schema:name property is required

### URL required for described resource

A schema:url for the resource is required

### Resource must have a description

A resource must have a description that uses schema:description

### Resource must have an identifier node

A resource must have an identifier

### Resource must have one or more keywords

A resource must at least one keyword
