---
posttitle: Merging Open Health Facility Data Sets - Part 1
categories: [health facilities, facility master list, africa]
background: assets/img/posts_20200416.png
author: [Anelda van der Walt, Andy South]
---

This blog post is a shorter version of the **[full report](https://htmlpreview.github.io/?https://github.com/anelda/merge_open_hospital_data/blob/master/reports/merge_open_hospital_data_part1.html)** that includes R code, readme files, data descriptions and much more. If you are really interested in what we've done, we strongly encourage you to head over to the full report and associated [Github repository](https://github.com/anelda/merge_open_hospital_data/). 

# Background

## `afrimapr` and `afrihealthsites`

Early in March 2020 the [_afrimapr_ team](http://afrimapr.org) started looking into mapping, comparing, and combining open health facility data sets to enable better access for decision makers in Africa during and after the COVID-19 pandemic. The [`afrihealthsites` package](http://afrimapr.org/code) currently allows one to compare two existing continental open data sets - one developed by the Kenya Medical Research Institute (KEMRI) in collaboration with the WHO, the second a global crowd sourced open health facilities mapping project - [healthsites.io](https://healthsites.io). `afrihealthsites` is under active development and we aim to get it out to potential users very early in the development cycle to allow for continuous input that can shape its functionality.

## South Africa: A case study

In South Africa the [Data Science for Social Impact](https://dsfsi.github.io/) group created an open [COVID-19 dataset and dashboard](https://arxiv.org/abs/2004.04813) to assist with local efforts. The group recruited volunteers to assist with the the collation of information about hospital resources in South Africa and I thought this was a great practical use-case for the kind of tools we had in mind to build within _afrimapr_. For more information about the challenges associated with building a comprehensive list of health facilities for South Africa see [this Github issue](https://github.com/dsfsi/covid19za/issues/115). During our conversations about developing a list of hospitals with various attributes such as address, website, contact details, services available, and corona-readiness, we realised this wasn't going to be a trivial exercise.

## Master Facility Lists

These challenges are experienced in every country when health facility lists from various stakeholders are combined to create, what is called, a Master Facility List (MFL). According to the [Master Facility List (MFL) Resource Pack](https://www.who.int/healthinfo/MFL_Resource_Package_Jan2018.pdf?ua=1) developed in 2018 by the WHO/USAID, the MFL is a complete, up-to-date, authoritative listing of the health facilities in a particular country. The article by [Maina et al (2019)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6658526/) describes their experience in collating a MFL for Kenya and subsequently assisting other countries to develop in-house MFLs and finally the continental health facility list.

A MFL typically contains information about health facilities including:

- data to accurately identify a facility (e.g. name, unique identifier, location, contact information);
- administrative data (e.g. facility type, ownership, operational status) and
- information about the service capacity (e.g. types of services offered, number of beds).

According to the WHO, a MFL should be updated regularly (at least every two years), should be verified, and must be accessible to stakeholders. The [Master Facility List (MFL) Resource Pack](https://www.who.int/healthinfo/MFL_Resource_Package_Jan2018.pdf?ua=1) provides further guidance on the development or strengthening of a Master Facility List. 

Countries can benefit tremendously from having a high quality, up-to-date MFL in the following ways:

- it can create efficiencies by having to maintain a single list rather than maintaining several lists and continuously facing the challenge of integration;
- it facilitates information exchange across different health data systems;
- it provides metadata needed by other information systems;
- it can facilitate planning and management and
- it can support case management of patients.

A quick Google search lead to openly available MFLs for at least the following African countries:

- [Malawi](https://github.com/BaobabHealthTrust/master-facility-list)
- [Kenya](http://kmhfl.health.go.ke/#/home)
- [Namibia](https://mfl.mhss.gov.na/)
- [Nigeria](https://hfr.health.gov.ng/download/facilities)
- [Tanzania](http://hfrportal.moh.go.tz/)
- [Uganda](https://health.go.ug/sites/default/files/Signed%20n%20final%20mfl.pdf) - in PDF format

# Creating a master table which will be populated from the various datasets

The ultimate aim of this project is to work through the process of collating the best possible facility list for South Africa by combining various openly available resources. We acknowledge that this cannot be called the Master Facility List as we will only work with openly available data sets and do not have access to all information available to the Department of Health (beyond what is published in the Data Dictionary). We want to understand the process and see where [_afrimapr_](http://afrimapr.org) can aid by developing building blocks to facilitate similar processes and complimentary data analysis workflows. 

# Collecting open hospital data sets from the Web

A wide variety of health facility web portals and data sets are available online. Some access points do not allow for data download, for example the Department of Health's [Primary Health Care Facilities and Services](https://www.healthestablishments.org.za/Home/Facility) page. Wikidata, the central storage for structured data of its Wikimedia sister projects, hosts a project named [Medicine/Hospitals by country/South Africa](https://www.wikidata.org/wiki/Wikidata:WikiProject_Medicine/Hospitals_by_country/South_Africa) which includes 208 facilities. Unfortunately the data for each facility is very sparsely populated.

The [District Health Barometer report data for 2017/2018](https://www.hst.org.za/publications/Pages/DHB20172018.aspx) was not considered for further analysis due to the inaccessible formatting of the tables in the spreadsheet.

[Medpages](https://www.medpages.info/sf/index.php?page=homepage), a private company, claims to be "the largest, most accurate, most up to date and most complete healthcare database available for Africa". Their data is not available for download except with express written consent (and at a fee) as they operate on a subscription basis. At the time of writing this report Medpages had contact information for 188,024 health organisations and 239,931 healthcare professionals (and counting as this is an actively managed database).

[South African Doctors](http://doctors-hospitals-medical-cape-town-south-africa.blaauwberg.net) is an online resource maintained by a private individual. The data is not available for download.

The following potentially useful sources with downloadable data were identified:

- Research article - [Geographical maldistribution of surgical resources in South Africa: A review of the number of hospitals, hospital beds and surgical beds](http://www.samj.org.za/index.php/samj/article/view/12143)[Figshare](https://figshare.com/articles/SURGICAL_RESOURCES_latestmarch2016_xlsx/12066711) 
- Report - [Department of Health District Health Barometer 2016/2017](http://www.health.gov.za/index.php/2014-03-17-09-09-38/reports/category/424-reports-2017#) 
- Report - [Department of Health District Health Barometer 2018/2019](https://www.hst.org.za/publications/Pages/DISTRICT-HEALTH-BAROMETER-201819.aspx)
- Data Dictionary - [Department of Health Data Dictionary](https://dd.dhmis.org/orgunits.html?file=NIDS%20Integrated&source=nids&ver=91b9) 
- Data Commons - [healthsites.io](https://healthsites.io/)
- Research article - [KEMRI/WHO: A spatial database of health facilities managed by the public health sector in sub-Saharan Africa](https://dx.doi.org/10.1038%2Fs41597-019-0142-2)

# Putting it all together

In the interest of keeping this blog post at a reasonable length, we won't go into details of the challenges encountered in trying to merge the health facility data sets.

Suffice to say that the process is not trivial and is in fact tremendously error prone if done by hand. 

Below you can see how vastly the datasets differ in terms of the number of facilities that are included.

![Number of health facilities listed in each dataset]({{ site.baseurl }}/assets/img/posts_20200416-1.png)

The various datasets also differ remarkably in terms of the types of health facilities that are listed.

![The frequency of various types of health facilities listed in each dataset]({{ site.baseurl }}/assets/img/posts_20200416-2.png)

The [full report](https://htmlpreview.github.io/?https://github.com/anelda/merge_open_hospital_data/blob/master/reports/merge_open_hospital_data_part1.html) and underlying [R code](https://github.com/anelda/merge_open_hospital_data/blob/master/reports/merge_open_hospital_data_part1.Rmd) describe the steps we've taken so far, including:

- converting weirdly formatted Excel tables to CSV files
- renaming column headers
- converting admin level contents to something that is comparable
- extracting coordinates into latitude and longitude
- extracting only useful columns
- creating a 'master' table
- fixing (some) typos
- cleaning up (some) capitalisation
- using reverse geocoding where coordinates was available but not addresses and admin level 2 - 4 info
- much more...

The next blog post (and report) in this series will continue the analysis and aim to find a way to merge the cleaned-up facility information.

In the meantime this work has inspired further development of methods in the [`afrihealthsites`](http://www.afrimapr.org/code) package that can support this process. _Watch this space for updates on new functionality!_

## Citation

Please cite this work as follows:

Anelda van der Walt, & Andy South. (2020, April 16). Merging Open Health Facility Data Sets: Part 1 (Version v1.1). Zenodo. http://doi.org/10.5281/zenodo.3754647