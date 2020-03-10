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
* Note that for a linear model, the plane that best approximates the behaviour of the function and the average gradient of the model, which points towards the stimulus which drives the system best, are one and the same. 

### Natural evolution strategies

* Natural evolution strategies (NES) are a family of black-box, gradient-free optimizers for (potentially non-differentiable) functions.
* The idea is to calculate the derivative of the *expectation* a function $f$ in a local neighborhood.
* The neighborhood is defined via a density $\pi(\theta, z)$.
* We can use the log-derivative trick to propagate the gradient through the expectation: 

$$\nabla_\theta E_\pi(z, \theta)[f(z)] = \nabla \int \pi(z, \theta) f(z) dz \newline = \int \nabla \pi(z, \theta) f(z) dz \newline
= \int \nabla \log \pi(z, \theta) \pi(z, \theta) f(z) dz$$

Where the last equality is derived from:

$$\nabla \log \pi(z,\theta) = \frac{\nabla \pi(z, \theta)}{\pi(z, \theta)}$$

* A standard neighborhood which is often used in practice is the isotropic gaussian centered at $\mu$ with a standard deviation $\sigma$.
* If we take a Monte Carlo estimate of the expectation, we find an approximation for gradient as:

$$\nabla E[f] \approx \frac{1}{N} \sum_{1}^N \frac{1}{\sigma^2} (z-\mu) f(z)$$

* This is exactly the response triggered average with an isotropic gaussian stimulus ensemble.
* Thus, we can view reverse correlation as estimating an approximate gradient of the response function of a neuron
* This reveals an unexpected link between reverse correlation and optimization: the response triggered average tells us how we should change a stimulus locally to increase the response of the system
* We could use reverse correlation as a subroutine in a closed-loop strategy to estimate the prefered stimulus of a neuron. Wierstra et al. (2014) present a complex method based on following the natural gradient of the estimate that works well in practice. 
* Because of the resurgence of interest in the application of black-box optimization for reinforcement learning and meta-optimization, we can learn a lot of interesting tricks to optimize standard reverse correlation by perusing this literature.
* My favorite interesting trick to increase the efficiency of estimation: pairing every stimulus with its opposite. This simple tweak increases efficiency of estimation by x.

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

### Open questions

* Can the brain implement scoring to learn to go down a gradient?
* Can the brain implement REINFORCE?

### Notes

* https://www.nature.com/articles/nprot.2007.27
* http://ai.stanford.edu/~quocle/TCNNweb/index.html

Zoterro folder: spike-triggered

