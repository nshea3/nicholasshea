---
title: "Well Logs Part3"
date: 2019-11-02T04:24:36+01:00
draft: true
---

# Well Logs Part 3
## Replicating the winning model

I was finally able to adapt , certain parts of the script were pretty opaque and difficult to adapt. 

To start, I walked through their solution. The biggest difference was the use of lags as a feature. THe 

I hypothesize that the optimal lag size is related to the distribution of unit thickness. The feature would then give us information on when the . 
I also see some utility in including the 


**All work done in SEG_Facies_Classification_features.ipynb on Google Colab**

## Size of the units

This is actually trickier than it sounds
The name for this is *run length encoding*. This is built in with Python's itertools functions. 

With my SQL background, I was expecting a very different function, but . This is even acknowledged in the documentation:

*The operation of groupby() is similar to the uniq filter in Unix. It generates a break or new group every time the value of the key function changes (which is why it is usually necessary to have sorted the data using the same key function). That behavior differs from SQL’s GROUP BY which aggregates common elements regardless of their input order.*

Pretty handy to have. 

## Size of units by facies type

Seems to be at least somewhat diagnostic of facies type, unit thickness. The distributions look different.  
This could be a feature that the learner is actually representing internally. Best way to find out is to put it to the test. 
Clearly this feature is pretty solid, now we just need to add it into the 


Obviously we can't use this directly as a feature since this is what we are trying to predict. But we can certainly explore what features related to this we can engineer from the data itself. And we can include data at these lags initially as we 