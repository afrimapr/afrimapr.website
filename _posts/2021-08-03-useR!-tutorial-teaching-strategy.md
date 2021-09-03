---
posttitle:  "afrimapr tutorial at useR!2021: Our teaching strategy"
categories: [useR!2021, teaching]
background: assets/img/blog/posts_20210803b.jpg
author: [Anne Treasure]
---

On 7 July 2021, we ran a 4 hour tutorial at [useR! 2021](https://user2021.r-project.org/) called "Entry level R maps from African data" in both English and French. For further information on participants and our teaching team, please read ‘[afrimapr tutorial at useR! 2021: An overview](https://afrimapr.github.io/afrimapr.website/blog/2021/feedback-from-our-user-tutorial/)’.

The aim was to provide an introduction to mapping and spatial data in R using African data. We expected that most participants would be quite new to creating maps and R, although our pre-course survey showed that we had a rather diverse audience on the day.

The tutorial materials and dataset is available as R project on Github at [https://github.com/afrimapr/useR2021_tutorial](https://github.com/afrimapr/useR2021_tutorial).

## Teaching approach

We adapted our interactive learnr tutorials that form part of the [afrilearnr package](https://afrimapr.github.io/afrilearnr/) to fit a 4-hour workshop. The main aim was to develop confidence in doing the basics really well in preference to straying too far into more advanced analyses and mapping. The tutorial focused on flexible workflows that learners could take away and apply in their own work. We also showed how to spot and avoid common pitfalls as well as how to troubleshoot problems. 

There were separate English and French language groups, each with materials available in the language of their choice (i.e. either French or English). useR! provided a Zoom meeting room for the tutorial. The learners all started together in the main Zoom room for an introductory session and then split into breakout rooms for the separate language sessions. We split the tutorial into three 50 minute slots with two breaks of 15 minutes each. The three teaching sessions covered the following: 
1. Introduction to spatial data; 
2. Reading my spatial data into R; and, 
3. Practical where learners were encouraged to bring their own data to map.

The learning objectives for the tutorial included teaching learners about what spatial data is, and how to: 
- load R packages and data
- create static and interactive maps
- overlay several data types on a map
- work with colour palettes on maps
- read a variety of spatial data file types into R
- use mapview for quick interactive maps, and options for making mapview maps more useful
- make a map from data of the learners’ own choice
- learn where to find help

We also had extra breakout rooms where learners could meet individually with helpers to receive focussed attention if necessary. After the third tutorial session, the groups came back to the main Zoom room for a final wrap-up session.

## Teaching platform

We used [RStudio Cloud](https://rstudio.cloud/) as our teaching platform, which worked very well. We paid for a monthly subscription for the purposes of the tutorial to ensure we had adequate resources and hours. By using RStudio Cloud, we removed the need for participants to have R and RStudio installed on their local computers. We were also able to pre-install all required packages in a base project which was shared with participants. This meant they could start running the code without waiting for (sometimes rather large) packages to be installed and running into difficulties with different versions of R and required packages.

The content was created in .Rmd files, from which HTML documents, containing the full tutorial narrative and code, were generated. The HTML documents could be opened in the RStudio Viewer pane to remove the need for learners to have a second screen to view code and content. We also created separate R script files which only contained the code necessary to run the tutorial (see figures below). 

Additionally tutorial content (including code) was also made available in PDF format for those learners who wanted to print out materials. A table of contents at the beginning of the .Rmd / HTML files meant that students could easily navigate through the tutorial sections in the Viewer pane.

![screen shot of RStudio cloud showing tutorial in English]({{ site.baseurl }}/assets/img/blog/posts_20210803b_1.png)

![screen shot of RStudio cloud showing tutorial in French]({{ site.baseurl }}/assets/img/blog/posts_20210803b_2.png)

The RStudio Cloud project could be downloaded as a zip file facilitating access to the full tutorial and the datasets after the workshop. The R project can also be run locally on learners’ computers if R and RStudio is installed..

All materials are available on GitHub at [https://github.com/afrimapr/useR2021_tutorial](https://github.com/afrimapr/useR2021_tutorial). We have also started to adapt the material for learners and instructors wanting to peruse the tutorials outside the context of useR!2021. The [new GitHub repository](https://github.com/afrimapr/r-maps-tutorial-fr-eng) includes instructions for using the material as learner or instructor.

The tutorial was a great success and we received very positive feedback from the learners. Through this event, we have also grown our afrimapr community with many more people interested in joining our monthly community meetups. If you’d like to learn more about our monthly meetups, [please join the afrimapr Google Group](https://groups.google.com/g/afrimapr/).

