## EMRI\_MC: A GPU-based code for Bayesian inference of EMRI waveforms

EMRI\_MC performs parameter inference for Extreme Mass Ratio Inspirals (EMRIs) based on the kludge formalism, including propagation effects due to modified gravity. It is designed to make use of GPU parallelisation for higher computational efficiency. For more information we refer to:  https://arxiv.org/abs/2311.17174

- [Authors](#Authors)
- [Installation](#Installation)
- [Modules](#Modules)
- [Execution](#Execution)

## Authors
The code was developed predominantly by Ippocratis D. Saltas and Roberto Oliveri, with the invaluable contributions of Stephane Ilic and Josef Dvoracek. 

## Modules

**global\_parameters.py**: This module defines the values of physical constants in cgs units, the parameters of the fiducial model, geometrical parameters and initial conditions of the binary system, parameters for the ODE solver (e.g., integration time window and grid resolution), and MCMC-related definitions. It also defines the maximum number of orbital overtones $n\_max$ in the computation of the waveform. A change in the number of the parameters in the MCMC requires adjusting the parameter vector in this module.  

**waveform.py**: This module defines the set of kludge ODE equations, the waveform generator, and some GPU-related functionality.

**mcmc.py**: This module defines the MCMC-related functions and the MCMC iterator.

**propagation.py**: This module defines the functions needed for the propagation of the GW wave through the cosmological background in the presence of any modified gravity effects. 

**run_code.py**: This module starts the MCMC run, building on the parameter definitions in check global_parameters.py.

**main.ipynb**: Assuming all parameters and fiducial values are properly defined as explained earlier, 
this Jupyter notebook calls the main functions to initiate the MCMC run, 
using the package $\texttt{emcee}$. As a simple choice, we have currently set throughout the numerical computation 
the source location $\{\theta_S,\phi_S\} = \{\pi/4, 0\}$, 
the orientation of the spin $\{\theta_K,\phi_K\} = \{\pi/8, 0\}$, 
$\alpha_{LSO} = 0$, the angle $\lambda = \pi/6$, 
the initial eccentricity $e_{LSO}=0.3$, and $\gamma_{LSO} = 0$, $\Phi_{LSO} = 0$, 
for the respective initial conditions. 
These can be straighforwardly modified in the code. 

## Installation 

On top of Python's usual **numpy** and **scipy** libraries, to run the code one needs the following modules: 

1. **cuda/cupy**: https://nvidia.github.io/cuda-python/install.html

2. **emcee**: https://emcee.readthedocs.io/en/stable/user/install/

3. **corner** or **seaborn** or anything similar: https://corner.readthedocs.io/en/latest/install/  https://seaborn.pydata.org/installing.html

The cuda/cupy library provides the GPU functionality, emcee is the library with the MCMC sampler, multiprocessing is needed for parallelisation, and the corner/seaborn for producing the corner plots. 


## Execution

Running the code is particularly simple. Placing all files in the same folder, and setting up all parameters as explained above, one starts the notebook main.ipynb, and executes the cells (the code can also be executed through the terminal). This notebook serves as an example - it first computes and plots the fiducial model, and then starts the MCMC run around the chosen fiducial. The MCMC results are stored in a text file, please make sure the path is defined appropriately. 
