---
title: "Non Linear Geostats"
date: 2020-01-28T19:26:37+01:00
draft: true
---

Currently preparing for an exam
The sentiment is that it's an underutilized field of geostatistics

Broad overview:

- Introduction 
- Selectivity curves, support effect, information effect
- Estimation

Stick with point support for the first post, estimation

- Indicator Approach
- Mosaic Model
- Indicator Cokriging/Disjunctive Kriging
- Indicator Residuals
- Discrete Diffusion models

We are able to do a lot with the *linear* tools, why should we consider nonlinear tools as well? 

The primary motivation for this technique was a desire to estimate a nonlinear function of the variable, like a threshold function (an **indicator** in geostatistics), rather than the variable itself as in kriging. In the mine evaluation process, the . We can ask, what proportion are over this value? What proportion are under?

<!---
Get the grade example from the first couple of lectures and put it here
-->

This set of methods has since been applied to environmental and petroleum problems as well.

## Thresholds and Selectivity Curves

Borrowing the title of this section from Chapter 31 of Multivariate Geostatistics, it's worth a read if you are a serious student of geostats. 

We introduce variables ore tonnage $T(z)$, where grade is over threshold $z$, 
metal tonnage $Q(z)$, average grade $m(z)$.

$$T(z)=E\left[1_{z(v) \geq z}\right]=P[Z(v) \geq z]$$

We can also regard the average grade as a function $m(T)$ and the metal tonnage as a function $Q(T)$ of ore tonnage $T$.

These are called *selectivity curves* in the mining industry and  

Notice that they take into account the 


## Indicator Kriging




## The best sources:

[Introduction to disjunctive kriging and nonlinear geostatistics](http://www.cg.ensmp.fr/bibliotheque/public/RIVOIRARD_Cours_00312.pdf)

[A Step by Step Guide to Bi-Gaussian Disjunctive Kriging](http://www.ccgalberta.com/ccgresources/report05/2003-107-dk.pdf)


<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>

<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>