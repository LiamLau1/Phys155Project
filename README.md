# Phys155Project
Mentoring project folder for understanding phase transitions

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
- [] 1D Ising problem analytic calculation and exploring properties

From what we discussed, the 1D Ising model has a Hamiltonian (which really means energy):
```math
\Huge H[\{\sigma\}] = - J \sum_i^{N-1} \sigma_i \sigma_{i+1},
```
where we call $J$ the coupling constant, and we will care about $J > 0$ (Ferromagnetic), $i$ means sites, and the spin $\sigma_i$ can be $\uparrow$ (taking the value $+1$), or $\downarrow$ (taking the value $-1$). Where the energy is a function of { $\sigma$ } which is a huge list of $+1$ and $-1$ which tells you the configuration of the spins on this 1D chain.

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
2. 
3.


### Week of Monday 17th November
- [] Setup classical montecarlo for 1D problem
- [] Explore the 1D problem using classical montecarlo
- [] Develop elevator pitch about your project
- [] Expand your code to 2D

### Week of Monday 24th November
- [] Introduction slides for your presentation
- [] 2D properties (magnetization, and correlations)


## Contact
- Pleae email me whenever you have any questions
- email: liam.lh.lau@physics.rutgers.edu
