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
<h2 id="Introduction:">Introduction</h2>
The main objective of our project is to answer the question: how does the walkability of a given area correlate with the number of cars people own and how does this relate to the number of low income workers in the area? It would make sense for people in more walkable areas to own fewer cars, and we want to test if that hypothesis is true. We also want to see if areas with more lower income workers are more likely have fewer people with many cars, and if these two hypotheses combine to show that areas with higher walkability are correlated with more lower income workers. 

We aim to answer these hypotheses using the large and comprehensive “Smart Location Database”, a nationwide geographic data resource for measuring location efficiency. The dataset consists of over 90 attributes measuring a wide range of characteristics of each census block of the U.S. Walkability index in this database is calculated based on various measures of the built environment that affect the probability of whether people walk as a mode of transportation. 

<br>

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
    width: 95vw;
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
<br>

