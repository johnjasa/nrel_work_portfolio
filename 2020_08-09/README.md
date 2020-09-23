## Contributions to WEIS

As part of the [ARPA-E Atlantis program](https://arpa-e.energy.gov/?q=arpa-e-programs/atlantis), NREL is developing [WEIS, the Wind Energy with Integrated Servo-control toolset](https://www.nrel.gov/news/program/2019/best-of-both-worlds.html).
For this project, I serve as an optimization methods and implementation expert as we adapt tools to be better suited for efficient design optimization.
Expanding the toolset's capabilities include developing efficient derivative computation methods to enable gradient-based optimization, adding new optimization methods to the stack, and examining the best optimization problem architectures.

### Continuing developing multifidelity optimization methods


### Introducing new optimization drivers to WEIS and OpenMDAO

Continuing the task within WEIS to introduce additional optimization libraries, I implemented a [wrapper for DAKOTA](https://github.com/WISDEM/WEIS/blob/master/weis/optimization_drivers/dakota_driver.py), which has a slightly different API due to DAKOTA requiring file IO to perform optimization.
This wrapper is slightly less full featured than the NLopt driver.
After running some performance benchmarks for representative optimization problems, we found that the DAKOTA optimizers performed at 2-3x the computational cost due to the additional overhead required for file IO.
This DAKOTA driver is useful for more expensive analyses or uncertainty-based optimization.

### WEIS code quality improvement
