# Report for INVEMAR

## Resources reviewed

* http://portete.invemar.org.co/chm/api/oih/expert?format=json
* http://portete.invemar.org.co/chm/api/oih/documents?format=json
* http://portete.invemar.org.co/chm/api/oih/institution?format=json
* http://portete.invemar.org.co/chm/api/oih/vessel?format=json
* http://portete.invemar.org.co/chm/api/oih/training?format=json

## Additional tooling used

In addition to Jupyter notebooks leveraging Python we can also inspect resources like this rather 
quickly from the command line. I used the following tools in addition to the standard 
curl and sed which would be found in common Linux, or Mac OS X environments.  
For Windows there is [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/) 
and also the ability to run Linux virtual machines with open source tools like [Virtual Box](https://www.virtualbox.org/).

The extra tools are jq and the jsonld cli from the Javascript JSON-LD library:

* jq  https://stedolan.github.io/jq/
* jsonld  https://github.com/digitalbazaar/jsonld.js   (installs a command line script)

The commands used to pull and explore the resources follow:

```bash
curl 'http://portete.invemar.org.co/chm/api/oih/expert?format=json' | sed  -e 's/\\\\//g' | jsonld frame --frame frames/person_frame.json | jq '.["@graph"][68]'

curl 'http://portete.invemar.org.co/chm/api/oih/documents?format=json' | sed  -e 's/\\\\//g' | jsonld frame --frame frames/crtvwrk_frame.json | jq '.["@graph"][68]'

curl 'http://portete.invemar.org.co/chm/api/oih/institution?format=json' | sed  -e 's/\\\\//g' | jsonld frame --frame frames/org_frame.json | jq '.["@graph"][68]'

curl 'http://portete.invemar.org.co/chm/api/oih/vessel?format=json' | sed  -e 's/\\\\//g' | jsonld frame --frame frames/vessel_frame.json | jq '.["@graph"][68]'

curl 'http://portete.invemar.org.co/chm/api/oih/training?format=json' | sed  -e 's/\\\\//g' | jsonld frame --frame frames/course_frame.json | jq '.["@graph"][68]'

```

We can break down what is going on here by rebuilding this UNIX command element by element.


```bash
curl 'http://portete.invemar.org.co/chm/api/oih/expert?format=json'
```

The above is the simple base curl call to pull down the JSON-LD


```bash
curl 'http://portete.invemar.org.co/chm/api/oih/expert?format=json' | sed  -e 's/\\\\//g'
```

The above pipes this into sed to resolve an issue with the Schema.org reference URL.  This seems likely due to the hosting Django framework
processing the output in some manner, though the exact cause is not known.


```bash
curl 'http://portete.invemar.org.co/chm/api/oih/expert?format=json' | sed  -e 's/\\\\//g' | jsonld frame --frame frames/person_frame.json
```

We can now use the jsonld command to frame the results to pull out specific examples from the larger graph.

Note:  You could also use

```bash
curl 'http://portete.invemar.org.co/chm/api/oih/expert?format=json' | sed  -e 's/\\\\//g' | jsonld format
```

to simply see the JSON-LD nicely formatted, which is also a quick structure check too since this will error out on badly formed JSON-LD.
All the JSON-LD from these sources was nicely formatted. 


```bash
curl 'http://portete.invemar.org.co/chm/api/oih/expert?format=json' | sed  -e 's/\\\\//g' | jsonld frame --frame frames/person_frame.json | jq '.["@graph"][68]'
```

We can not pass the framing results through jq and use this to pull out random elements from the array.  Here I picked item 68 but you could pick any 
number N where N is less than the number of items in the sitegraph item list.

Note:  For cases where the framed type is also used in the ItemList you may get entries in the first and or second array slots that are duplicate.  For 
example the type CreativeWork is used to multi-type the ItemList.  So, framing for CreativeWork returns the entire document as the first
array item.  There is no issue with this, as long as the user is aware of this behavior.


## Summary of examples

I am including an example element from each graph mostly for references here.

> Note:   The vessel entries are quite large so I am not including it in the examples.  
> However, it is quite excited to see such detailed entries 
> or that type by INVEMAR  The vessel pattern was the weakest of the initial set so 
> engaging with INVEMAR to use these records to improve that OIH type guidance is planned.



```json
{
  "@id": "_:b1185",
  "@type": "Person",
  "affiliation": "Universidad de Córdoba",
  "jobTitle": "Geografo",
  "name": "Universitario Katy Julieth GOMEZ",
  "nationality": {
    "@id": "_:b1186",
    "@type": "Country",
    "name": "Colombia"
  },
  "thumbnailUrl": "https://www.oceanexpert.net/uploads/profile/profile_32958.png",
  "url": "https://oceanexpert.org/expert/32958"
}
```

```json
{
  "@id": "_:b223",
  "@type": "CreativeWork",
  "description": "A partir de insumos obtenidos de sensores remotos, se ha realizado el análisis multitemporal de la evolución del borde costero de la bahía de Tumaco, en aproximadamente 780 km, permitiendo identificar...",
  "name": "Determinación de la variación morfológica costera de la Bahía de Tumaco, a partir de análisis multitemporal con sensores remotos",
  "thumbnailUrl": "https://www.oceandocs.org/bitstream/handle/1834/15220/dimarcioh_2018_boletincioh_036_071-086.pdf.jpg?sequence=3&isAllowed=y",
  "url": "https://www.oceandocs.org/handle/1834/15220"
}
```

```json
{
  "@id": "_:b282",
  "@type": "Organization",
  "address": {
    "@id": "_:b283",
    "@type": "PostalAddress",
    "addressLocality": "",
    "streetAddress": "St 55 # 1-94 Cali, , 760002 Colombia"
  },
  "name": "Global Youth Biodiversity Network GYBN",
  "thumbnailUrl": "/static/main/index/images/inst-default.png",
  "url": "https://oceanexpert.org/institution/20945"
}
```

```json
{
  "@type": "Course",
  "author": {
    "@type": "Organization",
    "name": "Autonomous University of Tamaulipas"
  },
  "contentLocation": "Mexico",
  "educationalCredentialAwarded": " Formal BS",
  "email": "ecienfue@uat.edu.mx",
  "name": "Autonomous University of Tamaulipas ->   Faculty of Engineering and Sciences ->   Engineer in Environmental Sciences",
  "teaches": "",
  "url": "http://www.uat.edu.mx/Paginas/CAMPUS-FACULTADES/CAMPUS-FACULTADES.aspx"
}
```


## Observations

### Schema.org URL encoding

As noted above, the biggest issue that holds up the easy use of these in our OIH graph workflow 
is the formmat of the schema.org URL.  It can be see as:

```json
"@context": {
    "@vocab": "https:\\/\\/schema.org\\/"
}
```

this needs to be:

```json
"@context": {
    "@vocab": "https://schema.org/"
}
```

which for this testing I fixed with sed.  However, this 
needs to be addressed for the production workflow.

### Lack of ID

The source graph does not contain an @id entry.  This will be problematic in some use patterns
when we start to pass the graph around or leverage it in a linked open data approach.  To 
help with this it would be good if an @id was added.   

The @id is used to identify the metadata record, not the resource being described by the record.
So there are some patterns we could try here to make this easy.

One example might in the case of the resources found in:

```
http://portete.invemar.org.co/chm/api/oih/institution?format=json
```

In that resource there is an example entry like:

```json
{
  "@type": "Organization",
  "address": {
    "@id": "_:b283",
    "@type": "PostalAddress",
    "addressLocality": "",
    "streetAddress": "St 55 # 1-94 Cali, , 760002 Colombia"
  },
  "name": "Global Youth Biodiversity Network GYBN",
  "thumbnailUrl": "/static/main/index/images/inst-default.png",
  "url": "https://oceanexpert.org/institution/20945"
}
```

We want the resource ID for a given entry to always be the same.  So, simply numbering them 
is problematic since the order might change due to generator code updates or simply the randomness
of working with certain language aggregations like maps.  

To address this we could try and hash the name of the entry and use that.  The name is 
likely, though not guarenteed to be unique.  So, for example the name:

```
Global Youth Biodiversity Network GYBN
```

Could be SHA256 hashed.  Again, using the command line we could something like what
follows.  Be sure not to have extra spaces at the ends as these will be used in 
the hash generation and might cause confusion later.  This example uses the command
line resources but most all language have such hashes either built in or available as 
packages.  


```bash
(base) ➜  work echo "Global Youth Biodiversity Network GYBN" | sha256sum
c2fb9f04fe180afcd412f201678dc9da2a60167c3a96b6b757b4939650c47d6f  -
```

So our @id could become:

```
http://portete.invemar.org.co/chm/api/oih/institution#c2fb9f04fe180afcd412f201678dc9da2a60167c3a96b6b757b4939650c47d6f  
```

and the modified record would not be:

```json
{
  "@id":  "http://portete.invemar.org.co/chm/api/oih/institution#c2fb9f04fe180afcd412f201678dc9da2a60167c3a96b6b757b4939650c47d6f  
  "@type": "Organization",
  "address": {
    "@id": "_:b283",
    "@type": "PostalAddress",
    "addressLocality": "",
    "streetAddress": "St 55 # 1-94 Cali, , 760002 Colombia"
  },
  "name": "Global Youth Biodiversity Network GYBN",
  "thumbnailUrl": "/static/main/index/images/inst-default.png",
  "url": "https://oceanexpert.org/institution/20945"
}
```

I use the URL fragment rather than the URL path pattern since the fragment should be ignored in processing and will give us back
the results for the URL base irrespective of the fragment value.  However, it can still work in our graph space so we can 
have an identifier that works in both graph space and linked open data space.  

SHA hashes are a bit long, but this is not an issue for the machines and this
is an ID for machines not people.   

Other approaches could be used to generate a unique ID it simply needs to be a documented
policy and proceedure of the group.  

> Note the generated IDs need to comply with the IRI formating.  This [RDF and IRI Syntax](https://afs.github.io/rdf-iri-syntax.html)
> provides a nice summary and list of resources for review.  It also provides links to 
> uses of URN or UUID patterns that may be used in place of the HTTP + SHA256 pattern
> above.


### Lack of description

Some of the resources have descriptions, some do not.  Descriptions are vital to discovery patterns since
many first passes at search leverage text indexes and not graph patterns.   Any work that can expand the 
number of resources with descriptions will greatly improve recovery of those resources later.  

Note, when the URL encoding for schema.org is resolved I will be able to process these through our
SHACL validation pipelines and give you a better overview of coverage for predicates like this.


### Language encode the description  

Those with description are obviously mostly in Spanish.  This is a great opportunity for us to work 
together to gain operational experience with language encoding.  Reference 
[OIH Book: Lamguges](https://book.oceaninfohub.org/thematics/languages/languages.html) for an example.
The example uses label but that pattern can be directly applied to description or other object
literal entries.  

### https vs http

Though not vital at this time, any production implementation likely should use https to avoid 
potential cross network schema issues in the future.  


