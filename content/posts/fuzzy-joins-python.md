---
title: "Fuzzy Joins Python"
date: 2020-01-19T05:26:04+01:00
draft: true
---

# Fuzzy Joins in Python

Data wrangling is widely seen as a , with most data scientists spending 50 to 80% of their time cleaning data. I have worked with , but I recently dealt with an exceptional situation. I was working with two independent datasets owned and maintaned by two separate government entities. They shared a "primary key" column. I crossed my fingers,

And poof, 80% of the rows are *gone*. 

Start poking around in the dataframes:


The. I thought there was a shared key. There is not! 

I tried a few different . It was soon obvious that . Fortunately, a few searches later I was poring over documentation for a Python package and learning about the science of Record Linkage. 

## Record Linkage

This approach . Totally unscalable to 

## 

Data scientists report dissatistfaction. I honestly enjoy the work, implementing standards, making reproducible workflows. 

This was not user-submitted.

References:

[Hidden Technical Debt in Machine Learning Systems](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf)

[How much of data wrangling is a data scientist's job?](https://datascience.stackexchange.com/questions/48531/how-much-of-data-wrangling-is-a-data-scientists-job)

[Cleaning Big Data: Most Time-Consuming, Least Enjoyable Data Science Task, Survey Says](https://www.forbes.com/sites/gilpress/2016/03/23/data-preparation-most-time-consuming-least-enjoyable-data-science-task-survey-says/#72ce17c06f63)

[Python Record Linkage Toolkit](https://recordlinkage.readthedocs.io/en/latest/about.html)
[]()
[]()
