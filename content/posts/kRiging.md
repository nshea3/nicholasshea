---
title: "kRiging"
date: 2019-12-09T17:41:29+01:00
---

# kRiging (Kriging in R)

As a programmer, it is often frustrating to solve equations by hand, knowing that a clever implementation in software could solve an infinite variety of similar problems. This cannot be said for the paper-and-pen approach. As a \<\<Mastère spécialisé\>\> student in the Cycle de Formation Spécialisée en Géostatistique at Mines Paristech, I have spent the better part of these past few weeks building and solving kriging systems. It certainly builds intution and confidence with the manipulations, but I'd still like to code up a quick implementation. 

At the end of the day, I find that the linear algebra or matrix form of an equation is much easier to read than the equivalent with nested sums (in multivariate geostats, the nesting can build to quadruple sums and beyond!)

*Cokriging system for 2 variables ([from Rivoirard, Course on Multivariate Geostatistics](http://cg.ensmp.fr/bibliotheque/public/RIVOIRARD_Cours_00608.pdf)). Only downhill from here.*

\begin{array} { l } { \sum _ { \beta \in S _ { 1 } } \lambda _ { 1 \beta } C \left( Z _ { 1 \alpha } , Z _ { 1 \beta } \right) + \sum _ { \beta \in S _ { 2 }} \lambda _ { 2 \beta } C \left( Z _ { 1 \alpha } , Z _ { 2 \beta } \right) = C \left( Z _ { 0 } , Z _ { 1 \alpha } \right) } 
\newline
{ \sum _ { \beta \in S _ { 1 } } \lambda _ { 1 \beta } C \left( Z _ { 1 \beta } , Z _ { 2 \alpha } \right) + \sum _ { \beta \in S _ { 2 } } \lambda _ { 2 \beta } C \left( Z _ { 2 \alpha } , Z _ { 2 \beta } \right) = C \left( Z _ { 0 } , Z _ { 2 \alpha } \right) } \end{array}

The terms in the sum expand for every point $\beta$ in $S_1$ (every point where we have a value for $Z_1$) and $\beta$ in $S_2$ (every point where we have a value for $Z_2$). Then the expression expands for every $\alpha$ (so we have this pair of large expanded sums for every permutation of points in $S_1$ with points in $S_2$). It is clear why kriging scales very poorly with input size ([this paper](https://arxiv.org/pdf/1702.01313.pdf) and [this paper](https://www.su.se/polopoly_fs/1.279682.1461150951!/menu/standard/file/fastkrigingGMRF.pdf) both peg the training time at $O(n^3)$ and the space complexity at $O(n^2)$ for ordinary *univariate* kriging). We also see that a matrix form would be a little easier to work with. 

I found a pretty [amazing paper, Kriging in Perspective](http://www.stat.cmu.edu/~cshalizi/kriging.pdf). It does a very good job introducing the intuition of kriging but also providing a mathematical justification of the connection to least squares and some of the properties that make kriging so special and useful.

[Follow along here](https://nshea3.github.io/geostats/kRiging/kriging.html)

The best feature by far of this paper is an entire worked example in R that solves the kriging matrix for a toy problem.
Most of the kriging examples and libraries are extremely optimized and the system is no longer presented in a readily interpretable form. I learn best when I can control the problem and introduce complexity little by little, and I still have access to tangible, primitive data structures that I understand well. 

That is a major advantage of using code examples. Here, for instance, I can create a system that shows the screen effect for an exponential variogram model with. Here, the weights of the distant points shrink to zero. 

```r
### Creating a vertical line of points 
coords <- expand.grid(x=c(0), y=c(-2,-1,0,1,2))

### Keep track of which row is the origin (where we want to predict at)
predict.pt <- which(coords$x==0 & coords$y==0)

### Use the built-in function to create distance matrices
distances <- dist(coords) # Euclidean matrix by default

### Returns a structure w/ just lower-triangular half
distances <- as.matrix(distances)

### Create the matrix of all covariances
covars <- 10*exp(-distances/8)

### Break it into Cov(Y,Z) and Var(Z)
Cov.YZ <- covars[predict.pt, - predict.pt]
Var.Z <- covars[-predict.pt, -predict.pt]


### Find the coefficients
beta <- solve(Var.Z) %*% Cov.YZ

plot(coords, xlab="longitude", ylab="latitude", type="n")
points(coords[predict.pt,], col="red")
points(coords[-predict.pt,], cex=10*sqrt(beta))
```
This code produces the following diagram:
<image src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABUAAAAPACAMAAADDuCPrAAAA0lBMVEUAAAAAADoAAGYAOjoAOmYAOpAAZmYAZrY6AAA6OgA6Ojo6OmY6ZmY6ZpA6ZrY6kJA6kLY6kNtmAABmOgBmOjpmZjpmZmZmZpBmkLZmkNtmtrZmtttmtv+QOgCQZjqQZmaQkGaQkJCQkLaQtraQttuQtv+Q2/+2ZgC2Zjq2kDq2kGa2tpC2tra2ttu225C227a229u22/+2///bkDrbkGbbtmbbtpDbtrbb25Db27bb29vb2//b/7bb////AAD/tmb/25D/27b/29v//7b//9v////tae1BAAAACXBIWXMAAB2HAAAdhwGP5fFlAAAdoElEQVR4nO3de2Pb1mGHYch1ZtVpuvmy1Fvs7ObFnutuSVS7qzNXVix9/680gjdRF0vijwAOgfM8/8S6kASIwze4qzkDINKUngCAsRJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoQEFCAkoAAhAQUICShASEABQgIKEBJQgJCAAoT2O6ANQGe6T1Tnz9ih0u82MC2dN6rrJ+xS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"></image>
*Four points, only two nonzero weights*

Another good resource, with a worked example that shows a kriging system solved by hand:
[Kriging Example](http://www.imm.dtu.dk/~alan/krexample.pdf)


Yet another good resource:
[Kriging Example](https://hal.archives-ouvertes.fr/cel-01081304/document)

I will follow up with further examples and resources for geostatistics as I discover them! 


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
