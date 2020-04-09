---
title: "Fuzzy Joins Python"
date: 2020-01-19T05:26:04+01:00
draft: true
---

# Fuzzy Joins in Python

Data wrangling is widely seen as a , with most data scientists spending 50 to 80% of their time cleaning data. I have worked with , but I recently dealt with an exceptional situation. I was working with two independent datasets owned and maintaned by two separate government entities. They shared a "key" column, with the same column name in both CSVs and even the same description in the , so I thought . I crossed my fingers, ran [`pandas.DataFrame.merge`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html) and waited for the cell to execute. A few seconds passed, the cell finished executing. I took a quick look at the dataframe, filtering out NULLs to , 

and poof, 80% of the rows are *gone*. 

# When the Foreign Key is less Key and more Foreign 

The. I thought there was a shared key. There is not! 

I tried a few different heuristics and . It was soon obvious that I would need a . Fortunately, a few searches later I was poring over documentation for a Python package and learning about the science of Record Linkage. 

## Record Linkage

Here, I was trying to reduce the number of matches that are made, working under the hypothesis that the memory savings would be sufficient to . I was looking in the right direction, but 

This is called *blocking* in record linkage problems, and it is easy to accomplish in `recordlinkage`. 

```python
import recordlinkage

indexer = recordlinkage.Index()

indexer.block('zipcode')

candidate_links = indexer.index(dfA, dfB)
```

Here we are blocking on zipcode, since it turned out that the zip codes were stored in a common format. 

## 

Data scientists report dissatistfaction. I honestly enjoy the work, implementing standards, making reproducible workflows. 

This was not user-submitted.


## Pitfalls

There are still limitations 

Things can get big quickly when you consider the cross join. This will result in out of memory errors, CPU hammering 


References:

[Hidden Technical Debt in Machine Learning Systems](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf)

[How much of data wrangling is a data scientist's job?](https://datascience.stackexchange.com/questions/48531/how-much-of-data-wrangling-is-a-data-scientists-job)

[Cleaning Big Data: Most Time-Consuming, Least Enjoyable Data Science Task, Survey Says](https://www.forbes.com/sites/gilpress/2016/03/23/data-preparation-most-time-consuming-least-enjoyable-data-science-task-survey-says/#72ce17c06f63)

[Python Record Linkage Toolkit](https://recordlinkage.readthedocs.io/en/latest/about.html)

[DEDUPE.IO](https://docs.dedupe.io/en/latest/API-documentation.html)
[]()
