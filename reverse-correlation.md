## Reverse correlation and linearization of complex functions

* Reverse correlation has long been used to characterize neurons.
* We present a series of random stimuli to a neuron, and average those that generated a response - this gives us the spike-triggered average
* It can be shown that this method estimates a local linear estimate of a neuron's response function.
* It's fallen out of favor as people have graduated to more complex models (e.g. GLMs and deep nets) with more complex stimuli (natural scenes) to probe brain representations
* However, the machinery underlying reverse correlation is making somewhat of an unexpected comeback in different corners of machine learning, something that I'm sure will surprise many machine learning people as well as neuroscientists.
* Digging deeper into these subfields yields some insights on improvements in reverse correlation that we can take back to computational neuroscience.

### The theory behind reverse correlation

* Wiener-Volterra theory
* Expansion to second order
* Scale of the expansion is important!
* We have $f(x) \approx x_0 + \nabla f \cdot \dot (x - x0)$

### Natural evolution strategies

* Natural evolution strategies estimate an averaged gradient of a (potentially non-differentiable) function within a neighborhood.
* The idea here is to approximate a function locally, in a least-squares sense via a weighted estimate from a plane.
* A standard neighborhood which is often used is the isotropic (gaussian) one with a standard deviation $\sigma$.
* We can use the log-derivative trick to find an estimate of the linear function.
* It turns out that this is exactly equal to the response triggered average with an isotropic gaussian stimulus ensemble.
* The paper proposes an interesting trick to increase the efficiency of estimation: pairing every stimulus with its opposite. 
* This increases efficiency by x.

### LIME

* Ref: https://christophm.github.io/interpretable-ml-book/lime.html
* Local surrogate models try to approximate complex functions with simpler, local expansions.
* In general, we try to find a model which approximates a complex function $f$ according to a weight window $\pi$: $\arg \min_{g\in G} L(f, g, \pi) + \Omega(g)$, where $L$ is a loss function and $\Omega(g)$ captures the complexity of $g$.
* The authors suggest to use a Gaussian-shaped neighborhood around an anchor $a$ and a sum-of-squares loss, leading to the weighted loss: $L = \sum_i \exp(-\frac{||x_i - a||^2}{\sigma^2}) (f(x_i) - g(x_i)) ^ 2$
* Furthermore, they assume the complexity penalty to be zero. With a linear $g$, we obtain the same estimate as the natural evolution strategy, which itself is equivalent to reverse correlation.
* Because surrogate models are local only, we can obtain different local linear estimates by changing anchors. 
* One example of this idea is that we can linearize quadratic responses (i.e. complex cells) by choosing an appropriate anchor point. This is the idea behind Movshon et al. (1978)

![](reverse-correlation-images/movshon-1978.png)

* There's other excellent nuggets in the paper. For instance, they suggest using a maximally diverse ensemble of examples (SP-LIME) to illustrate the functioning of the models for humans. A similar idea was used in Cadena et al. (2018) to visualize diverse features that triggered large responses in early stages of a deep neural net around an anchor point (invariant or equivariant features).
* One issue is that we still don't know how to estimate $\epsilon$

### Conclusions

* Both NES and LIME use a similar local linearization strategy as reverse correlation.
* From NES, we learn that using pairs of balanced stimuli improves the efficiency of estimation
* From LIME, we highlight that we can perform RC centered around different anchor stimuli, getting different results
* LIME can be used to open a deep net's black box around a given stimulus class center or a particular exemplar
* New classes of estimations can be found - in particular, we can apply the technique of STC (aka the order 2 Wiener-Volterra expansion) to find the invariant dimensions of a deep net.
* Sampling could be improved in the current implementation of LIME. Data points are sampled from a Gaussian distribution, ignoring the correlation between features. This can lead to unlikely data points which can then be used to learn local explanation models.

### Notes

* https://www.nature.com/articles/nprot.2007.27
* http://ai.stanford.edu/~quocle/TCNNweb/index.html

Zoterro folder: spike-triggered

