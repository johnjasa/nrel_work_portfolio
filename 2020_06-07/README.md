## Contributions to WEIS

As part of the [ARPA-E Atlantis program](https://arpa-e.energy.gov/?q=arpa-e-programs/atlantis), NREL is developing [WEIS, the Wind Energy with Integrated Servo-control toolset](https://www.nrel.gov/news/program/2019/best-of-both-worlds.html).
For this project, I serve as an optimization methods and implementation expert as we adapt tools to be better suited for efficient design optimization.
Expanding the toolset's capabilities include developing efficient derivative computation methods to enable gradient-based optimization, adding new optimization methods to the stack, and examining the best optimization problem architectures.

### Efficient derivative computation study

I set up and ran multiple computational experiments to benchmark different ways to compute derivatives for WISDEM, with the [results hosted here](https://github.com/johnjasa/derivative_comparisons).

Large portions of [WISDEM](https://github.com/WISDEM/wisdem) lack efficient derivative calculations, which would speed up gradient-based optimization.
This comparison study aimed to benchmark derivative computation methods that are relevant to WISDEM to determine their feasibility and utility.

I found that depending on the size of the inputs and outputs to the component, as well as the underlying code complexity, automatic differentiation may be a reasonable solution.
Analytic derivatives were always the fastest in terms of computational time, but required much more developer time, so they should be implemented only for extreme bottlenecks within the codebase.
The figure below shows an example of how the computational cost of different derivative computation methods scale with the number of inputs to the component.

<p align="center">
  <img src="total_derivs_num_inputs.png" alt="Derivative cost scaling with number of inputs" width="650"/>
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

## IEA Task 37 layout optimization

This is a continuation of the work [I originally presented here](https://github.com/johnjasa/nrel_work_portfolio/tree/master/2020_04-05#iea-task-37-layout-optimization).

I'm currently working with Chris Bay on performing turbine layout optimization with multiple discrete concave regions.
This is part of the [IEA Task 37 comparison challenge](https://github.com/byuflowlab/iea37-wflo-casestudies/blob/master/cs3-4/iea37-cs3-announcement.pdf) and [my code is hosted here](https://github.com/johnjasa/iea37_case_study/tree/autograd/cs3-4).

I've implemented a hybrid-nested optimization strategy that uses a gradient-free genetic algorithm to choose the number of turbines to place in each region, then uses a gradient-based local optimization method to fine-tune the placement of the turbines.
This method can be run on a laptop instead of a supercomputer.
The XDSM flowchart for the optimization process is shown below.

<p align="center">
  <img src="layout_opt_formulation.png" alt="XDSM for layout optimization process" width="800"/>
</p>

Here is a preliminary result showing the initial and final AEP values.
Our optimization method currently produces results that have higher AEP values than other researchers' methods within the task.

<p align="center">
  <img src="case_810.png" alt="Optimized layouts for discrete regions" width="700"/>
</p>
