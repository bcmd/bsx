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
TODO

## Optim
The `optim` directory contains optimisation jobs and target data for the false positive and false negative
results presented in Figure 5 of the paper. These can be executed via the `optim.py` script in the [BCMD][bcmd]
distribution (which in turn depends on the [OpenOpt](openopt) library). They require that the `bsx_pulse` model
has been built and is available to `optim.py` (typically in the `build` directory).

[bcmd]: https://github.com/bcmd/BCMD
[bsx1]: https://github.com/bcmd/bsx
[r]: http://www.r-project.org
[openopt]: http://openopt.org
