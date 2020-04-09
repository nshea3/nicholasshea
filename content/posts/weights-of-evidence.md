---
title: "Weights of Evidence"
date: 2020-02-07T00:15:54+01:00
draft: true
---


Weights of evidence is a broad label describing a number of different methods and frameworks. Weights of evidence methods are used in binary classification problems. Weights of evidence is frequently used for feature engineering and exploratory data analysis in many different applicatoins. It is also very popular as a supervised learning algorithm, especially in geospatial and geoscientific problems (including mineral potential mapping) and in public health research. Weights of evidence is intuitive, convenient, and has deep theoretical links to information theory and Naive Bayes classifiers. 

## Information Theory Background

Weights of Evidence comes from Shannon's *mutual information* measure. Mutual information measures the amount of information we obtain about one random variable $X$ by observing a different random variable $Y$. This is the essence of the feature engineering task (we want to find feature variables that tell us a lot about our variable of interest) and supervised learning (we want to use those feature variables to predict our variable of interest!) Mutual information is expressed as follows:

<div>
$$ \mathrm{I}(X;Y) \equiv \mathrm{H}(X)+\mathrm{H}(Y)-\mathrm{H}(X, Y)$$
</div>

$\mathrm{H}(X)$ and $\mathrm{H}(Y)$ are marginal entropies and $\mathrm{H}(X, Y)$ is the joint entropy. 

Joint entropy $\mathrm{H}(X, Y)$ is further defined as 

<div>
$$H(X, Y)=-\sum_{x, y} p(x, y) \log _{2} p(x, y)$$
</div>

Mutual information is maximized when the the joint entropy $\mathrm{H}(X, Y)$ is **lowest**. Entropy is often described as the average level of "uncertainty" or "surprise" associated with a random variable's possible outcomes. It is useful to think about the opposite extreme: the distribution with maximum entropy is a uniform distribution. In the case of *independent* random variables, knowing $X$ gives us no information about $Y$. 


The entropy 

At the extremes, if 



## Mineral Potential Mapping

Starts with Bayes' rule:

With the 

<div>
$$P(D | B)=P(D) * \frac{P(B | D)}{P(B)}$$
</div>

Taking the logarithm 

Of course, there are many limitations to the weights of evidence classifier 



Sources: 

[Weights of Evidence Method](https://www.ige.unicamp.br/wofe/documentation/wofeintr.htm)

[Geographic information systems for geoscientists: modelling with GIS](http://agris.fao.org/agris-search/search.do?recordID=US201300289050)

[Data Exploration with Weight of Evidence and Information Value in R](https://multithreaded.stitchfix.com/blog/2015/08/13/weight-of-evidence/)


[CS340 Machine learning Information theory](https://www.cs.ubc.ca/~murphyk/Teaching/CS340-Fall07/infoTheory.pdf)


[Application of Information Theory, Lecture 2 Joint & Conditional Entropy, Mutual Information](http://www.cs.tau.ac.il/~iftachh/Courses/Info/Fall14/Printouts/Lesson2_h.pdf)


[Mutual information versus correlation](https://stats.stackexchange.com/questions/81659/mutual-information-versus-correlation)

[Information entropy](https://www.youtube.com/watch?v=2s3aJfRr9gE)

[Information Package Vignette](https://cran.r-project.org/web/packages/Information/vignettes/Information-vignette.html)

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