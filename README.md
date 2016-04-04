# BSX
This repository contains model definitions, scripts and data used in the paper
[Modelling confounding effects from extracerebral contamination and systemic factors on functional near-infrared spectroscopy][bsx1].

## Models
The `models` directory contains model definitions in [BCMD][bcmd] format.
The main model from the paper is in the `bsx.modeldef` file.
The file `bsx_pulse.modeldef` defines a variant that generates its own internal stimulus pulse
instead of expecting inputs; this is for use with the optimisation scripts below.

The definition files in the top-level `models` directory are fully self-contained.
Because there is a great deal of overlap between both of these and many earlier models,
actual model development was performed using definitions decomposed into multiple files,
with the shared details referenced from various master files. For completeness, all these
files included in the `decomposed` subdirectory. These files are not required to build
the models and their structure is somewhat opaque, so for most purposes it is probably
simpler to just use the self-contained versions.

## Data
The `data` directory contains simulated and experimental data used in the paper, arranged
into several subdirectories. Within each data set, the `input` directory includes the model
input files used to drive the simulations, while the `out` directory contains the simulation
results. Unless otherwise noted, inputs are for use with the main `bsx` model. The individual
subdirectories are listed below in the order their contents are used in the text.

### sim/bsx_compare
Steady state simulations for variations in single parameters, for the BSX model, and also for the
original BrainSignals and the 2015 variant B1M2 (implementations of both models can be found
in the neighbouring [BrainSignals Revisited][bsrv] repository). Results are presented in
Figure 2.

### sim/basic
Simulated single and joint haemodynamic responses, as shown in Figures 3 & 4.

### sim/false_opt
Optimised false positive and false negative examples, as shown in Figure 5. These input files
are for use with the `bsx_pulse` model rather than the main `bsx` model. They set parameters
defining step changes in the driving signals rather than supplying those
signals directly.

### sim/false
Quasi-steady state simulations with varying levels of both arterial pressure and CO2, as
used in Figure 6. In `pc.input`, systemic variables are changed with no change in demand,
potentially giving rise to false positive results. In `pcu.input`, systemic variable changes
occur alongside demand changes, potentially giving rise to false negative results.

### fs_2013
Grouped data from Scholkmann et al 2013, as used in section 3.3, Figure 7. Original data as supplied
are in the `excel` directory. Results from the four different challenges are collated in CSV form in
the `csv` subdirectory, which also contains the same data upsampled to 1 Hz by linear interpolation.
Simulation input and output files are included for the three different cases considered: file names
ending in `_u` include a synthetic demand input (Figure 7B), those ending in `_c` include measured CO2
as an input (Figure 7C) and those ending in `_uc` include both (Figure 7D).

### ck_2012
Individual data from Kolyva et al 2012, as used in section 3.4, Figures 8-10. Original data as supplied
(already resampled) is in the `csv` subdirectory. For each subject (S1-S8) there are separate A and B
files for the left and right hemispheres. Channel A was used for all simulations. Global data are
present in both files, but of course are identical for both channels.


## Optim
The `optim` directory contains optimisation jobs and target data for the false positive and false negative
results presented in Figure 5 of the paper. These can be executed via the `optim.py` script in the [BCMD][bcmd]
distribution (which in turn depends on the [OpenOpt](openopt) library). They require that the `bsx_pulse` model
has been built and is available to `optim.py` (typically in the `build` directory).

[![DOI](https://zenodo.org/badge/11938/bcmd/bsx.svg)](https://zenodo.org/badge/latestdoi/11938/bcmd/bsx)

[bcmd]: https://github.com/bcmd/BCMD
[bsx1]: https://github.com/bcmd/bsx
[bsrv]: https://github.com/bcmd/bsrv
[r]: http://www.r-project.org
[openopt]: http://openopt.org
