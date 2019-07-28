---
title: "Buffalo Civic Innovation Challenge: Introduction"
date: 2019-05-22T13:12:24-07:00
---

I recently competed in the Buffalo Civic Innovation Eco Challenge. We finished "in the money", earning a prize from ESRI for best use of mapping technology. [The competition was covered in the local paper!](https://buffalonews.com/2019/05/20/cool-buffalo-pair-wins-eco-challenge-competition/)

While it is neat to get my name in the Buffalo News, the writeup did not include any detail on our project. I built a web application, [Lead Free Buffalo](https://leadfreebflo.com), that has some useful information on lead contamination of drinking water and a couple visualizations of some lead testing performed across the city. I also built and deployed a ML model that responds to prediction requests from a webform on the page, using several publicly available data to assess the lead contamination risk at an address supplied by the user. 

I'll be breaking this into a couple of posts, covering each of the stages of the investigation. I will say that I underestimated the amount of time it would take to assemble the dataset, so I was not able to do much hyperparameter tuning or validation of the model originally, but I will address that shortcoming as I present the results. 

### Inspiration and Data

The City ran a brainstorming session in the first few weeks of the competition. I noticed that lead contamination was mentioned a lot in the transcripts. It's clearly a top concern for residents in the aftermath of the Flint crisis. I immediately wondered if there was a dataset I could use for an ML approach to the problem of mapping lead service lines. I found [one dataset from Buffalo](https://investigativepost.carto.com/tables/buffalo_lead/public), with [some excellent analysis, visualization, and storytelling](http://interactive.investigativepost.org/lead-buffalo-2016/) in an accompanying article by Dan Tevlock, an investigative reporter with the Investigative Post. 

### Next steps

Over the next couple posts I will walk through my approach to data scraping and cleaning, preliminary visualization and learning, and then present my results. I'll also make an attempt to analyze the spatial distribution of the data using geostatistics. 