 # acs-aggregate

Tools to help aggregate American Community Survey data to non-Census ("custom") geographies.

A common problem for journalists and other analysts is wishing that the Census Bureau tabulated American Community Survey (ACS) data for locally meaningful geographies, such as neighborhoods, wards, or police districts. This project aims to make that as easy as possible, while acknowledging that there are some wrinkles.

* See the `crosswalks` directory for crosswalks for specific geography types.
* See `generalized` for examples of a general method (with a worked example). 
* see BOUNDARIES.md for a randomly assembled list of available GIS data which might be the kinds of things for which people would want to use this.

The longer term goal is to make this as automated as possible, but we're still getting a sense of the problem. We welcome discussion, or even just expressions of interest and votes of confidence.

To read: [Target‐Density Weighting Interpolation and Uncertainty Evaluation for Temporal Analysis of Census Data](https://onlinelibrary.wiley.com/doi/full/10.1111/j.1538-4632.2007.00706.x), which may provide insights on whether these methods are well-designed.

