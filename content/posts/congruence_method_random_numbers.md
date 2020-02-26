---
title: "Random Numbers via the Congruence Generator Method"
date: 2020-02-03T19:47:02+01:00
draft: true
---



It's something that has interested me for some time, from when I was asked to produce random samples on an exam (resorted to tossing a paperclip on the sheet in front of me, a strategy which as I learned later in an  actually undersamples the edges MIT OCW course , did not want )

It was even touched on briefly in my discrete math course and in my . It made an unexpected appearance 

## Motivation

Not immediately clear why we need random numbers without 
Often the justification is left at mumbling about Monte Carlo and crypto, which is fine if you know what both of those things are and how they work. 

I think the best example I could give for that would be the lottery. If we did not have a robust method of choosing, and the lottery became predictable, that would be great for people that are very good at math and pretty bad for everyone else. And when lotteries are used for things other than giving away money, the stakes can be much higher. 

[Why Randomness Matters](https://blog.cloudflare.com/why-randomness-matters/)

[Applications of randomness](https://en.wikipedia.org/wiki/Applications_of_randomness)

[Can You Behave Randomly?](http://faculty.rhodes.edu/wetzel/random/intro.html)

[Introduction to Randomness and Random Numbers](https://www.random.org/randomness/)

## Linear Congruential Generator

Method of generating a sequence of random numbers distributed *uniformly* between zero and one. 
Every number in $[0,1)$ has an equal probability of being chosen. 

We choose $X_{n+1}$

Recurrence relation (basically a recursive definition or difference equation)

### Defintion

$$X=\left(a X_{n - 1}+c\right) \bmod m$$

where $X_{n - 1}$ is the previous 

### Issues

The modulus function outputs integers. At minimum, it outputs $0$, and at maximum it outputs $m - 1$.
Dividing by m to get output between 0 and 1, we have
Numbers generated from the example can only assume values from the set $I = \left(0, \frac{1}{m}, \frac{2}{m}, ... , \frac{m - 1}{m}\right)$

This makes sense because we would expect the 


## Conclusion

Is it practical? Not for most purposes, though it has pretty amazing performance .
However, we are able to look at the advantages and drawbacks and design considerations for random number generators with an accessible example, rather than jumping right into the Mersenne Twister source code.

Are we expected to accept their randomness on blind faith? does not seem right. It can be proven that the LCG method produce pseudorandom numbers in general, broadly appropriate for certain tasks, but the mathematics gets very advanced very quickly. A much better question to ask is whether this sequence of numbers is suitable. Ideally we would perform an empirical test to. 

Now that we have a sequence of numbers, is there a way of checking whether they are good or not? This can be accomplished using statistical tests including the Kolmogorov–Smirnov test.

## Sources:

[Linear Congruential Generator I](https://web.archive.org/web/20190729074539/http://pi.math.cornell.edu/~mec/Winter2009/Luo/Linear%20Congruential%20Generator/linear%20congruential%20gen1.html)

[Linear Congruential Method](https://web.archive.org/web/20200203185729/https://www.eg.bucknell.edu/~xmeng/Course/CS6337/Note/master/node40.html)

[Linear Congruential Generators, RPub by Aaron Schlegel](https://rpubs.com/aaronsc32/linear-congruential-generator-r)

[Linear Congruential Generators](https://demonstrations.wolfram.com/LinearCongruentialGenerators/)


<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>


<script type="text/javascript" 
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>