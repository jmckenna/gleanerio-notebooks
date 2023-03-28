# Notes

## Dashboards

Converting notebooks to dashboards is a common goal for many.  Approaches 
like Dash and Streamlit are the most common but there are many others.

Some of these are; 

* [Streamlit](https://streamlit.io/)
* [Dash](https://plotly.com/dash/)
* [Mercury](https://github.com/mljar/mercury)
* [PieSparrow](https://piesparrow.itsdaniyalm.com/)


## Utils

* [LineaPy](https://github.com/LineaLabs/lineapy)
* [Fugue](https://fugue-tutorials.readthedocs.io/tutorials/quick_look/ten_minutes.html)
* [LangChain](https://github.com/hwchase17/langchain)

## Re-org

All three main users (GeoCODES, IoW, Oih, Polder? and more) are looking at:

- Validation via SHACL (leverage Dask)
- robots.txt and sitemap.xml validation
- Graph assessment via SPARQL (graph assay)
- Site review template (for reporting results)
- spatial assessment
- semantic assessment (really X assessment)



## Setting Metadata for LaTeX export

Add the following to your notebook metadata:

```JSON
{
   "kernelspec": {
      "name": "conda-env-.conda-kglab-py",
      "display_name": "Python [conda env:.conda-kglab] *",
      "language": "python"
   },
   "language_info": {
      "name": "python",
      "version": "3.8.10",
      "mimetype": "text/x-python",
      "codemirror_mode": {
         "name": "ipython",
         "version": 3
      },
      "pygments_lexer": "ipython3",
      "nbconvert_exporter": "python",
      "file_extension": ".py"
   },
   "authors": [{
      "name": "Ocean InfoHub, IOC Ocean Data and Information System"
   }],
   "institution": [
      "IOC Ocean Data and Information System"
   ],
   "subtitle": "A review of patterns",
   "title": "SeaDataNet metadata"
}

```
