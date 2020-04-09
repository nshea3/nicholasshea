---
title: "Kriging: BLUE Estimator"
date: 2020-03-04T21:19:47+01:00
draft: true
---

Many discussions about spatial interpolation begin with a few of the more widely understood methods (nearest neighbor, inverse distance weighting, splines) and end with kriging, driven that way by an understanding that kriging has special, optimal properties. What isn't so well understood are the exact properties that make kriging so special. What exactly does kriging optimize? This is a shame because it's a valuable piece of information for anyone who uses kriging, and there are some great resources that explain it very well. 

There is even an easy acronym that summarizes the special properties: **BLUE**. **B**est, **L**inear, **U**nbiased **E**stimator. 

# L: Linear 

The kriging estimator is part of a class of estimators called *linear* estimators. The value of the estimator $z^{*}(x)$ at any point $x$ is the sum of the known values $z_i$ weighted by $\lambda_i$ (or, a linear combination of the $z_i$):

<div>
$$
z^{*}(x)=\sum_{i=1}^{N} \lambda_{i} z_{i} = \lambda_1 z_1 + \lambda_2 z_2 + ... + \lambda_N z_N
$$
</div>

The kriging estimator is a specific *linear* estimator. There are other linear estimators, but they have different weights $\lambda_i$.They do not have the other special properties, unbiasedness and "best-ness" (optimality). And there are certainly non-linear estimators that might have very interesting properties, *but we do not consider them here*.

# E: Estimator 

We get this one for free. The kriging estimator $Z^{*}(x)$ is a function of the sample $z_1, z_2, z_3, ... z_n$ (as we saw above).

# U: Unbiased

The kriging estimator is *unbiased*, meaning that the expected difference between the true value $z(x)$ and the estimated value $z^{*}(x)$ is zero. 

<div>
$$
E\left[Z({x})-Z^{*}({x})\right]=0
$$
</div>

This means, on average, the estimator will be correct. 

This is one of the kriging constraints. We know that the estimator $z^{*}(x)$ can be rewritten as a weighted sum. A weighted sum is just many additions written in a convenient, abbreviated way, so the expectation operator can go inside the sum (the expectation of the sum is the sum of the expectations). It is applied individually to every $z(x_{i})$.

<div>
$$
E\left[Z^{*}\right]=E\left[\sum_{i=1}^{N} \lambda_{i} z\left(x_{i}\right)\right] = \sum_{i=1}^{N} \lambda_{i} E\left[z\left(x_{i}\right)\right]
$$
</div>
 
It is important to remember that we do not know the values $z(x_{i})$ as we are in the general case. The best guess we can make for their value is the mean, $\bar{z}$, *if we make the assumption that the mean is the same everywhere*. This is called the **stationarity** assumption.  
Then the expectation can be written as

<div>
$$
E\left[Z^{*}\right]=\sum_{i=1}^{N} \lambda_{i} E\left[z\left(x_{i}\right)\right]=\sum_{i=1}^{N} \lambda_{i} \bar{z}=\bar{z} \sum_{i=1}^{N} \lambda_{i}
$$
</div>

With the assumption that 

<div>
$$
\sum_{i=1}^{N}\lambda_{i}=1
$$
</div>

we can finally rewrite the kriging system in the way we would like:

<div>
$$
E\left[z({x})-z^{*}({x})\right]=E\left[z({x})\right]-E\left[z^{*}({x})\right] = \bar{z} - \bar{z}\sum_{i=1}^{N} \lambda_{i} = \bar{z} - \bar{z}\times{1} = 0
$$
</div>

The difference is zero when we enforce that assumption, so the estimator is *unbiased*. 

# B: Best



# Why is this important? 

It's important because
- Good to know what exactly is optimized when 
- Strengths and weaknesses of the kriging algorithm, and expectations 
- Helps us learn the 

# Resources

[Derivation of the Kriging Equations](https://web.archive.org/web/20190904062202/http://ceadserv1.nku.edu/longa//modules/geostats/lec/latex2html/node1.html)


[Kriging Methods](https://www.nersc.no/sites/www.nersc.no/files/Basics2kriging.pdf)


[Best Linear Unbiased Estimation and Kriging](http://alertgeomaterials.eu/data/school/2014/session2/06b_Fenton_Blue.pdf)

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