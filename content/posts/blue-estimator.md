---
title: "Kriging: BLUE Estimator"
date: 2020-03-04T21:19:47+01:00
draft: true
---

Many discussions about spatial interpolation begin with a few of the more widely understood methods () and end with kriging, driven in some part by an understanding that it has special, optimal properties. What isn't so well understood are what properties make kriging so special and what exactly it optimizes. This is a shame because it's a valuable bit of information, and there are some great resources to . There is even an acronym (BLUE) that summarizes the properties of the kriging estimator: Best, Linear, Unbiased Estimator. 

# L: Linear 

The kriging estimator is part of a class of estimators called *linear* estimators. The value of the estimator $z^{*}(x)$ at any point $x$ is the sum of the known values $z_i$ weighted by $\lambda_i$:

<div>
$$
z^{*}(x)=\sum_{i=1}^{N} \lambda_{i} z_{i} = \lambda_1 z_1 + \lambda_2 z_2 + ... + \lambda_N z_N
$$
</div>

The kriging estimator is a specific *linear* estimator. There are other linear estimators, but they have different weights $\lambda_i$ and they do not have the other special properties. And there are certainly non-linear estimators, but we do not consider them.

# U: Unbiased

The kriging estimator is *unbiased*, meaning that the expected difference between the true value $z(x)$ and the estimated value $z^{*}(x)$ is zero. 

<div>
$$
E\left[z({x})-z^{*}({x})\right]=0
$$
</div>

This means, on average, the estimator will be correct. It is as likely to be high as it is to be low. If we did not make this assumption, the estimator would 

This actually leads to one of the kriging constraints. Since we know that the 


<div>
$$
E\left[z^{*}\right]=\sum_{i=1}^{N} \lambda_{i} E\left[z\left(x_{i}\right)\right]=\sum_{i=1}^{N} \lambda_{i} \bar{z}=\bar{z} \sum_{i=1}^{N} \lambda_{i}
$$
</div>

# 

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