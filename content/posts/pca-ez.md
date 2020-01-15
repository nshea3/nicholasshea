---
title: "PCA the Easy Way?"
date: 2019-12-16T18:59:19+01:00
draft: true
---

### Introduction

I am (re) learning PCA for probably the fourth time. I first saw PCA in an undergraduate Applied Linear Algebra course. I had not taken a serious statistics course yet, so the idea of a covariance matrix was not very clear. Like many of the other applications I saw in that class, the how of PCA was very clear, but not the why. 

The second time would have come during my graduate Machine Learning course in Georgia Tech's OMSCS program. The focus was somewhat different as it was not  I had an excellent intution for the dimensionality reduction . After that, I used PCA for denoising and signal separation of TEM data in a geophysics field study [(source)](https://pdfs.semanticscholar.org/71c0/44b3dafba2d12826cbed9fe473a161c42c49.pdf). 

This time, I'm learning PCA for noise reduction in multispectral imaging. I have learned noise reduction algorithms, either in computer vision, or frequency-domain, or ICA. PCA is versatile and omnipresent and I believe it is time I developed a better understanding of the algorithm as a whole. And at the end of the day, it never hurts to know more linear algebra *(though learning it might cause a headache or two)*

### Intuition 

This is much of what I learned . My argument borrows heavily from a few different sources .

![Data projections along vectors](https://i.imgur.com/BPpYs9K.gif)



### Worked Example 

### Application: Handwriting 

### Application: 

### How does it remove noise though? 

This one was admittedly not clear. Why would noise be concentrated in the lower components (not the principal components). Wouldn't noise be 

We are looking at COVARIANCE, not VARIANCE (though we are also sorta looking at variance?)

*It's an assumption of the process that the noise components have lower variance than the signal*. In some cases, noise components can have higher variance than the data and in this case principal components will fail to give an intuitive order of image quality [(Source)](http://www2.compute.dtu.dk/pubdb/views/edoc_download.php/209/pdf/imm209.pdf)

"Use of principal component analysis in the de-noising and signal separation of transient electromagnetic data"

"For example, incoherent
noise often populates the last few principal components and discarding them during reconstruction would
yield a cleaner signal"
"This result is derived from the fact that PCA measures correlated energy. If a
signal is random from trace to trace then there is very little correlated energy between the signals, so the
reconstruction of those signals falls to the later components. "


"The strength in PCA, however, comes not only from the removal of uncorrelated noise, but also from
correlated signals that contaminate the desired signal. If signals recorded from different sources contain
different characteristics (i.e. unexploded ordnance and geology), PCA is able to separate them into specific
components. More importantly, only the signals due to the desired source can be reconstructed by choosing
the appropriate principal components. "

### Drawbacks of the Algorithm



<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
