# Event-based-neuron

This is the readme for the event-based modeling framework described in the manuscript titled 
Reproducibility of biophysical in silico neuron states and spikes from event-based partial histories.

To recreate the figures from this paper, begin by running the `init.sh` script to build the data directories and compile 
the mod files.
This script works for linux and Mac systems, modify this to work in Windows.

The data of this project is generated with the various scripts and script wrappers in `./scripts`. The figures themselves 
are generated within jupyter notebooks within `./notebooks` and saved in the figures folder `./figures`. All of which 
utilize code from the `./utils` directory.

## Python Requirements
- jupyter
- NEURON 8.2
- numpy
- scipy
- matplotlib


## Paper Figures
All figures of Cudone et al. 2023 can be reconstructed from the contents of this repository. 

- **Figure 1**: Generated using `notebooks/model_specs.ipynb`.

- **Figure 2**: Generated using `notebooks/spike_centered.ipynb`.

- **Figure 3**: data generated with `partial_history_setup.py` and `partial_history.py` within the scripts folder for the 
Hodgkin Huxley models, and `partial_history_WB_setup.py` and `partial_history_WB.py` within the scripts folder for the 
Wang Buzsaki models. Figures visualized within `notebooks/partial_history.ipynb`.

- **Figures 4 & 5**: data generated with `scripts/nst_distribution_evolution.py` and visualized within 
`nst_distribution_evolution_part1.ipynb`, `nst_distribution_evolution_part2.ipynb`, and 
`nst_distribution_evolution_part3.ipynb` in the notebooks directory.

- **Figures 6 & 7**: data generated with `scripts/nInputs.py` for the Hodgkin Huxley model and `scripts/nInputs_WB.py` for 
the Wang Buzsaki model, which utilize the wrappers `scripts/nInputs_wrapper.sh` and `scripts/nInputs_WB_wrapper.sh` 
respectively. Visualization is in `notebooks/nInputs_analysis.ipynb`.

- **Figures 8 & 9**: data generated with `scripts/nInputs_morpho.py`, wrapped by `scripts/nInputs_morpho_wrapper.sh`, and 
visualized in `notebooks/nInputs_analysis_morpho.ipynb`.

- **Figure 10**: data generated with `state_reconstruct_part1.py`, `state_reconstruct_part2.py`, and 
`state_reconstruct_part3.py` in the scripts directory. and visualized with `notebooks/state_reconstruction.ipynb`.

- **Figure 11**: TODO

- **Figure 12**: TODO

## Repository contents

### utils 
`HH.py`
Contains the HH point cell model as a python class used throughout the codebase.

`Morpho.py`
Contains the morphologically detailed CA1 pyramidal cell as a python class used throughout the codebase. This class uses neuroMorpho's cell morphology file (Ascoli et al. 2007) originally from the work of (Ishizuka et al. 1995). This file is contained in the resources directory in this repository. 

`Stimuli.py`
Contains python classes and functions to assist in stimuli generation throughout the codebase; maintains consistency with synaptic parameterizations. 


### scripts
runs much of the experiments and outputs data to be analyzed in the jupyter notebooks in ./notebooks

`nInputs.py`
Performs the nInputs experiment on the HH model using the event-based-neuron framework within NEURON. 
This generates the data necessary for Figure 6 and Figure 7
    
`nInputs_wrapper.sh`
Bash script to run the nInputs.py script with each of the HH point cell synaptic parameterizations. 

`nInputs_morpho.py`
Performs the nInputs experiment on the morphologically detailed CA1 pyramidal cell. This script produces the 
data responsible for Figure 8 and Figure 9.
        
`nInputs_morpho_wrapper.sh`
Bash script for running the nInputs_morpho.py script. 

`partial_history_setup.py`
Generates the stimuli and histories necessary to do the partial histories experiment in partial_history.py

`partial_history.py`
Performs the partial histories experiment responsible for Figure 3 using the stimuli and histories generated in partial_history_setup.py.
    
`nst_distribution_evolution.py`
Runs the simulations responsible for Figure 4 and Figure 5. 
    
`state_reconstruct_part1.py`
Runs an extended simulation of a conductance-based HH point cell for which to compare reconstructed state variables of the event-based analog to. 

state_reconstruct_part2.py
Models a cell using the event-based-framework and then reconstructs the state variables of given windows. 

`state_reconstruct_part3.py`
Calculates the errors between the conductance-based model's state variables and the analogous event-based state variable reconstructions. 

`state_reconstruct_morpho_part1.py`
Runs an extended simulation of a conductance-based morphologically detailed CA1 pyramidal cell for which to compare reconstructed state variables of the event-based analog to. 
        
    
### data
directory to store intermediate and output data from the python scripts. Internal directory structure for all analysis 
should be as follows and is instantiated with `init.sh`.
    
    ./nInputs
    ./nInputs_morpho
    ./nst_distribution_evolution
        ./results
        ./stimuli
    ./partial_history
        ./results
    ./state_reconstruct
        ./original_simulation_data
        ./reconstruction_data
    ./state_reconstruct_morpho
        ./original_simulation_data
    
        

### notebooks
holds all of the jupyter notebooks used to generate the figures in the manuscript.
`model_specs.ipynb`
Describes the model specifications for the HH model and its synaptic parameterizations used in the manuscript. 
Generates table 1 and Figure 1.
    
`spike_centered.ipynb`
Includes the spike centered experiment. Generates table 2 and Figure 2.

`partial_history.ipynb`
Figure 3
NEEDS TO BE CLEANED UP

`nst_distribution_evolution_part1.ipynb`
Figure 4

`nst_distribution_evolution_part2.ipynb`
Figure 5 (part)

`nst_distribution_evolution_part3.ipynb`
Figure 5 (part)
NEEDS TO BE CLEANED UP

`nInputs_analysis.ipynb`
Figure 6, Figure 7

`nInputs_analysis_morpho.ipynb`
Figure 8, Figure 9

`state_reconstruction.ipynb`
Figure 10
NEEDS TO BE CLEANED UP

`state_reconstruction_morpho.ipynb`
Figure 11, Figure 12
        
        
### mod
`nInputs.mod`
Custom mod file to integrate event-based partial history input encodings in to NEURON, for the.

`morpho_nInputs.mod`
Custom mod file to integrate event-based partial history input encodings in to NEURON, for the morphologically detailed CA1 pyramidal cell.

`Nap.mod`
Passive Sodium channel used in the dendrites for the CA1 pyramidal cell. Derived from Magistretti & Alonso 1999.

`vecevent.mod`
NOT SURE IF WE USE THIS ANYMORE, CHECK!



### Morphology
`c91662.CNG.swc`
The CA1 pyramidal cell morphology file. Downloaded from https://neuromorpho.org/neuron_info.jsp?neuron_name=c91662 (Ascoli et al. 2007). Morphology originally from the work of (Ishizuka et al. 1995)
    
        
    
    
