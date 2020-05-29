# John Jasa's NREL work portfolio

This portfolio serves to document and highlight my contributions to NREL projects, focusing on deliverables and tangible value-add.

It is a continual work-in-progress and is roughly divided by project.

## Contributions to WEIS

### Efficient derivative computation study

I set up and ran multiple computational experiments to benchmark different ways to compute derivatives for WISDEM, with the [results hosted here](https://github.com/johnjasa/derivative_comparisons).

Large portions of [WISDEM](https://github.com/WISDEM/wisdem) lack efficient derivative calculations, which would speed up gradient-based optimization.
This comparison study aimed to benchmark derivative computation methods that are relevant to WISDEM to determine their feasibility and utility.

I found that depending on the size of the inputs and outputs to the component, as well as the underlying code complexity, automatic differentiation may be a reasonable solution.
Analytic derivatives were always the fastest in terms of computational time, but required much more developer time, so they should be implemented only for extreme bottlenecks within the codebase.
The figure below shows an example of how the computational cost of different derivative computation methods scale with the number of inputs to the component.

<p align="center">
  <img src="total_derivs_num_inputs" alt="Derivative cost scaling with number of inputs" width="500"/>
</p>


### Introducing new optimization drivers to WISDEM and OpenMDAO

One of the goals of the WEIS project is to enable efficient exploration of the complex design space for floating offshore turbines.
To do this, we plan on integrating additional optimization packages into WISDEM so we can use evolutionary algorithms, discrete design variables, and eventually uncertainty quantification.

Towards this goal, I have implemented [NLopt](https://nlopt.readthedocs.io/) as a driver in OpenMDAO so we can use it in WISDEM.
NLopt provides optimization methods we previously could not access, including ISRES and DIRECT, which are both global optimizers.
My [driver implementation is hosted here](https://github.com/johnjasa/OpenMDAO/blob/nlopt_driver/openmdao/drivers/nlopt_driver.py) and I've written [tests verifying its capabilities here](https://github.com/johnjasa/OpenMDAO/blob/nlopt_driver/openmdao/drivers/tests/test_nlopt_driver.py).

This task is ongoing and Rob Hammond and I are working together to get more advanced optimization packages integrated, including [DAKOTA](https://dakota.sandia.gov/).

### WISDEM documentation and code quality improvement

- Contributed to many bugfixes and code cleanup commits
- Set up automated doc generation with the results [hosted here](https://wisdem.readthedocs.io/en/latest/)
- [Created a script](https://github.com/WISDEM/WISDEM/blob/IEAontology4all/docs/_utils/convert_docstrings.py) to parse WISDEM components and automatically produce docstrings to increase user understanding of the code. These docstrings live in the actual component files and are also automatically rendered on the documentation site. For example, [here is the page for the Tower component in WISDEM](https://wisdem.readthedocs.io/en/latest/wisdem/towerse/documentation.html), showing the API documentation.

Although not a direct measure of value-add, I have been able to jump into WISDEM and contribute to the code from Day 1.
The graph below shows that I have made the second-most commits to WISDEM in the past month.

<p align="center">
  <img src="github_wisdem_commits" alt="Contributions to WISDEM" width="500"/>
</p>

## BAR tower redesign

I optimized the tower used in BAR studies to meet design constraints and lower overall LCOE.

Because BAR was mostly focused on rotor and blade design, they were using a placeholder tower with linear taper and a 10 meter base diameter.
However, that original tower did not meet buckling and frequency constraints, and its 10 meter diameter prevented it from being easily transportable.
To both obtain a better tower design and help get me accustomed to useing WISDEM, I design and performed a series of studies with different design constraints to understand the design space and provide BAR with a more reasonable tower design.
Pietro and Garrett helped me formulate and interpret these studies.

The image below shows a comparison of optimal tower designs, highlighting which design are feasible.
This figure, more studies, and what it means for the BAR project are contained in this slide deck I made and presented to the BAR group.
The BAR team is moving forward using the optimized 6 meter base diameter tower, which gives their trade studies more meaningful LCOE values.

<p align="center">
  <img src="BAR_tower_redesign" alt="Optimized BAR towers" width="500"/>
</p>

## IEA Task 37 layout optimization

I'm currently working with Chris Bay on performing turbine layout optimization with multiple discrete concave regions.
This is part of the IEA Task 37 comparison challenge and [my code is hosted here](https://github.com/johnjasa/iea37_case_study/tree/autograd/cs3-4).

I've implemented a hybrid-nested optimization strategy that uses a gradient-free genetic algorithm to choose the number of turbines to place in each region, then uses a gradient-based local optimization method to fine-tune the placement of the turbines.
This results in the highest AEP values reported for this problem yet using a method that can run on a laptop instead of a supercomputer.

Here is a preliminary result

