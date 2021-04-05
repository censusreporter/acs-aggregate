# US Federal Court District to US County Crosswalk

As part of our work with the [SCALES](https://scales-okn.org/) project, we set out to create a crosswalk which would support analysis of Census and other data by US Federal Court District.

The districts are established by statute, specifically, [Title 28, United States Code, Chapter 5](https://www.law.cornell.edu/uscode/text/28/part-I/chapter-5). Generally, each US county is in exactly one District. There are a few special cases such as with waterways around New York City, a Federal Correctional Institution in North Carolina, and the like, but those are disregarded for the purposes of creating this cross-reference.

Some Federal Court Districts are split into "Divisions" by the statute. There are also cases of local (non-statutory) rules creating Divisions in Federal Court Districts. Statutory divisions are included in this data set -- if a District has Divisions, each county is in exactly one. Local-rule Divisions are **not included** in this data. 

## The data file

The [crosswalk](county_district_xref.csv) is a UTF-8 encoded CSV file with one row per US county or county-equivalent. Each row has the following columns, each of which should be treated as text, even though some have only digits:

* geoid - a US Census Bureau [GEOID](https://www.census.gov/programs-surveys/geography/guidance/geo-identifiers.html). Each value is unique in this file. 
* state_fips - a two-digit [state FIPS code](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standard_state_code#FIPS_state_codes)
* county_fips - a three-digit [county FIPS code](https://en.wikipedia.org/wiki/List_of_United_States_FIPS_codes_by_county)
* state - the state's name, in text
* county - the county or county-equivalent's name
* district - the name of the district, or the state name if the state is not divided into districts
* division - the name of the division, or blank if the district does not have statutory divisions
* statute_url - a link to the Cornell LII version of the statute for the given state, in case one wants to validate/review the data

We welcome input from people with expertise about whether there's a more systematic way to represent the districts and divisions, such as numeric or coded identifiers. 

(We've since learned about [a GIS file of districts](https://hifld-geoplatform.opendata.arcgis.com/datasets/us-district-court-jurisdictions) which includes identifiers. In the future we may either use that file to create the crosswalk, or at least integrate its IDs to make it easier to create maps based on aggregated data. See also [this nice interactive javascript map](https://observablehq.com/@caged/the-united-states-courts-of-appeals-and-district-courts) of the districts and counties...)

## Using this crosswalk

This repository includes two notebooks demonstrating how you can use the crosswalk with python code to aggregate ACS data by Judicial District:

* [population_by_district.ipynb](population_by_district.ipynb) - a simple case to get the estimated total population for each district. If you just want that data, download [population_by_district_acs2018_5yr.csv](population_by_district_acs2018_5yr.csv)
* [race_by_district.ipynb](race_by_district.ipynb) - a more involved example which also shows how to account for the aggregated margin of error, and how to test the reliability of the aggregates.

Of course, you don't have to use python to use the crosswalk, but it's our working language, so it was easiest to use for demonstration. We'll gladly link to examples using `R` or other tools.

## More on the method

The crosswalk here is not purely created by code. We were able to match most of the counties with a scraper (available in this [Google Colab notebook](https://colab.research.google.com/drive/1ghrzwtNhwlN6E3GBH8N5zqP9cAOPOGd0#scrollTo=LtDXNodX4KO9)), but at a certain point, it didn't seem worth working through formatting peculiarities, misspellings in the statute, and annoying nuances of regular expressions. 

We are particularly grateful to Mary Catherine Talbott, University of Richmond Law Student, Class of 2022, for careful review of the cities of Virginia, which, while treated as "county-equivalents" by the Census, are not specifically enumerated in the statute.
