# Towards a Generalized Tool for Aggregating ACS Data for non-Census Geographies

A common problem for journalists and other analysts is wishing that the Census Bureau tabulated American Community Survey (ACS) data for locally meaningful geographies, such as neighborhoods, wards, or police districts. 

The [jupyter notebook](notebook.ipynb) in this directory provides working python code which does this, and demonstrates its use to create datasets of ACS estimates for Chicago Police districts.  An obvious next step would be to factor the code out of a notebook into a reusable library.  

It would be even more convenient to provide this as a web-hosted service, but we have some concerns about the system resources to support whatever requests people might bring. But it's still something to consider.


## Method

Without access to individual Census responses, the only way to obtain Census data for custom geographies is to map Census geographies to your custom geographies and add up the figures. This is relatively straightforward, unless the Census geographies are split between two or more custom geographies. 

While census blocks vary in size, [more than half of them are smaller than 0.1 sq. miles](http://proximityone.com/geo_blocks.htm). Smaller census blocks are less likely to cross boundaries of custom geographies, and since they also, generally, have smaller populations, the inaccuracy introduced by treating them as they are not split is usually tolerable.

However, block-level data is only provided for the Decennial Census. The ACS, which is released every year, and which also includes many topics not covered by the Decennial Census, uses the *block group* as its smallest geography. While small, block groups still contain dozens of blocks or more, increasing the likelihood of distorting the data if block groups are simply assigned to a single custom geography when they are, in reality, split between two or more. 

To address this issue, when a block group is split, we allocate its data to each segment segment in proportion to the population of that segment, based on the block-level population of the most recent Decennial Census. (For certain data, using the block-level housing unit count is more appropriate.)

It's actually still an open question as to whether it would be better to use block groups or tracts as the building block of aggregate data. Block groups, being smaller, might seem to provide closer alignment. However, because the ACS is a survey, smaller geographies tend to have larger margins of error, especially for small sub-populations. ACS census tract level data may reduce some of that uncertainty.  For now, this library supports using either.


## Status

Currently, there's a [Jupyter notebook](https://github.com/censusreporter/acs-aggregate/blob/master/notebook.ipynb) which explains the origin of the project and demonstrates the basic method. If you have a "block assignment" file, you can use it now to pull ACS data for your custom geographies.

Next steps:

* Package the code in the notebook into a library
* Make it easier to create a "block assignment file"
* Address the caveats below

### Caveats and limitations

* Right now, margin of error is simply disregarded. It would not be too hard to aggregate the margin of error as part of the process, but it sort of clutters up things by doubling the number of columns. At some point, I think I'd like to add an option to include aggregated MOE.

* The library is not equipped to aggregate median values such as "median household income". Folks at the LA Times have [done work in this area](https://github.com/datadesk/census-data-aggregator#approximating-medians) but applying it requires a slightly different API than the library currently uses. It's something I'd like to work on, though.

* The library is not equipped to aggregate percent values. The ACS Subject tables and Data Profile tables have a mix of "total" and "percent" variables. It's probably possible to aggregate percentages, but I'm not clear on the method.

* Making a block assignment file is a lot of work, if not just out-of-reach, for most people. In a project which re-ignited this one, [John Keefe reported out cases](https://johnkeefe.net/chicago-race-and-ethnicity-data-by-police-district) where blocks themselves were split by custom geographies. Other approaches simply assign blocks to whatever custom geography contains their centroid, which should be automatable. A near-term future goal is to support creating the block assignment files using centroid-assignments. I'd imagined trying to make a web-tool to help with the review/assignment, but I'm not sure it's worth the considerable effort, especially for ACS data, which is always imprecise by its survey nature.

