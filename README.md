# Gleaner Notebooks

## About

The notebooks here are focused on supporting people using JSON-LD and
structured data on the web.  They are specific to the use of Gleaner but 
some do work on the idea that objects are collected to an object store. 


## Checking Sitemaps

The notebook [sitemap assay](./notebooks/sitemap_assay.ipynb) can 
be used to review the configuration and the elements, or a subset
of elements, 

Note that the __Plot sitemap diversity__ section my not be of value for 
many groups.  It was used in cases where the URL path has more varied
structure.  In some cases the structure is the same till the end
path element.  In those cases the graphs will be busy (slow) and not
very useful.  

The __Sample and test sitemap entries__ section near the end cab be used
to spot check a sample of the sitemap URLs, or modified to check more
or all.  That section can also check for JSON-LD in the resources too.

> NOTE:  The checking does not work for resources that dynamically 
> place the JSON-LD in the DOM.  Doing so would not be hard to do in this
> notebook but is not present yet.  

It also has a section that will attempt to pull down the JSON-LD and 
validate its structure by a simple compact call. 

