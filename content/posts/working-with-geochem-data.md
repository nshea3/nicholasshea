---
title: "Working With Gawler Geochem Data"
date: 2020-03-09T19:57:18+01:00
draft: true
---

*This work is part of a submission to Unearthed's [ExploreSA Gawler Challenge](https://unearthed.solutions/u/competitions/exploresa)*

The [ExploreSA Gawler Challenge](https://unearthed.solutions/u/competitions/exploresa) is a competition to predict areas of potential mineralization in the Gawler region of South Australia. In this post I will lay some of the groundwork for a computational approach to this mineral favorability mapping challenge. We'll begin by loading some of the geochemistry data from the [SARIG data package](https://unearthed.solutions/u/competitions/80/data) into Dask and extracting a smaller set of soil geochemistry records. 

Finally, we will interpolate the soil geochemistry records on a grid to create a map across the region, which is a useful input for human interpretation and computational methods alike. 


## Opening the archive

![Imgur](https://i.imgur.com/NGWIB9T.png)

Looking at the downloaded data in the file, one stuck out. Geochemistry anomalies are very important in , so we want to zoom in at 

![Imgur](https://i.imgur.com/is1g4Sx.png)

So it's 11 GB of geochem data, ouch. 

We are pretty solidly in "medium data" territory (following the terminology in [this excellent article](https://medium.com/@jackmaughan_50251/handling-medium-data-with-dask-explore-sa-gawler-challenge-278405ace5)). It is likely not possible to have this file in memory all at once, let alone open it in any text editor. This is where a little familiarity with the command line is extremely useful. 

We can use a Unix program called `head` to look at the first few lines of the file, without opening it all up at once:

![Imgur](https://i.imgur.com/lnoiJfA.png)

Now we know the column labels, and we have a better sense of the structure: every row is a single geochemical test. One location may have multiple rows for multiple different geochemical tests. The measurement unit, measurement value, and *support* are all recorded in the row. 

In geostatistics, a measurement is always associated with an area or volume. Measurements made over different areas or different volumes (*at different supports*) cannot be directly compared or aggregated. It is generally a good idea to only use samples at a single support collected with a single sampling method. 

## Sample Source and Anomaly Type

Soil sampling is a popular method for collecting geochemistry data across a wide area. It is considerably less expensive than drilling and. There is support for . 

Now that we have fixed the sampling method, we need to figure out what kind of geochemical test we'd like to . This is an exploration geochemistry question. Exploration geochemistry is a broad field of scientific research concerned with the application of geochemical theories and techniques to detecting ore deposits. A definition from [General Geology](https://doi.org/10.1007/0-387-30844-X_26):

> *Geochemistry* can be defined as the measurement of the relative and absolute abundance of the elements and isotopes in various parts of the Earth with the object of discovering the principles governing their distribution and migration throughout the geological cycle. *Exploration geochemistry* concentrates particularly on the abundance, distribution, and migration of ore elements, or elements closely associated with ore, with the object of detecting ore deposits. This distinction is only one of emphasis since ores are natural, but not abundant, products of the overall rock-forming cycle.

One of the very popular geochemical exploration strategies is based on the observation that an anomalous abundance of certain elements is indicative of certain types of mineralization. In particular, elevated `Ce` (cerium) and `La` (lanthanum) concentrations are associated with our target mineralization type, IOCG (Iron oxide Copper Gold). 

Another important question that geochemistry can answer: why do we look for cerium and lanthanum anomalies and not iron oxide, copper, or gold anomalies? It's not an immediately obvious answer. IOCG deposits must ALSO have anomalously high grade, but anomalously high grade is not diagnostic of the specific alteration process that produces IOCG deposits. Though there is obviously variation, the specific process creates deposits that are (1) enormous (2) relatively simple to mine and process and (3) relatively high grade. These conditions are very favorable for mining, which is not true of a small, low-grade, refractory orebody. 

## Back to Dask


You can set the `sample` parameter to something very large and it will force 

dd.read_csv('E:/Gawler/Unearthed_5_SARIG_Data_Package/SARIG_Data_Package/sarig_rs_chem_exp.csv',sample=25000000)


There is a . Dask will throw an exception if you don't have the right datatypes . It is good to align your expectations of the datatype with the datatype in order to avoid issues later. 




Sources:

- [Favorability potential for IOCG type deposits in the Riacho do Pontal Belt: new insights for identifying prospects of IOCG-type deposits in NE Brazil](https://doi.org/10.1590/2317-4889201820180029)

- [Signatures of Cu (-Au) mineralisation reflected in inorganic and heavy mineral stream sediments at Vähäkurkkio, north-western Finland](https://doi.org/10.1016/j.gexplo.2018.01.012)

- [Investigation Into the Use of Radon and Soil Sampling in Exploration at the Hillside Copper-Gold Deposit, South Australia](https://www.researchgate.net/profile/Adrian_Fabris/publication/320013992_Investigation_into_the_use_of_radon_and_soil_sampling_in_exploration_at_the_Hillside_Cu-Au_deposit_South_Australia_Hillside_deposit/links/59c86118aca272c71bc7f483/Investigation-into-the-use-of-radon-and-soil-sampling-in-exploration-at-the-Hillside-Cu-Au-deposit-South-Australia-Hillside-deposit.pdf)

- ["Mapping iron oxide Cu-Au (IOCG) mineral potential in Australia using a knowledge-driven mineral systems-based approach"](https://doi.org/10.1016/j.oregeorev.2019.103011)

- ["GEOCHEMICAL FOOTPRINTS OF IOCG DEPOSITS BENEATH THICK COVER: INSIGHTS FROM THE OLYMPIC CU-AU PROVINCE, SOUTH AUSTRALIA"](https://www.researchgate.net/publication/320014326_GEOCHEMICAL_FOOTPRINTS_OF_IOCG_DEPOSITS_BENEATH_THICK_COVER_INSIGHTS_FROM_THE_OLYMPIC_CU-AU_PROVINCE_SOUTH_AUSTRALIA)
