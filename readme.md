# Predicting Fire Risk for New York City Census Tracts

### Problem Statement 

Urban fires, especially structural fires, are potentially dangerous incidents that can have devastating outcomes. In 2018 alone, New York City had a total of 27,053 structural fires resulting in the deaths of 88 civilians. While fire departments have worked to improve response times and conduct risk assessment inspections to better identify vulnerable or at-risk properties, there are many obstacles to addressing this risk in its entireity.

This leads us to our problem:
- Using machine learning how accurately can we predict if a census tract will have a structural fire for a given year?
- How accurately can we predict the number of structural fires that will occur in a given census tract for a given year?

---

### Project Files

Here is the workflow order to follow when running through the notebooks:
- [Bokeh Map of Fire Incidents](code/bokeh-map-of-fire-incidents)
- [FDNY Data & Geocoding](link) 
- [MapPLUTO & Census Tracts](link) 
- [ACS Housing Data](link) 
- [Modeling Fire Risk for Census Tracts](link)

---

### Executive Summary

This project began with an initial survey of available data and scholarship that would be useful for predicting structural fire risk. After reading a few different papers (linked in the Resources folder), and exploring availability of relevant datasets on [New York City's Open Data Portal](https://opendata.cityofnewyork.us/), I settled on three main datasets that seemed to provide enough information to construct a working fire risk model. These datasets were:
- [Incidents Responded to by Fire Companies](https://data.cityofnewyork.us/Public-Safety/Incidents-Responded-to-by-Fire-Companies/tm6d-hbzd)
- [Primary Land Use Tax Lot Output (PLUTO)](https://www1.nyc.gov/site/planning/data-maps/open-data/dwn-pluto-mappluto.page)
- [ACS 5-Year Estimates - Selected Housing Characteristics](https://factfinder.census.gov/faces/tableservices/jsf/pages/productview.xhtml?src=bkmk)

The 'Incidents Responded to by Fire Companies' dataset was the source for fire incident data between January 2013 and December 2018. This dataset was accessed via the NYC Open Data API, cleaned, and filtered to only include certain 100-level fire codes (relating to structural or building fires), and some 200-level codes (relating to overpressures, ruptures, explosions, or overheat incidents, as with boilers or pipes). The dataset included various geographic identifiers, but as these identifiers were at a larger scale than would be useful for fire predictions, I opted to use the street name and zipcode provided to geocode the incidents in order to locate the census tract the incident occurred in. Using the ArcGIS geocoding API, I was able to get approximate coordinates for nearly every incident in the dataset. One caveat here is that the dataset only provided the name of the street that the incident occurred on and did not include the house or building number. Thus the geocoding can only be so precise with the coordinates for each incident. This step did, however, allow for a spatial join to be performed with a [shapefile](https://www1.nyc.gov/site/planning/data-maps/open-data/districts-download-metadata.page#collapse4) of New York City census tracts provided by the Department of City Planning. By doing this, each incident was able to be assigned to one of New York City's 2166 census tracts. Incident counts were then aggregated by census tract and by year and month, in order to both reduce the size of the dataset and allow for predictions to be generated on the same spatial and temporal scale.

This dataset was then merged with the MapPLUTO dataset, a shapefile version of the PLUTO dataset of all properties in New York City. The MapPLUTO shapefile was also spatially joined with the census tract shapefile to assign each property to a census tract. Selected features of properties were also aggregated by census tract with calculations being done to ensure that the features were aggregated appropriately. After this, the merge with the fire incident data yielded a dataset with the number of incidents in each tract per month as well as the features of the properties within that census tract.

This dataset was then merged with data pulled from the American Community Survey 5-Year Estimates Selected Housing Characteristics dataset. Variables from the ACS dataset were chosen based on their percieved relevance to predicting fire risk, and were calculated as percent of the total universe for each feature.

After merging these datasets together two forms of the dataset were produced, one with incident counts aggregated by month, and one with incident counts aggregated by year. Both of these datasets were then run through three classfication models: Random Forest Classifier, Adaptive Boost Classifier, and XG Boost Classifier. The classification model binarized the incident counts for each census tract, simply indicating if a fire occured in that census tract for each time period. Additionally, a Random Forest Regressor was run on the dataset of incidents aggregated by year to predict the number of fire incidents that would occur in each census tract for every year.



### Model Interpretation

---

### Conclusion and Next Steps



---

### Source Documentation

- [text](link) 
- [text](link) 
