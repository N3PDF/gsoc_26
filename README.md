# Google Summer of Code 2026
Evaluation task set up for GSoC 2026.

# Overall objectives
The objective of this evaluation task is for us to understand your familiarity with Rust/Python and (importantly) the interplay between those languages.
This is a very simplified version of our proposal for GSoC so it will also help you to understand if this is the right kind of problem for you :smiley:

The idea is to integrate some function which potentially could be very computationally intensive.
Thus, we want the computationally intensive function to be compiled in Rust, and then interfaced to a Python library (for instance, `scipy` provides routines for integration).

The example function here is the [Euler Beta function](https://en.wikipedia.org/wiki/Beta_function):

$$
B(\alpha, \beta) = \int_{0}^{1} \text{d} x \, x^{\alpha - 1}(1-x)^{\beta-1} = 2 \int_0^{\pi/2}\text{d} \theta\,(\sin\theta)^{2\alpha-1}(\cos\theta)^{2\beta-1}
$$

The beta function can be regularly encountered in particle physics.
The first representation naturally appears, e.g., when trying to solve the DGLAP equations, the main differential equations which EKO is solving.
The second representation naturally appears, e.g., when considering the volume of higher-dimensional balls (which is one out of many ingredients necessary to arrive at the DGLAP equations).

Your task is to implement both representations using Python top-level, i.e. for providing the interpolation library and the steering program, and Rust low-level, i.e. for the integration kernels.
Make the choice of which representation to choose a parameter and resolve that choice on the Rust side, such that you have three functions in Rust.
You can use this control flow function in Rust also to apply a change of variables to, e.g., representation two to harmonize the integration limits (which lay on the Python side).

## Plan
A possible breakdown of the task is the follwing:

1. Create two Rust functions for the two integrands, and another one for choosing the representation.
2. Integrate the functions above numerically using a integration algorithm (e.g. from `scipy`). 
3. Perform a benchmark study of the two implementations.
   - How long do they take? How heavy each one of them is in memory?
   - How does this depend on the integration routine parameters, such as the relative tolerance, the absolute tolerance, the number of subdivisions, etc.
   - How does this depend on the targeted accuracy? Compare to known analytical results (give references!). Compare to the implementation of [`scipy.special.beta`](https://docs.scipy.org/doc/scipy/reference/generated/scipy.special.beta.html#scipy.special.beta).
   - You can also compare with a pure Python implementation.
   - Bonus: in the realistic physics case $\alpha$ is a complex number, how does the implementations deal with this case?

### Bonus
The given case is a simplified version of our EKO code.
In the real case the "control flow function", i.e. the function calling the "hard" Rust function, is a [numba-compiled Python function](https://numba.pydata.org/).
Implement this intermediate layer also here.
How does this affect the benchmark study?

# Evaluation
Clone this repository into a private repository and add both Juan and Felix to it:

- Juan Cruz-Martinez @scarlehoff
- Felix Hekhorn @felixhekhorn

Please send us an email, when you are done.

**Deadline: Thursday, March, 12 2026 00:00 UTC**

If there is something unclear, don't hesitate to contact us.
