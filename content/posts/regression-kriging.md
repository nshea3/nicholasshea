---
title: "Regression Kriging"
date: 2020-04-09T14:49:25+02:00
draft: true
---



Regression kriging is a hybrid interpolation method combining regression on predictors and a simple kriging of point observations. It's a non-stationary method: here we have done away with the assumption that the expectation of the random variable $E[Z(x)]$ is the same everywhere in the domain.

The proof begins with the expression for kriging with external drift. 

Universal kriging: trend is modeled as a function of the coordinates
Kriging with external drift: Drift defined as function of some auxiliary variables

## Kriging with External Drift 

The most popular example of kriging with external drift is the mapping of a surface in petroleum exploration. Surfaces are typically mapped from seismic images of the subsurface. Some portion of the seismic wave energy reflects as one layer stops and another begins. This is measured at the surface and based on the time, we have a rough idea of where the contact surface is located in the subsurface. Despite very advanced acquisition and processing algorithms, the location is not exact, and the resolution is not very good. However, the coverage is truly vast.
We also typically have drill holes that intercept this surface. With precise depth and survey measurements, we can locally constrain. Of course, we can only constrain the surface at a tiny point in a vast subsurface. 
We'd like to have a way to combine these two sources of data into something that 

It's typically presented this way, but the fact of the matter is 
- multiple drift functions 
- related linearly, slope and intercept 

Move on to building the expression. Our expectation 

<div>
$$\mathrm{E}[Z(\mathbf{x})]=a_{0}+b_{1} s(\mathbf{x})$$
</div>

Predictions are made by kriging, but the covariance matrix of residuals is extended with auxiliary predictors

In regression kriging (or *simple kriging with varying local means*), the drift and residuals are estimated separately. Despite this difference, KED and regression kriging are equivalent. In particular, the predictions and prediction variances will be the same.



<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
  MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    displayMath: [['$$','$$']],
    processEscapes: true,
    processEnvironments: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
    TeX: { equationNumbers: { autoNumber: "AMS" },
         extensions: ["AMSmath.js", "AMSsymbols.js"] }
  }
  });
  MathJax.Hub.Queue(function() {
    // Fix <code> tags after MathJax finishes running. This is a
    // hack to overcome a shortcoming of Markdown. Discussion at
    // https://github.com/mojombo/jekyll/issues/199
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
  });

  MathJax.Hub.Config({
  // Autonumbering by mathjax
  TeX: { equationNumbers: { autoNumber: "AMS" } }
  });
</script>