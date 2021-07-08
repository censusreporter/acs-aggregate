# Sources of Boundary Information

Often people who want to use a tool like `acs-aggregate` have a bootstrapping problem: where are the GIS files for the areas for which they want to aggregate data?

While this will probably be hard to keep up to date, and perhaps should be in some form other than markdown in this repository, let's take a stab at building a list. 

*Since this is about aggregating Census data, let's stipulate that it should only include polygon data, not points and lines. And, only boundaries relevant to the United States and its territories. We'll organize it by state (or state-like.)*

## US - United States

* [Home Owners' Loan Corporation (HOLC) "Redlining" maps](https://dsl.richmond.edu/panorama/redlining/#text=downloads) (also available for many specific cities)
* [US District Court Jurisdictions](https://hifld-geoplatform.opendata.arcgis.com/datasets/us-district-court-jurisdictions) (see also [`COUNTY_DISTRICT_README.md`](crosswalks/judicial_districts/COUNTY_DISTRICT_README.md))

## CO - Colorado

* [Various state-level files](https://demography.dola.colorado.gov/gis/gis-data/) including hospital, library, water, fire protection districts and more

## DC - Washington, DC

* [Washington, DC Neighborhood Clusters](https://opendata.dc.gov/datasets/f6c703ebe2534fc3800609a07bad8f5b_17)

## GA - Georgia

* [Atlanta Neighborhoods](https://dpcd-coaplangis.opendata.arcgis.com/datasets/neighborhood/)
* [Atlanta Neighborhood Planning Units](https://dpcd-coaplangis.opendata.arcgis.com/datasets/npu) (NPUs)


## HI - Hawaii

* [Honolulu "Realtor Neighborhoods"](https://honolulu-cchnl.opendata.arcgis.com/datasets/neighborhoods-realtor-neighborhoods/)

## IL - Illinois

* [Chicago Neighborhoods](https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Neighborhoods/bbvz-uum9)
* [Chicago Community Areas](https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6)
* [Chicago Police Districts](https://data.cityofchicago.org/Public-Safety/Boundaries-Police-Districts/4dt9-88ua)
* [Chicago City Council Wards](https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Wards-2015-/sp34-6z76)

## IN - Indiana

* [Bloomington City Neighborhood Associations](https://data.bloomington.in.gov/dataset/city-neigbhorhoods-gis-data)


## MA - Massachusetts

* [Boston Neighborhoods](https://data.boston.gov/dataset/boston-neighborhoods)
* [Cambridge CDD (Community Development Department) Neighborhoods](https://www.cambridgema.gov/GIS/gisdatadictionary/Boundary/BOUNDARY_CDDNeighborhoods)

## MI - Michigan

* [Detroit neighborhood bondaries](https://data.detroitmi.gov/datasets/neighborhoods)

## MO - Missouri

* [Kansas City neighborhood boundaries](https://data.kcmo.org/Neighborhoods/Kansas-City-Neighborhood-Boundaries/q45j-ejyk)
* [St. Louis city shapefile data](https://www.stlouis-mo.gov/data/formats/format.cfm?id=21) (includes ward and neighborhood boundaries as well as other divisions)

## NY - New York

* [New York City Community Districts](https://data.cityofnewyork.us/City-Government/Community-Districts/yfnk-k7r4)
* [New York City Council Districts](https://data.cityofnewyork.us/City-Government/City-Council-Districts/yusd-j4xi)
* [New York City Election Districts](https://data.cityofnewyork.us/City-Government/Election-Districts/h2n3-98hq)
* [New York City Neighborhood Tabulation Areas (NTAs)](https://data.cityofnewyork.us/City-Government/NTA-map/d3qk-pfyz) (note that an [NTA-census tract crosswalk](https://www1.nyc.gov/assets/planning/download/office/data-maps/nyc-population/census2010/nyc2010census_tabulation_equiv.xlsx) is available)
* [New York City School Districts](https://data.cityofnewyork.us/Education/School-Districts/r8nu-ymqj) (to the Census, NYC is one big district)


## OR - Oregon

* [Portland Neighborhood Association Boundaries](https://hub.arcgis.com/datasets/1ef75e34b8504ab9b14bef0c26cade2c_3)

## PA - Pennsylvania

* [Philadelphia Neighborhoods](https://www.opendataphilly.org/dataset/philadelphia-neighborhoods)
* [Pittsburgh Neighborhoods](https://data.wprdc.org/dataset/neighborhoods2)

## RI - Rhode Island

* [Providence Neighborhoods](https://pvdgis.maps.arcgis.com/home/item.html?id=368395369304497090ddb33f5636da87)
* [Providence Wards](https://pvdgis.maps.arcgis.com/home/item.html?id=36468e873abd482ba89aa58be9613ce0)

## TX - Texas

* [Houston "Super Neighborhoods"](https://cohgis-mycity.opendata.arcgis.com/datasets/c3bfee99cbc14a899e4a603ee73203ee_3/)

## WA - Washington

* [Seattle Community Reporting Areas](http://data-seattlecitygis.opendata.arcgis.com/datasets/community-reporting-areas)
* [Seattle "City Clerk" Neighborhoods](http://data-seattlecitygis.opendata.arcgis.com/datasets/city-clerk-neighborhoods)
* [Seattle Council Districts](http://data-seattlecitygis.opendata.arcgis.com/datasets/council-districts)

---
If you aren't finding what you're looking for above, here are some other resources which haven't been fully explored yet:


* while it may or may not be current, the [GitHub repo](https://github.com/codeforamerica/click_that_hood/tree/master/public/data) for [Click That Hood](http://click-that-hood.com/) is worth a look if you don't find what you're looking for here -- and it goes far beyond the US as well.
* The Big Ten Academic Alliance has a [Geoportal](https://geo.btaa.org/) with links to [geodata for a number of US municipalities](https://geo.btaa.org/?f%5Bdc_subject_sm%5D%5B%5D=Municipalities+geospatial+data)
Also, while it may or may not be current, the [GitHub repo](https://github.com/codeforamerica/click_that_hood/tree/master/public/data) for [Click That Hood](http://click-that-hood.com/) is worth a look if you don't find what you're looking for here -- and it goes far beyond the US as well. 
* For a while, Zillow offered neighborhood maps that they pulled together for their service. They no longer provide it, but I came across [this site](https://mapcruzin.com/free-download-neighborhood-boundary-shapefiles.htm) which seems to have archived them. They're organized by state, but for many states, there are only neighborhoods for a single city.
* [Koordinates.com](https://Koordinates.com) is a geospatial data management platform which has aggregated GIS data from diverse sources. At the time of this writing, [a search for 'neighborhood'](https://koordinates.com/search/?q=neighborhood) gets well over 500 hits.
