## Contributions to WEIS

As part of the [ARPA-E Atlantis program](https://arpa-e.energy.gov/?q=arpa-e-programs/atlantis), NREL is developing [WEIS, the Wind Energy with Integrated Servo-control toolset](https://www.nrel.gov/news/program/2019/best-of-both-worlds.html).
For this project, I serve as an optimization methods and implementation expert as we adapt tools to be better suited for efficient design optimization.
Expanding the toolset's capabilities include developing efficient derivative computation methods to enable gradient-based optimization, adding new optimization methods to the stack, and examining the best optimization problem architectures.

### Creating and curating the WEIS repo

We have created the [WEIS repository](https://github.com/WISDEM/WEIS) which holds all code developed as part of WEIS as well as the NREL-developed dependencies, like WISDEM and OpenFAST.
All of my multifidelity and optimization driver work now lives within this WEIS repo.
To minimize activation energy, we've made it so the entire toolset can be installed using `python setup.py develop`, which makes WEIS a one-stop-shop.
We continue to refine the codebase and make it easier for users and developers to understand.

### Continued multifidelity work

I continued my multifidelity optimization work by presenting to the WEIS team about my progress detailed in the previous reporting period.
This opened up a lot of conversations about how best to use these methods, which models we should optimize, and how the CCD and integration subtasks can work together.
Specifically, I've had discussions with CCD team members and now attend the CCD meetings to keep everyone on the same page.
This work is ongoing and will continue now that we better understand each team member's role.

At the same time, I am focusing my efforts in developing a journal paper on this multifidelity work.
Continued discussions have **focused my priorities to developing a set of aerodynamic and aerostructural blade design problems for this paper**.
I have successfully set up the CCBlade and AeroDyn multifidelity cases on the HPC system Eagle and can now run cases for this paper.
It's a continual effort to analyze and refine the optimization problems as we increase model and optimization problem complexity.

### Introducing new optimization drivers to WEIS and OpenMDAO

Continuing the task within WEIS to introduce additional optimization libraries, I implemented a [wrapper for DAKOTA](https://github.com/WISDEM/WEIS/blob/master/weis/optimization_drivers/dakota_driver.py), which has a slightly different API due to DAKOTA requiring file IO to perform optimization.
This wrapper is slightly less full featured than the NLopt driver.
After running some performance benchmarks for representative optimization problems, we found that the DAKOTA optimizers performed at 2-3x the computational cost due to the additional overhead required for file IO, which suggests **DAKOTA is not useful for most of our use cases**.
This DAKOTA driver is useful for more expensive analyses or uncertainty-based optimization.

Completion of this DAKOTA driver, along with the NLopt driver, marks **a completed deliverable for the WEIS project**.

## Miscellaneous tasks completed

We recently released an updated version of WISDEM to the develop branch, based on the IEAontology4all branch.
This features many updates to functionality and code reorganization that are necessary for WEIS capabilities.
I focused on developing documentation and testing, as well as updating the OpenMDAO usage within WISDEM to use the latest syntax to simplify the codebase.

I recently attended the IEA Task 37 annual meeting to stay up-to-date with the group's progress in multiple work packages.
Our results from the layout optimization problem presented previously were presented and discussed.

I am preparing NREL's contribution for the 2020 OpenMDAO workshop, which is posed as a ["reverse hackathon" this year.](https://openmdao.org/2020-openmdao-reverse-hackathon/)
We will submit a study on using nested optimization techniques, which are common within WISDEM and WEIS, and receive expert feedback from the OpenMDAO dev team about the best way to structure these problems.
