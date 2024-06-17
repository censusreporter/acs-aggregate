# ZIP Code to ZCTA Crosswalk

While Census Reporter refers to ZIP codes in its interface, it's actually the case that American Community Survey (ACS) data is not available by ZIP code. Instead, the geography we call ZIP Code is a ZIP Code Tabulation Area, or ZCTA.

While folks commonly think of them as geographic areas, ZIP Codes actually identify a post office which handles delivering the mail to its final destination. While, in many cases, there's an implicit area that contains all of the addresses in that ZIP code, there are other ZIP codes where that doesn't work. There are ZIP codes which are only used for PO Boxes, and others which collect all the mail for a large business or organization that then handles the final delivery. In both of these cases, there's no straightforward way to draw them as an area on a map.

The key issue is that there are thousands of ZIP codes for which there is no corresponding ZCTA. And while the ACS data is tabulated by ZCTA, not ZIP code, there are other data sources which are at the ZIP Code level, not the ZCTA level, including Census programs like ZIP Code Business Patterns, or ZBP (part of the [County Business Patterns](https://www.census.gov/programs-surveys/cbp.html) program).

For a project where we wanted to integrate data from the ACS and the ZBP, we needed to come up with [a crosswalk assigning each ZIP Code to a ZCTA](zip_zcta_xref.csv). Since it was a bit of work, we wanted to share it with others who might need it. But, again, ZIP Codes change, so this file may go out of date. So we are also sharing the code and method in case you need to do it again with updated data files.

## The data file

`zip_zcta_xref.csv` provides a crosswalk between ZIP Codes and ZCTAs. It was created using [build_crosswalk.ipynb](build_crosswalk.ipynb), a reimplementation of the method described below.

<table>
    <tr>
        <th>column</th>
        <th>datatype</th>
        <th>notes</th>
    </tr>
    <tr>
        <td>zip_code</td>
        <td>text</td>
        <td>Source: Census Gazetteer, GeoNames or ZIP Code Business Patterns</td>
    </tr>
    <tr>
        <td>zcta</td>
        <td>text</td>
        <td>the best available ZCTA for the ZIP Code, or null in a small number of cases</td>
    </tr>
    <tr>
        <td>source</td>
        <td>text</td>
        <td>the original source of the ZIP Code in our data processing pipeline. You can probably ignore this.</td>
    </tr>
        
</table>

## Our method

Getting data about USPS ZIP codes is not exactly straightforward. The USPS does not provide a simple, free list. We used [a dataset](https://download.geonames.org/export/dump/US.zip) from [GeoNames](https://www.geonames.org/) as our master list. For a comprehensive list of ZCTAs, we used [the ZCTA file](https://www2.census.gov/geo/docs/maps-data/data/gazetteer/2017_Gazetteer/2017_Gaz_zcta_national.zip) from the [2017 Gazetteer files](https://www.census.gov/geographies/reference-files/time-series/geo/gazetteer-files.2017.html), although for this version, we use the Census's ZCTA ESRI Shapefile, which is just the Gazetteer plus geographic boundaries.

To the GeoNames master list, we added ZIP Codes in the ZIP Code Business Patterns data which weren't already in GeoNames. (See what we mean about it being hard without an authoritative master list?)

We began with the assumption that any ZIP Code which had a corresponding ZCTA (same 5-digit identifier) should be treated as the same as that ZCTA. This is not strictly true: the Census Bureau acknowledges that their method for assigning ZCTAs sometimes results in addresses being placed in a ZCTA that differs from the address's ZIP code. However, we didn't see any way we could feasibly deal with that issue.

After comparing the ZIP and ZCTA master lists, we identified nearly 8,000 ZIP Codes which do not have matching ZCTAs. 

The GeoNames dataset includes a geocode (latitude/longitude) for each ZIP code. It's not clear how those geocodes were assigned, so this is a leap of faith, but it's the best we had to go-on. We use GIS software to try locating non-ZCTA ZIP Codes in a ZCTA. It’s difficult to estimate what distortion might be introduced by this approach.

After the GIS analysis, we were left with about 100 ZIP Codes which were in GeoNames, and so had a geocode, but were not located in any ZCTA. There were also a few dozen ZIP codes which appeared in the ZBP dataset but which were not in either GeoNames or the ZCTA gazetteer. These were put to a manual review process. 

The process was thus: we loaded the ZIP Codes which weren't ZCTAs into [this Google Sheets document](https://docs.google.com/spreadsheets/d/1sbf-15PzHTnT6CsUMKcVnmhoHx-wKZ_PR-f_1WS5l5A/edit#gid=1978067583). We added a couple of columns to do Google Map searches: `point map url`, based on the latitude and longitude, if we had them, and `zip map url`, searching Google Maps for the ZIP Code.  We included ZIP Codes which were matched to ZCTAs by geocoding (as above), in case we wanted to spot check any of them, but we were focused on those which had no ZCTA.

For each row, the reviewer would load the point map. If the result was implausible, like many which came up in water, then the reviewer would load the zip code map. 

For plausible maps, the reviewer would right-click on the map to bring up the Google Maps context menu, and choose "What's Here?" If that gave further information that had a ZIP Code, we used it, otherwise we tried "What's Here" for very nearby points on the map until a ZIP Code was found.  

That ZIP Code was placed in the `result` column, which would then generate a link in the `census_reporter_check` column for that row. Clicking on that link would try to open the Census Reporter page for the ZCTA that was entered in the "result" column. If loading the page on Census Reporter errored, that was a sign that the ZIP Code found was not a ZCTA.  

For ZIPs which could not be resolved to ZCTAs, we used a `notes` column to provide more information.

After this process, only three ZIP Codes remained unresolved, and for each, plausible explanations were documented in the ‘notes’ column of the Google Sheets document. In the rebuilt process, documented here, we also turned up two new ZIP Codes from the ZBP data which haven't been manually reviewed.

We're very grateful to Caroline Dudlak, Medill '21, for her human review efforts.


## More info

* [US Census: ZIP Code Tabulation Areas (ZCTAs)](https://www.census.gov/programs-surveys/geography/guidance/geo-areas/zctas.html)
* [What is the difference between ZIP code "boundaries" and ZCTA areas?](http://gis.washington.edu/phurvitz/zip_or_zcta/index.html) by Phil Hurvitz, University of Washington
* [HUD USPS ZIP Code Crosswalk Files](https://www.huduser.gov/portal/datasets/usps_crosswalk.html) — we found this after we created our own, but it looks like this is regularly updated, and ZIP Codes change fairly frequently, so it is probably a better resource than ours. Registration is required, so that is a bit of friction.
* HRSA [ZIP Code to ZCTA Crosswalk](https://data.hrsa.gov/DataDownload/GeoCareNavigator/ZIP%20Code%20to%20ZCTA%20Crosswalk.xlsx) (linked from [Health Center Program GeoCare Navigator](https://geocarenavigator.hrsa.gov/)) — this is a directly downloadable Excel file provided by the US Dept. of Health and Human Services, and it seems to be updated frequently.
* [ZIP Codes by Area and District codes](https://postalpro.usps.com/ZIP_Locale_Detail), provided by the USPS, may be the most authoritative source. This is another we found after we did our work, and this one requires synthesizing data from different worksheets in an Excel file, but for many data users, that will be straightforward.
