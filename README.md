# Analogies between physics and learning

Here I will review some areas of physics that I believe can inform AI research by providing an additional conceptual and computational frameworks. This AI-physics cross-pollination has existed since before Boltzman Machines and Simulated Annealing, often suggesting unexpected directions for AI research. What's next?

## Fisher Information in Thermodynamics and Statistics

The Fisher Information matrix *F* quantifies sensitivity of a parametric probability distribution to small variations in its parameters. Its significance in statistics is reinforced by several useful properties, e.g.
- *F* is the second derivative of the Kullback-Leibler divergence *D<sub>KL</sub>(q|p)* evaluated at the same distribution (*q=p*). 
-  *F<sup> -1</sup>* places a lower bound on the variance of parameter estimators through the Rao-Cramer theorem.

Fisher information has played a key role in several machine learning contexts recently, to name two:

- Natural Gradient methods
- Elastic Weight Consolidataion

Through Natural Gradient, the ML community has come to learn that *F* is actually a Riemannian metric, in the sense of differential geometry.

As it happens, the physics community is still attempting to understand what this metric means in the context of thermodynamics. Some intriguing hints have surfaced in the past few years.
- Like any metric, *F* can be used to compute the lengths of curves, and it turns out that the curves shortest curves represent ways of varying the control parameters of systems such that minimal energy is dissipated in traveling between the two endpoint configurations.
- Singularities in *F* (and, it seems more likely, in the corresponding Ricci curvature tensor *R*) correspond to phase transitions, in paricular second-order ("critical") phase transitions.

To my knowledge, these facts have yet to be translated back into the language of machine learning. Here is my interpretation:

- Equilibrium corresponds to stabilized learning: the parameters of the network have converged to their optimal values given the data distribution.
- Dissipation corresponds to misprediction: in transit between training distributions 1 and 2, the network is exposed to the data of 2 but is not yet adapted to this distribution. Dissipation corresponds to total integrated difference between the training distribution 2 and the model's distribution, where the integration is along the trajectory in model space.

Understanding this analogy more quantitatively would be a nice step toward understanding Elastic Weight Consolidation and Natural Gradient methods more precisely.

## Entropy, Fluctuations, and Reinforcement Learning

A remarkable result in 1999 showed that entropy production is directly related to microscopic reversibility, viz.

<img src="https://github.com/AI-RG/hello-world/blob/master/ai_phys_assets/entropy1.gif" alt="eq1" />

In other words, the difference of log likelihoods of forward to reverse trajectories is proportional to the net entropy procuced along the (forward) trajectory. To rephrase: not only does entropy tend to increase with time, but entropy actually *quantifies* how likely a process is compared to its reverse.

Following this insight, there arose several *fluctuation theorems* that quantify the likelihood of statistical fluctuations, usually in terms of entropy.

Such fluctuation theorems may be useful in the context of Reinforcement Learning. For example, for any Markov process with reversible transitions, we have the following inequality:

<img src="https://github.com/AI-RG/hello-world/blob/master/ai_phys_assets/entropy4.gif" alt="eq4" />

where

<img src="https://github.com/AI-RG/hello-world/blob/master/ai_phys_assets/etropy5.gif" alt="eq5" />

and where 

<img src="https://github.com/AI-RG/hello-world/blob/master/ai_phys_assets/entropy2.gif" alt="eq2" />
<img src="https://github.com/AI-RG/hello-world/blob/master/ai_phys_assets/entropy3.gif" alt="eq3" />


## Bibliography



- G. Crooks, "Entropy production fluctuation theorem and the nonequilibrium work relation for free energy differences" (arXiv: cond-mat/9901352)
- D. Sivak and G. Crooks, "Thermodynamic Metrics and Optimal Paths" (arXiv: 1201.4166)
- M. Prokopenko et al., "Relating Fisher Information to Order Parameters" Phys. Rev. E 84 (2011)
- X. Wang, J. Lizier, and M. Prokopenko, "Fisher Information at the Edge of Chaos in Random Boolean Networks" Artif. Life (2011)
- X. Wang, J. Lizier, and M. Prokopenko, "A Fisher Information Study of Phase Transitions in Random Boolean Networks" ALife XII (2010)
- G. Rotskoff and G. Crooks, "Dynamic Riemannian Geometry of the Ising Model" (arXiv: 1510.06734)
- G. Bisker et al., "Hierarchical Bounds on Entropy Production Inferred from Partial Information" (arXiv:1708.06769)
- T. Gingrich, G. Rotskoff, and J. Horowitz, "Inferring dissipation from current fluctuations" (arXiv: 1609.07131)
