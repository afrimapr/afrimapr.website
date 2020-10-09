---
posttitle: Administrative boundaries - making other data more operationally useful
categories: [admin boundaries]
background: assets/img/posts_20201009.png
author: [Andy South, Anelda van der Walt, Ahmadou Dicko]
---

Administrative boundaries are special data. [Almost by definition](https://en.wikipedia.org/wiki/Administrative_division), local decisions tend to be made with respect to administrative units. Presenting data within administrative units has the potential to make them more relevant to, and understandable by, local decision makers and communities.

That’s a wordy way of describing it. From a more technical mapping viewpoint, administrative boundary data can allow us to : 

- make maps from spreadsheet data with no coordinates
- summarise gridded data to known areas

These are our motivations within afrimapr for making it easier for data analysts to access and use sub-national administrative boundaries for African countries.

Administrative boundaries for countries are available at a series of ‘admin’ levels, starting at admin0 which is the country outline followed by admin1, 2, 3, etc referring to increasingly smaller subdivisions of the country. This use of admin1, 2, 3, etc. helps avoid issues related to  non-standard naming of [sub-national units](https://en.wikipedia.org/wiki/List_of_administrative_divisions_by_country) across countries. For example, Rwanda levels 1 to 4 are called provinces, districts, sectors and cells respectively whereas Benin has three levels called departments, communes and districts. 

Finding the ‘best’ source of administrative boundary data for a particular use-case is not straightforward for the data analyst or even for [companies providing boundary data](https://sovereignlimits.com/blog/mapping-internal-administrative-boundaries-part-1). There are excellent initiatives including the [UN SALB](https://www.unsalb.org/) and [GRID3](https://grid3.org/solution/boundary-harmonisation) working with countries to improve provision of boundaries. These initiatives are necessarily long term. Our focus is on boundaries that are available to data analysts now.   

Boundaries change, which means old data files may have incorrect coordinates, names or numbers of areas. Also boundary data can be available at different resolutions. The highest resolution is not necessarily the best to use for all use-cases. If you want to make a national level map for a publication or website, for example, intricate boundary detail is not needed and may make the map look worse or the website load more slowly.  

The names of administrative units can be an issue too. We have struggled (more than once) to join boundary data to other data when the names of administrative units differ in speling or Cases or accénts. Place names (even when one expects them to be uniform) can differ between data sets sourced from various providers or at different times from the same provider. At admin level 0, Côte d'Ivoire (or Ivory Coast) can be the bête noire of the unsuspecting analyst. We are developing resources to help specifically with joining datasets onto boundary data. We’ll return to that issue in a subsequent post.

In this post we focus on different data sources. We’ve been working on an [R package to facilitate access to admin boundary data for African countries](https://github.com/afrimapr/afriadmin) and an associated [shiny app to visualise admin boundaries](https://andysouth.shinyapps.io/afriadmin-compare/) from different sources.

So far we have concentrated on [GADM](https://gadm.org/) and [geoBoundaries](https://www.geoboundaries.org/). GADM, a database of Global ADMin areas, has been around for over 10 years, has been a great resource and is well used. geoBoundaries is relatively new, launched in 2017 and described in useful detail in this [2020 technical paper](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0231866). geoBoundaries has transparent workflows, more open licensing and open discussion of development plans (e.g. see this discussion of [plans for different versions](https://github.com/wmgeolab/gbRelease/issues/51) to address licensing issues). The [Humanitarian Data Exchange](https://data.humdata.org/search?ext_administrative_divisions=1) (HDX) is another good source of administrative boundaries for humanitarian use, indeed geoBoundaries source some boundaries from here. It is fairly easy for a human to visit the site, search for a country and download boundaries. However, programmatic access to boundaries for a defined country, or the whole continent, is tricky, so we aren't able to include in the app. From recent discussions, we understand that  programmatic data access from HDX is due to improve soon.

The motivation for the [afriadmin package](https://github.com/afrimapr/afriadmin) (in early development) is to ease access to different data sources for users and help them choose which is the best for their needs. afriadmin is relatively simple, mostly just standardising access using existing packages ([rgeoboundaries](https://github.com/wmgeolab/rgeoboundaries) and [raster](https://cran.r-project.org/web/packages/raster/index.html)) targeted at individual data sources.

To get a defined admin level and country :

```r

library(afriadmin)
sftgo <- afriadmin("togo", level=2) 

```
The default datasource is currently geoboundaries, but can be changed when specifying `datasource='gadm'`, and we hope to add other options, such as HDX, as they become available. If you are aware of any other good sources of machine readable boundaries, do let us know. 

To compare different sources :

```r

compareadmin("togo", level=2, datasource=c('geoboundaries','gadm'))`

```
The [afrimapr boundaries comparison app](https://andysouth.shinyapps.io/afriadmin-compare/) runs the code above, allowing you to select a country and look at boundary differences from the two sources.

![Comparing internal boundaries for Liberia using the afriadmin comparison app]({{ site.baseurl }}/assets/img/posts_20201009_1.png)

Toggle geoboundaries & gadm layers on/off via the layers icon top-left of the map panel to see better. The last ticked item will be painted on top which allows changing layer and legend order.

![Toggle boundary layers on/off in afriadmin app]({{ site.baseurl }}/assets/img/posts_20201009_2.png)

The ‘names’ tab in the app allows viewing of admin unit names to anticipate potential data joining issues. Spot the difference here for Liberia. We will cover how such joining issues could be addressed in a following post.

![Comparing names of admin divisions in the afriadmin app]({{ site.baseurl }}/assets/img/posts_20201009_3.png)

In the meantime, if you have any feedback or questions, do [get in touch by any means you wish](https://afrimapr.github.io/afrimapr.website/get-involved/). 
