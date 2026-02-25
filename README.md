# gsoc_26
Evaluation task set up for GSoC 2026.

# Overall objectives
The objective of this evaluation task is for us to understand your familiarity with rust/python and (importantly) the interplay between those languages.
This is a very simplified version of our proposal for GSoC so it will also help you to understand if this is the right kind of problem for you :)

The idea is to integrate, using a higher-leve python library, some function which potentially could be very computationally intensive.
For that, we want the computationally intensive function to be compiled in rust, and then interfaced to a python library (for instance, `scipy` provides routines for integration).

The function to be integrated is the following:

$$
y = \int_{0}^{1} \text{d} x | \mathbf{A} \vec{z} |
$$

where $x$ can go between 0 and 1, $\vec{z}$ is a two-component vector such that $z = (x/2, 2*x)$, and $\mathbf{A}$ a $2x2$ matrix.

As a bonus, you can try to compile the python wrapper of the rust function with numba. This is something that might be useful also during the project :)

## Plan
A possible breakdown of the task is the follwing:

1. Create a Rust kernel for the integrand.
2. Integrate the function above numerically using a integration algorithm from `scipy` . 
3. Benchmark the implementation, how long does it take? How close is it to the analytical result? How heavy is it in memory?
4. (bonus) compile with `numba` the python function integrated in 2. Is it faster? Does it use more memory?

# Evaluation
Create a private repository and add both Juan and Felix to it, usernames:

Juan Cruz-Martinez @scarlehoff
Felix Hekhorn @felixhekhorn
