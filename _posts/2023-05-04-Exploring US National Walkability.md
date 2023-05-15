---
title: Exploring U.S National Wakability With Tableau
categories:
- Visualizations
excerpt: |
  Here we explore how the different walkability ratings of many places in the U.S with some visuals
feature_text: |
  ## Exploring U.S National Walkability Index
  Made with Tableau
feature_image: "https://picsum.photos/2560/600?image=733"
image: "https://picsum.photos/2560/600?image=733"
---
<h2 id="Introduction">Introduction</h2>
The main objective of our project is to answer the question: how does the walkability of a given area correlate with the number of cars people own and how does this relate to the number of low income workers in the area? It would make sense for people in more walkable areas to own fewer cars, and we want to test if that hypothesis is true. We also want to see if areas with more lower income workers are more likely have fewer people with many cars, and if these two hypotheses combine to show that areas with higher walkability are correlated with more lower income workers. 

We aim to answer these hypotheses using the large and comprehensive [“Smart Location Database”](https://www.epa.gov/smartgrowth/smart-location-mapping#SLD), a nationwide geographic data resource for measuring location efficiency. The dataset consists of [over 90 attributes](https://www.epa.gov/sites/default/files/2021-06/documents/epa_sld_3.0_technicaldocumentationuserguide_may2021.pdf) measuring a wide range of characteristics of each census block of the U.S. [Walkability index](https://www.epa.gov/sites/default/files/2021-06/documents/national_walkability_index_methodology_and_user_guide_june2021.pdf) in this database is calculated based on various measures of the built environment that affect the probability of whether people walk as a mode of transportation. 


<h2 id="Visualization Guide">Visualization Guide</h2>
The first Visualization on the left shows the average walkability aggregated by state. The tooltip when you hover over a state lists the walkability, average percentage of people in the state with two or more cars, average percentage of low wage workers in the state, and the sum total population in the CBSA groups<sup id="fnref:1"><a href="#fn:1" rel="footnote">1</a></sup> in which data was collected for that state. The top right Visualization shows the walkability by census CBSA block group, the smallest geographic area by which data was collected. The state data is the aggregation of the groups shown in this Visualization. The final Visualization on the bottom right is a bubble plot which compares walkability to the percentage of people who own two or more cars. The bubble size is dictated by total population, and the bubble color indicates the percentage of low wage workers. Each bubble is a CBSA group, and the plot can be filtered by state by clicking on the states in the first visualization. 



<div class="footnotes">
<hr>
<ol>
<li id="fn:1">CBSA stands for "<a href="https://en.wikipedia.org/wiki/Core-based_statistical_area">core-based statistical area</a>", which consists of one or more counties anchored by an urban center of at least 10,000 people plus adjacent counties that are socioeconomically tied to the urban center by commuting. <a href="#fnref:1" rev="footnote">↩</a></li>
</ol>
</div>


<style>
  .tableau-center {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
    height: 1000px;
    position: relative;
    left: 50%;
    right: 50%;
    margin-left: -50vw;
    margin-right: -50vw;
  }

  .tableau-container {
    width: 90vw;
    height: 1000px;
  }
</style>

<div class="tableau-center">
  <div class="tableau-container">
    <script type="module" src="https://public.tableau.com/javascripts/api/tableau.embedding.3.latest.js"></script>
    <tableau-viz id="tableauViz" src="https://public.tableau.com/views/WalkabilityAndNumberOfCars_16831713836970/ExploringWalkabilityIndexIntheU_S?:language=en-US&:display_count=n&:origin=viz_share_link"  toolbar="bottom" hide-tabs></tableau-viz>
  </div>
</div>
<br>

<h2 id="Conclusions">Conclusions</h2>
The bubble plot tests our hypotheses. In it we can see, there are more orange CBSAs, which have a larger than median percentage of low wage workers, in higher walkability areas. This fits with our hypothesis that low wage workers will be more present in walkable areas. We can also see more walkable areas have more variety of the percentage of people with multiple cars. There are still many CBSAs with high percentages of people with 2 or more cars, but overall they are more likely to have fewer cars than CBSAs with low walkability. The maps allow us to see general trends in walkability across the country, and to filter the bubble plot so we can see how it breaks down by state. These are general trends. In Virginia specifically these patterns are not strong. There are more blue CBSAs at lower walkabilities, and orange at high walkabilities, but it is not overwhelmingly split into blue and orange sections. 

<br>
<h2 id="Helpful Links">Helpful Links</h2>
[Download the data used](https://edg.epa.gov/metadata/catalog/search/resource/details.page?uuid=%7B251AFDD9-23A7-4068-9B27-A3048A7E6012%7D) in our visualizations: This is the link to download the data we used for your own use.
<br>
<br>
[Methodology Link](https://www.epa.gov/sites/default/files/2021-06/documents/national_walkability_index_methodology_and_user_guide_june2021.pdf): This is a document about what walkability means practically. It also details how the walkability measure came about and what algorithm is used to calculate it.
<br>
<br>
[Documentation Link](https://www.epa.gov/sites/default/files/2021-06/documents/epa_sld_3.0_technicaldocumentationuserguide_may2021.pdf): This is the technical documentation for the smart location database, where the data is from. It includes a list of variable names and their meanings in this dataset on page 6. 

<br>
<br>
<h2 id="Citations">Source Citations</h2>

[Environmental Protection Agency. (n.d.). EPA](https://www.epa.gov/sites/default/files/2021-06/documents/epa_sld_3.0_technicaldocumentationuserguide_may2021.pdf) Retrieved May 4, 2023

<br>
