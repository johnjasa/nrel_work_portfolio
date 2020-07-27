## Contributions to WEIS

As part of the [ARPA-E Atlantis program](https://arpa-e.energy.gov/?q=arpa-e-programs/atlantis), NREL is developing [WEIS, the Wind Energy with Integrated Servo-control toolset](https://www.nrel.gov/news/program/2019/best-of-both-worlds.html).
For this project, I serve as an optimization methods and implementation expert as we adapt tools to be better suited for efficient design optimization.
Expanding the toolset's capabilities include developing efficient derivative computation methods to enable gradient-based optimization, adding new optimization methods to the stack, and examining the best optimization problem architectures.

### Implementing multifidelity optimization methods

- Introduce multifidelity methods and why we want them
- Show the three-level WISDEM chart
- Show example output for 1-D function
- Explain WISDEM and OpenFAST couplings
- Show results from two-chord blade optimization, paste table from teams
- I'm working these efforts into a paper

### Introducing new optimization drivers to WISDEM and OpenMDAO

- Update the NLopt links here
- Explain the path forward on Dakota

### WISDEM documentation and code quality improvement

- Contributed to many bugfixes and code cleanup commits
- Introduced Coveralls to show where we need to improve testing
- Added docs throughout, link to them here

## IEA Task 37 layout optimization

This is a continuation of the work [I originally presented here](https://github.com/johnjasa/nrel_work_portfolio/tree/master/2020_04-05#iea-task-37-layout-optimization).

- We've written our sections in the joint paper
- Will now examine an extension into another paper on layout optimization comparing these methods
- The methods will be implemented and documented in FLORIS