# Proposal for Semester Project

<!-- 
Please render a pdf version of this Markdown document with the command below (in your bash terminal) and push this file to Github. 
Please do not Rename this file (Readme.md has a special meaning on GitHub).

quarto render Readme.md --to pdf
-->

**Patterns & Trends in Environmental Data / Computational Movement Analysis / Geo 880**

| Semester:      | FS26                                     |
|:---------------|:---------------------------------------- |
| **Data:**      | GPS Data of cats  |
| **Title:**     | Patterns in Domestic Cat Movement Data                 |
| **Student 1:** | Viktoria Rieder                        |
| **Student 2:** | Anna Kessler                        |

## Abstract 
<!-- (50-60 words) -->

This project studies how domestic cats move using GPS tracking data collected over one month. By analysing trajectories from maximum 92 cats, we want to understand patterns in activity, distances and space at different times of the day, especially comparing daytime and nighttime behavior. We also want to see if cats show regular movement habits and if these habits are similar across different cats. 

## Research Questions
<!-- (50-60 words) -->

- RQ1: How do cat speed and travelled distance vary between different times of the day (e.g. daytime, evening, night)? 
- RQ2: How many trips are cats doing per day/night, and how often do they switch spots for resting? (stops in between movement)
- RQ3: How large is a cat`s home range and how does it differ between cats?
- RQ4: How often do cats meet (e.g. within 10 meters) at a certain density of cats? (density is calculated by number of cats (e.g. 20) divided by the convex hull of all HR)
- Optional RQ5: Which places do cats like to visit often or spend a lot of time there?
- Optional RQ6: How many roads do cats cross and does this change between day and night?


## Results / products
<!-- (50-100 words) -->
<!-- What do you expect, anticipate? -->

We expect the analyses to show temporal patterns in cat movement behavior. In particular, we anticipate that cats will show different speeds and distances depending on the time of day. Cats may be more active during nighttime periods, while daytime movement could be shorter or more localized. (RQ1)

We expect that most cats will make several trips during a day or night cycle, while spending longer periods resting at a limited number of preferred locations. (RQ2)

For the home range analysis, we expect that many cats will have relatively similar sized movement areas, but that some individuals will stand out with much larger ranges and higher activity levels. (RQ3)

Regarding encounters between cats, we expect that direct close-contact situations will occur rarely, especially in areas with lower cat density. Cats may avoid each other spatially or temporally, resulting in only occasional overlaps in their trajectories. (RQ4)


## Data
<!-- (100-150 words) -->
<!-- What data will you use? Will you require additional context data? Where do you get this data from? Do you already have all the data? -->

We will use open source GPS tracking data from 92 domestic cats that is provided on GitHub (https://github.com/richbi/CatTrack_public). The dataset consists of tracking data of 92 cats in the area of Oslo with the coordinates and timestamp provided. 

We do not need to collect new field data, but we may also use additional data for example roads, networks or land-use, to better understand movement patterns, if this research question is considered. 


## Analytical concepts
<!-- (100-200 words) -->
<!-- Which analytical concepts will you use? What conceptual movement spaces and respective modelling approaches of trajectories will you be using? What additional spatial analysis methods will you be using? -->

We will conceptualize the GPS data as individual movement trajectories, consisting of ordered time-stamped point locations for each cat. From these trajectories, we will derive basic movement parameters such as step length, time lag, speed and travelled distance. To investigate temporal movement patterns, the trajectories will be segmented into predefined time periods such as daytime, evening and night. This allows us to compare movement intensity across different phases of the day.

For the analysis of stops and trips, we will apply a simple stop-move model. Stops will be defined as periods where a cat remains within a small spatial radius for a minimum duration, while movements between stops will be interpreted as trips. Home ranges will be estimated for each individual cat using spatial methods such as minimum convex polygons or kernel density estimation. Additionally, potential encounters between cats will be identified based on spatial and temporal proximity, for example when two cats are within 10 meters during a similar time interval. 


## R concepts
<!-- (50-100 words) -->
<!-- Which R concepts, functions, packages will you mainly use. What additional spatial analysis methods will you be using? -->

We will mainly use the tidyverse ecosystem for data preprocessing, filtering, aggregation and visualization of the GPS trajectories. Spatial data handling and coordinate transformations will be performed using the sf package, while movement trajectories and movement metrics such as speed, distance and time lags may be analysed using the methods learnt in class. Home ranges will be calculated using methods such as minimum convex polygons (MCP) or kernel density estimation (KDE). For visualization, we will use ggplot2 and potentially leaflet for interactive maps. Additional spatial analysis methods include proximity analysis between cats and spatial clustering of resting locations.

## Risk analysis
<!-- (100-150 words) -->
<!-- What could be the biggest challenges/problems you might face? What is your plan B? -->

One of the main challenges may be the quality and consistency of the GPS tracking data. GPS errors, missing timestamps or irregular sampling intervals could affect the calculation of speed, travelled distance and stop detection. Another challenge is the definition of concepts such as trips, stops and encounters, since different thresholds may strongly influence the results. A problem might also be the fact, that the used Data was preprocessed, whereby the GPS positions are provided with a spatial offset, to protect the privacy of cat owners. It is not specified how and to what extent the data has been manipulated. This would be specially important when analyzing how often cats cross streets.

As a plan B, we can simplify the project by focusing on fewer research questions or by reducing the complexity of certain analyses. For example, if encounter detection proves too computationally demanding or unreliable, we will instead focus on temporal movement patterns, trip statistics and home range analysis, which are more robust and easier to interpret.


## Questions? 
<!-- (100-150 words) -->
<!-- Which questions would you like to discuss at the coaching session? -->

Main question: Do we have too few / too many research questions or are they below expectations regarding the complexity level?

We still need to decide on which RQ(s) we want to focus. I think we want to focus on day and night differences in speed and distance. We could need some support on deciding what makes sense to explore/research.

We also would like guidance on the following points: 

- Is Convex Hull = Home Range? Or better take KDE (95%) anyways?
- How much ecological importance/relevance must the RQ have?
- How many cats should we use for RQ1?
- We need to decide on the time intervals that are best for comparing night and day movement. Should we do this after trying out different intervals?
- How do we define favorite places (staying long or frequency or both)?  if RQ is considered
- We had another idea for a RQ: Do cats follow the same paths regularly (repeated routes)? – but we don’t really know how we would need to do this. Is this done by measuring the similarity, then decide on which tracks are similar and then count it?
