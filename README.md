# Phys155Project
Mentoring project folder for understanding phase transitions. Inspired by computational physics project at Cambridge part II.

## Goal of the project
- Main goal is to get a feel for what phase transitions are and why they are so generally applicable. Hopefully you'll get a taste of physics, particular statistical mechanics, and get interested in research.
- Two problems. The first is about percolation, which will be more of a warm up exercise. The second is about the Ising model, which become more and more open ended at the end.   
- For the presentation, just demonstrate what you've learnt in simple words to your peers.

## Expectations and Guidelines
- Be kind, work collaborativelyi please. There is no competition, just learn what you can.
- Minimal use of AI, limited to conceptual questions please.
- I will do my best to be adaptable to your backgrounds and expectations for the project.
- 5 hours of work per week
- Please please comment your code with your thoughts

## Reading
1. Motivation. Section 1.1 of David Tong's [Statistical Physics lecture notes](https://www.damtp.cam.ac.uk/user/tong/statphys/statphys.pdf)
2. [Introduction to the Ising Model by Barry Cirpa](https://www2.stat.duke.edu/~scs/Courses/Stat376/Papers/isingIntro.pdf) until the start of section 2.

## Project Checklist
### Week of Monday 3rd November
- [x] Pseudo code for percolation
- [x] Reading 1 and 2
- [x] Send Liam questions about 1 and 2
- [x] Fill in code and produce successful throughput probability vs metallic probability
### Week of Monday 10th November
- [x] Discussion on the week of November 10th about reading 1 and 2.
- [x] 1D Ising problem analytic calculation and exploring properties

From what we discussed, the 1D Ising model has a Hamiltonian (which really means energy):
```math
\Huge H[\{\sigma\}] = - J \sum_i^{L-1} \sigma_i \sigma_{i+1},
```
where we call $J$ the coupling constant, $L$ is the length of the chain (number of lattice sites), and we will care about $J > 0$ (Ferromagnetic), $i$ means sites, and the spin $\sigma_i$ can be $\uparrow$ (taking the value $+1$), or $\downarrow$ (taking the value $-1$). Where the energy is a function of { $\sigma$ } which is a huge list of $+1$ and $-1$ which tells you the configuration of the spins on this 1D chain.

Some questions for the 1D Ising problem:

1. As we discussed on Monday 10th November, we never really know the actual configuration of our box of "stuff" (ie. how the spins look). Since we **don't know**, the configuration, we have to take a statistical approach. The probability distribution is given by,
```math
\Huge p(H[\{\sigma\}]) = \frac{e^{-\frac{H[\{\sigma\}]}{k_B T}}}{Z}
```
where
```math
\Huge Z = \sum_{\{\sigma\}} e^{-\frac{H[\{\sigma\}]}{k_B T}}
```
is called the Partition function, and the sum over { $\sigma$ } means the sum over all possible configurations. For example if we have two spins, there are 4 configurations. Could you show why $p$, above, has the properties of a probability (non negative, and also only takes values between 0 and 1, inclusive).
Imagine we want to measure the magnetization, which we've defined last time tells us how ordered the state is,
```math
\Huge m = \frac{1}{L} \langle \sum_i^L \sigma_i \rangle
```
2. Could you write what the sum over the configurations explicitly means? Hint: think about what each spin value can take.
3. If we just took one state (ie. forget the expectation value of the moment), what is the $m$ value for the ferromagnetic state (all up or all down), and what is the $m$ value for the antiferromagnetic state (alternating up and down). What about some random configuration in between?
4. Before trying this part, let's discuss 2. first, so email me when you get here or need some help. Using your explict sum over configurations, find Z as a closed form expression of $J$ and $k_B T$. This is a little involved, have a go without chatgpt, and let's discuss it when I meet you guys separately.
5. Imagine now you measure how correlated the spin on site $i$ is to the spin on site $i + j$. Ie. we want to measure the average alignement of two spins $\sigma_i$ and $\sigma_{i + j}$ that do not necessarily have to be neighbors. You could derive that,
```math
\Huge \langle \sigma_i \sigma_{i+j} \rangle = \left[\tanh{\left(\frac{J}{k_B T}\right)}\right]^j
```
What happens to this average correlation value when you make $j$ big?

### Week of Monday 17th November
- [] Develop elevator pitch about your project (This is the most important thing this week)
- [] Setup classical montecarlo for 1D problem
You might find [this useful to get going with the algorithm](https://phys.libretexts.org/Bookshelves/Mathematical_Physics_and_Pedagogy/Computational_Physics_(Chong)/13%3A_The_Markov_Chain_Monte_Carlo_Method/13.02%3A_The_Ising_Model)

I will describe the algorithm for the 2D case, and you can generalize this down to the 1D case. Suppose we have a square lattice of $N$ by $N$ lattice points, for a total of $N^2$ sites. The energy of the system is given by,
```math
\Huge H[\{\sigma\}] = - J \sum_{\langle i j \rangle} \sigma_i \sigma_{j},
```
where the sum $\langle i j \rangle$ is over nearest neighbor pairs of atoms only. In 2D we thus have 4 nearest neighbor interactions. $J$ is the exchange energy. It is useful to use periodic boundary conditions (as we described in our meeting this week), so that every spin has four neighbors.

Starting from some initial set of spin orientations, perhaps a random or uniform set (I suggest you start with a ferromagnetic state to begin with), the model is evolved in time by a Monte‑Carlo technique: pick a spin, and calculate the energy $\Delta E$ required to flip it. If $\Delta E < 0 $, flip the spin; if $\exp{(−\Delta E/T)} > p $, where $p$ is a random number drawn from a uniform distribution in the range $[0, 1]$, then flip the spin; else do nothing.

We now repeat this step for many lattice sites. One can either step systematically through the lattice doing $N^2$ possible flips, or pick $N^2$ random points. You can think of these $N^2$ operations together as a single time step.

Now repeat many steps to evolve the spin system, sampling relevant quantities and averaging them. The physical goal is to measure the thermodynamic and magnetic properties of the system as a function of time and as a function of the temperature (and magnetic field, if we have time).

You will find it easiest to measure $T$ in units of $J$ (where we have set $k_B = 1$ for convenience). Let's now explore what physics this model has, and see if this is what we see in the real world!

- [] Explore the 1D problem using classical montecarlo
- [] Expand your code to 2D
- [] Explore 2D properties (magnetization, and correlations, etc.)

So let me point out a few things that you might want to investigate (you can do a WHOLE lot more, and I want to leave this to your discretion of what you want to investigate).

1. Try to quantify how long (ie. the number of montecarlo whole "time steps") it takes to get from your initial configuration (I recommend an ordered state to begin with, then you can explore after), to a state which appears to be in thermal equilibrium (ie. as you generate new samples from each montecarlo time step, it "looks" basically the same). Hint: how can we quantify "looks" the same? Maybe you can calculate something here and see if that changes? Try this for a range of different temperatures. This amount of time to reach equilibrium is called the thermalization time, or the burn-in time.

Why is it important to calculate physical things about the system, for example magnetization, or other correlations, when the system is in equilibrium?

2. Quantify how the total magnetization $ M $ (or you could you the magnetization per spin $ m $ by dividing the total magnetization by the number of sites, I would recommend this, and use small $m$ for everythin instead of large $M$) fluctuates with “time” when the system is in equilibrium.  
The autocovariance of the magnetization $ M(t) $ for a time lag $ \tau $ is given by

```math
A(\tau) = \langle M'(t)\, M'(t+\tau) \rangle ,
```

where $ \langle \cdot \rangle $ denotes averaging over a “long” time (ie. it's a running average over our samples that is constantly being updated by the metropolis algorithm and this average is for some long enough "time", ie. enough "time steps") and  
$ M' = M - \langle M \rangle $ is the deviation from the mean.

The autocorrelation is

```math
a(\tau) = \frac{A(\tau)}{A(0)}.
```

Determine the “decorrelation time”: the time lag $\tau_e$ over which the autocorrelation falls to $ 1/e $ at different temperatures, especially near the critical temperature $ T_c $ (once you find it using other methods that we will outline below, or you can use Onsager's analytical solution for the infinite lattice $T_c(\infty) = 2/\ln{(1+ \sqrt{2})}$, but I would recommend you wait).

Plot graphs of the decorrelation time versus the temperature for two different lattice sizes $ N $, and consider how this impacts the averaging time needed to get accurate values in the other investigations.

3. Determine how the time averaged magnetization $\langle |m| \rangle$ varies with temperature, we use the absolute value to make sure we don't get cancellations if we motecarlo explore for a long time. Can you make an estimate of $T_c$?

4. Measure the heat capacity of the system as a function of temperature (google what this is and try to interpret it physically). We separately know that the heat capacity can be calculated using the fluctuations of the energy $H$.
```math
C_v = \frac{\langle E^2 \rangle - \langle E \rangle^2}{N^2 T^2}
```
Plot this as a function of temperature $T$. What happens around your estimate of $T_c$ to the heat capacity? Maybe this feature will actually be a better estimate for $T_c$ than your magnetization plot?

5. Compare your $T_c(N)$, which is dependent on the lattice size $N$, to the Onsager analytical result for the infinite lattice $T_c(\infty) = 2/\ln{(1+ \sqrt{2})}$. Investigate "finite size scaling", which suggests the critical temperature $T_c(N)$ for a lattice of size $N$ (remember your lattice is $N^2$ total size) varies as,
```math
T_c(N) = T_c(\infty) + a N^{-1/ \nu}
```
where $a$ and $\nu$ are constants. Try and see if your data fits this result (do not use the value of $T_c(\infty)$, but see if you can estimate it from your data). Can you quantify your uncertainties? 


### Week of Monday 24th November
- [] Introduction slides for your presentation
- [] Continuation of exploring 2D properties (magnetization, and correlations, etc.)


## Contact
- Pleae email me whenever you have any questions
- email: liam.lh.lau@physics.rutgers.edu
