---
posttitle: Open health facility location data for Africa to support COVID-19 efforts
categories: [health facilities, africa, covid-19, coronavirus]
background: assets/img/blog/posts_20200326-b.png 
author: [Andy South, Anelda van der Walt]
---

We aim to improve access to the best-available health facility data for Africa to support the response to the coronavirus pandemic.  

This is a part of _afrimapr_, a one year project running in 2020, funded by the [Wellcome Open Research Fund](https://wellcome.ac.uk/funding/people-and-projects/grants-awarded/afrimapr-facilitating-use-spatial-data-african-public) to make health data more useable in Africa.

The _afrimapr_ approach is to create building-blocks in [R](https://www.r-project.org/) that will make it easier for others to create data-driven tools and apps. We are now applying that approach to help address the pandemic.

## Inspiration from the USA

We are inspired by efforts in the US where an open data set of the location and bed numbers of [all US hospitals](https://coronavirus-resources.esri.com/datasets/definitivehc::definitive-healthcare-usa-hospital-beds) has been made available (around 6.5k locations). These open data are already being used, for example in [COVID Care Map](https://www.covidcaremap.org/), an open source project to support health system capacity.   

## Health facility open-data in Africa

There seem to be two main existing open datasets for health facility locations across African countries.

In 2019 the Population Health Research Unit at KEMRI-Wellcome released
[a spatial database of health facilities managed by the public health sector in sub-Saharan Africa](https://www.nature.com/articles/s41597-019-0142-2). The article and an [accompanying piece](https://researchdata.springernature.com/users/269086-joseph-maina/posts/51542-the-first-step-towards-global-high-resolution-geographic-analysis-of-health-facility-access) describe the lengthy effort and difficulties in producing a continental level dataset. They outline how the dataset is now curated by the [WHO Global Malaria Program](https://www.who.int/malaria/areas/surveillance/public-sector-health-facilities-ss-africa/en/) with plans to refine and update.

The second dataset can be obtained from the global project - [healthsites.io](https://healthsites.io/) “an initiative to create an online map of every health facility in the world and make the details of each location easily accessible”. This excellent global health facility mapping project, associated with OpenStreetMap, has lots of resources for collaboration. Data are obtained both from bulk imports and crowdsourced contributions. [Anyone can contribute](https://healthsites.io/map) locations and attribute data for individual sites by first creating an OpenStreetMap account. The project has a clear vision and roadmap for how location coverage and accuracy will be [improved over time](https://github.com/healthsites/healthsites/wiki/Healthsites-roadmap). 

There is variable overlap between these two sources. Some coordinates in the WHO-KEMRI data were sourced from healthsites.io and some of the WHO-KEMRI data have subsequently been used to update healthsites.io

## How are we responding

Last week we created an R package [afrihealthsites](https://github.com/afrimapr/afrihealthsites) that makes it easier to access and compare health facility data for Africa from these two sources (and potentially others in future). This currently contains around 96k locations from the WHO-KEMRI dataset and 57k locations from healthsites.io. This week we created a relatively simple [healthsites viewer](https://andysouth.shinyapps.io/healthsites_viewer/) that allows anyone to choose a country and view the locations of different health facility categories from the two datasets. 

This is the first effort we are aware of to compare these two, potentially complementary, datasets. Using the viewer we can see e.g. for Angola that there appear to be many more sites from the WHO-KEMRI data (shown by the smaller blue-purple circles) than healthsites.io (shown by the larger yellow-green circles).

![]({{ site.baseurl }}/assets/img/blog/posts_20200326_1.png)

In contrast, zooming in on the capital, Luanda, in the north-east shows more records from healthsites.io. 

![]({{ site.baseurl }}/assets/img/blog/posts_20200326_2.png)

These differences may partly reflect the different categories of health facilities. In healthsites.io, sites across all countries are categorised as hospital, clinic, doctors, pharmacy and dentist (you can filter which ones you want to display using the tick boxes on the left). In the WHO-KEMRI data, categories are kept from national source data so there are different categories for each country (giving 172 categories across the whole continent). Also the WHO-KEMRI data are restricted to public facilities where healthsites.io can include private.   

For Burundi the situation seems to be different, there is much greater overlap between the two datasets.

![]({{ site.baseurl }}/assets/img/blog/posts_20200326_3.png)

This can be confirmed by turning off the healthsites layer :

![]({{ site.baseurl }}/assets/img/blog/posts_20200326_4.png)

## Where are we headed

We are really just starting out with this investigation, we have only covered the first two countries alphabetically in this blog post! We welcome input, particularly on other potential data sources or how it would be useful for us to improve these tools. We are conscious that we are new to this and that others are likely to know more.

We have lots of things that we are considering doing, for example checking whether there are other, more recent or comprehensive data sources maybe from national ministries of health.

## How can you help

We would love others to [get involved](https://afrimapr.github.io/afrimapr.website/get-involved/). We are keen to use our digital skills to create something that will be useful for the COVID-19 response and beyond.


