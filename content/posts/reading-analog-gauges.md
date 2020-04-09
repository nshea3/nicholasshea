---
title: "Reading Analog Gauges"
date: 2020-03-02T23:30:01+01:00
draft: true
---

![Imgur](https://i.imgur.com/WX1fnuX.png)

Reading clock faces is an interesting problem because it is exactly the sort of problem that is sort of trivial, but might be very challenging to explicitly program. I did not realize there was a compelling business case until I read [an article](https://pubs.spe.org/en/jpt/jpt-article-detail/?art=6417) in the Journal of Petroleum Technology about an effort to digitize an offshore rig by automating data collection from . Elsewhere in industry, analog gauges , putting employees in ha

It is also a good problem precisely because it is so well studied with traditional computer vision techniques. 

## Computer Vision Approach

The classical computer vision approach is described in [this paper](https://www.cs.bgu.ac.il/~ben-shahar/Teaching/Computational-Vision/StudentProjects/ICBV151/ICBV-2015-1-ChemiShumacher/Report.pdf) and [this paper](https://software.intel.com/en-us/articles/analog-gauge-reader-using-opencv) and others. 

The steps are laid out clearly in "Analog clock and watch reader":

- Isolate the clock from the rest of the image
- Apply edge detection to the image
- Use Hough transform to isolate watch hands
- Calculate line angles
- Filter out irrelevant lines
- Compute the time


Sources:

[Artificial Intelligence Transforms Offshore Analog Fields Into Digital Fields](https://pubs.spe.org/en/jpt/jpt-article-detail/?art=6417)
[Deep gauge (using Tensorflow to read gauges)](https://github.com/oci-labs/deep-gauge)
[Analog Gauge Reader Using OpenCV in Python](https://software.intel.com/en-us/articles/analog-gauge-reader-using-opencv)
[Reading a value of a real gauge](https://ai.stackexchange.com/questions/4415/reading-a-value-of-a-real-gauge)
[Looking for ideas to read gauge meter values](https://www.reddit.com/r/MachineLearning/comments/8odtnt/d_looking_for_ideas_to_read_gauge_meter_values/)
[Analog clock and watch reader](https://www.cs.bgu.ac.il/~ben-shahar/Teaching/Computational-Vision/StudentProjects/ICBV151/ICBV-2015-1-ChemiShumacher/Report.pdf)
[MACHINE LEARNING IN PRACTICE: USING ARTIFICIAL INTELLIGENCE TO READ ANALOG GAUGES](https://objectcomputing.com/resources/publications/sett/june-2019-using-machine-learning-to-read-analog-gauges)
[MLClock](https://github.com/KittyMac/MLClock)
