---
posttitle: Exploring open African health facility data
categories: [health facilities, facility master list, africa]
background: assets/img/blog/posts_20200529.jpg
author: [Anelda van der Walt, Andy South]
---

This blog post is a shorter version of the **[full report](https://rpubs.com/anelda/african-mfls)** that includes R code, readme files, data descriptions and much more. If you are interested in what we've done, we strongly encourage you to head over to the full report and associated [Github repository](https://github.com/anelda/african-open-mfls/). 

## Background
In March 2020 we started working on the [`afrihealthsites` package](http://afrimapr.org/code) to make African health facility data more accessible for analysis, visualisation, and to allow others to combine it more easily with other datasets. [Macharia et al (2020)](https://www.medrxiv.org/content/10.1101/2020.05.27.20113803v1), for example, created vulnerability indices to assist with prioritisation and improved planning specifically with the COVID-19 epidemic, but also beyond this crisis. This kind of data can be overlayed onto health facility data to identify gaps and inform decision-makers if health facility data is readily accessible.

Over the past month the _afrimapr_ team have been looking into health facility data for Africa. In this blog post, we briefly share some highlights of what we found.

## Finding openly available online health facility data

Google searches for open online health facility lists in Africa were performed between 24 April and 8 May 2020. Search terms included “[country name] health facility list”, “[country name] master facility list”, and “[country name] health facility registry”. If the search results did not include an open health facility list for the country in question, we scrutinized the Ministry of Health website for links to a facility list. We also looked for links to a facility list from the country’s health information system (DHIS2) pages if none of the previous strategies lead to an open online facility list. Finally, if the previous strategies were still unsuccessful, we searched for general open data portals for the country in question.

For countries where English is not the primary language, we translated the search terms to either French, Portuguese or Spanish. Despite these efforts there were still a number of cases where we didn’t find health facility lists via this search strategy, but rather by stumbling upon them when searching for something else, or by being referred to specific lists by community members. We realise therefore that the list may not be comprehensive and aim to update it as more open facility lists come to the fore. Our experience indicates that lists can exist for a country even when initial searches fail to find them.

[This interactive map](https://rpubs.com/anelda/health-facility-lists-africa-map) provides an overview of data availability for the continent. By clicking on an individual country, the reader can learn more about data available for that country. A static image of the map is displayed below.

<a href="https://rpubs.com/anelda/health-facility-lists-africa-map"><img src="{{ site.baseurl }}/assets/img/posts_20200529_1.png" alt="Health facility lists in Africa map">


## Evaluating open health facility lists 

Health facility lists vary considerably in terms of the type of facilities included, whether public and/or private sector facilities are listed, and the attributes described. Access to the data also varies greatly, for example, some can be accessed via API, others directly via a download button in a website, and others via request to the Ministry of Health. Lastly, data download formats include PDF, Excel (both .xlsx and .xls), CSV, and Google Sheets. Some datasets are neither downloadable via the web nor the API. 

To get an overview of the similarities and differences between official MFLs available in Africa, we focussed our analysis on health facility lists that were:

- clearly recognised by a country’s Ministry of Health as the official MFL;
- available for download from the MFL database or website; and
- available for download in a format that could be analysed directly in R, therefore including data available in Excel, comma-separated format (CSV), and JavaScript Object Notation (JSON) but excluding data embedded in reports and made available only in PDF format.

Seven African countries’ had open health facility lists that fulfilled the requirements for inclusion in the analysis. These included Kenya, Malawi, Namibia, Rwanda, South-Sudan, Tanzania, and Zambia. We included the KWTRP and healthsites.io datasets in the analysis to get a sense of the differences and similarities that exist between global or continental open datasets and the official MFLS.

The selected datasets were compared by evaluating the number of facilities and attributes described for each facility as well as the type of facilities that were included. The R scripts are available at on [Github](https://github.com/anelda/african_open_mfls/).

### Number of facilities listed

Below we compare the number of facilities from each master facility list to the number of facilities that are available from two open continent-wide health facility registries. The continental datasets are [healthsites.io](https://healthsites.io/) and a resource developed by the [KEMRI-Wellcome Trust Research Programme](https://pubmed.ncbi.nlm.nih.gov/31346183/) now hosted by the World Health Organisation (WHO).

![Number of facilities per dataset]({{ site.baseurl }}/assets/img/blog/posts_20200529_2.png)

### Facility types

To allow for comparison of different facility types that form part of each dataset, the “type” column had to be identified through visual inspection of each dataset as the column names varied considerably between them. Notably the Namibian MFL did not include a column describing the facility type despite the fact that the online MFL database do indeed display facility type. In this [Jupyter Notebook](https://github.com/anelda/african-open-mfls/blob/master/python_notebooks/namibia_mfl_convert.ipynb), we show how the original JSON format was converted to tabular format and a type column was deduced from the data after careful inspection of the MFL.

The [report](https://rpubs.com/anelda/african-mfls) provides great detail about the facility types that are listed in each dataset. Suffice to say here that the lack of a standardised nomenclature makes it quite difficult to compare across datasets and also to combine datasets for a single country.

## Conclusion

A large number of online health facility lists are available for many African countries. The data is currently often not easy to access programatically to include in analysis, modeling, and visualisations. _afrimapr_ is exploring ways to enhance the accessibility of these resources and will continue to share our progress here.  We invite readers to reach out with information about other similar online resources for health facilities and suggestions for functionality that should be included in the open-source R building blocks we are developing.

### Citation

Please cite this work as follows:

_Anelda van der Walt, & Andy South. (2020, June 1). Exploring open African health facility data (Version v1.1). Zenodo. http://doi.org/10.5281/zenodo.3871224._
