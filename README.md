# IFEP — Integrated Fast Evolutionary Programming

<p align="center">
  <img src="IFEP_logo.png"
       alt="IFEP — Automated Material Identification"
       width="720">
</p>

<p align="center">
  <strong>Automated Material Identification</strong><br>
  An Integrated Fast Evolutionary Programming Framework
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Language-MATLAB-blue" alt="MATLAB">
  <img src="https://img.shields.io/badge/Application-Material%20Identification-orange" alt="Material Identification">
  <img src="https://img.shields.io/badge/Status-Research%20Software-lightgrey" alt="Research Software">
</p>

<!-- Add the Zenodo DOI badge here after the first public release. -->

> **Research software:** IFEP is developed for automated material-parameter identification in nonlinear constitutive models. Users should independently validate numerical results before applying them to engineering decisions.

---

## Overview

**IFEP (Integrated Fast Evolutionary Programming)** is a MATLAB-based computational framework for automated identification of material parameters in nonlinear constitutive models.

The framework employs an extended evolutionary programming architecture to solve inverse identification problems using experimental material-response data. Its implementation combines population-based search, multiple mutation strategies, adaptive parameter handling, diversity preservation, and elitist selection mechanisms.

The accompanying research describes the application of this architecture to the identification of entropy-based creep constitutive-model parameters from experimental creep histories.

The principal objective of IFEP is to provide an efficient and adaptable computational framework for material identification, particularly for nonlinear constitutive models involving multiple interacting parameters.

## Main Features

The current implementation and accompanying research manuscript describe the following capabilities:

- **Automated material identification:** Optimization of material parameters using experimental response data.
- **Bounded parameter search:** Identification within prescribed physical parameter limits.
- **Parameter normalization:** Linear and logarithmic parameter transformations.
- **Multi-strategy evolutionary search:** Gaussian and/or Cauchy mutation strategies.
- **Adaptive mutation:** Dynamic handling of mutation-step parameters.
- **Population diversity:** Random-immigrant mechanisms to support exploration.
- **Restart mechanisms:** Strategies intended to mitigate premature convergence and stagnation.
- **Elitist selection:** Preservation of high-quality candidate solutions and the best solution found.
- **Response-based fitness evaluation:** Including the shortest sampled-distance (SSD) objective described in the accompanying manuscript.
- **Model-specific configuration:** Parameter bounds, transformations, and optimization settings for supported constitutive models.

The exact functionality available in a public release depends on the complete set of MATLAB source files and dependencies included in that release.

## Repository Structure

The recommended repository organization is:

```text
IFEP/
│
├── README.md
├── USER_GUIDE.md
├── CITATION.cff
├── LICENSE
├── CHANGELOG.md
├── .gitignore
│
├── IFEP_logo.png
│
├── src/
│   └── MATLAB source files and dependencies
│
├── examples/
│   └── Example input files and scripts
│
├── data/
│   └── Distributable experimental datasets
│
└── results/
    └── Selected example outputs
```

Only include experimental datasets and other materials that you have permission to redistribute.

## Requirements

- MATLAB.
- All MATLAB helper functions and dependencies called by the main program.
- Any required MATLAB toolboxes or external functions.

The minimum MATLAB release and toolbox requirements have not yet been verified. These should be established and documented before the first public release.

## Getting Started

1. Clone or download the complete IFEP repository.
2. Open the repository root directory in MATLAB.
3. Add the source directory and all required subdirectories to the MATLAB path.
4. Read `USER_GUIDE.md` for information about configuration, input data, and execution.
5. Place the required experimental input files in the appropriate data directory or update the paths in the configuration.
6. Verify that all required MATLAB functions and input files are available.
7. Run a small test case before performing a full parameter-identification analysis.
8. Examine the optimization results and compare the identified material response with the experimental data.

The currently supplied main script refers to a folder named `2-EXP_Mat_Entropy_Strain_folder`, calls `FE8_Run_Sterategy_Loop`, and subsequently performs post-processing. These names and paths should be checked against the final public source distribution.

## Constitutive Models and Configuration

The supplied configuration currently selects the **Zajkani–Khonsari model** by default and includes other model-specific branches.

The configuration framework provides model-dependent settings, including:

- Material-parameter bounds.
- Parameter normalization and denormalization.
- Fitness-function settings.
- Mutation and evolutionary-strategy options.
- Population diversity and restart settings.

A constitutive model should be considered supported in a public release only when its forward model, fitness evaluation, parameter mapping, required input data, and associated dependencies are included and tested.

Parameter bounds and transformations are important components of the inverse identification problem. Any changes to these settings should be documented when reporting identified parameters.

## Reproducibility

Evolutionary optimization is stochastic. Reproducibility therefore requires documenting the computational environment and optimization settings.

For each identification analysis, users should record:

- IFEP version or Git commit.
- MATLAB release and operating system.
- Constitutive model and model configuration.
- Experimental dataset and preprocessing procedure.
- Parameter bounds and normalization choices.
- Population size and maximum number of generations.
- Mutation, adaptation, diversity, and restart settings.
- Random-number-generator seed, if supported and fixed by the implementation.
- Best objective-function value and identified parameters.
- Comparison plots between experimental and identified material responses.

Where possible, repeat optimization runs using different random seeds. A low objective-function value alone does not establish parameter uniqueness or physical identifiability.

## Data Availability

Experimental datasets are not necessarily included in the software repository.

Users should ensure that they have permission to redistribute any experimental data, figures, or supplementary materials. Where redistribution is restricted, the original data source should be cited and the procedure for obtaining authorized access should be explained.

## Citation

If you use IFEP in academic research, please cite the associated research publication and the specific software release used in your work.

The software will be archived through **Zenodo**, providing a permanent Digital Object Identifier (DOI) for reproducibility and citation.

**GitHub repository:** [Insert public repository URL]

**Zenodo DOI:** [To be added after the first public release]

A `CITATION.cff` file is provided to facilitate software citation. Its metadata should be completed before publication.

## License

The software license will be specified in the `LICENSE` file.

The selected license must be consistent with the rights of the authors, co-authors, institution, sponsors, and any third-party software included in the distribution. Do not treat a placeholder or license-selection note as a final license.

## Disclaimer

IFEP is research software provided for scientific and computational research.

Users are responsible for independently verifying numerical implementation, constitutive assumptions, experimental input data, parameter identifiability, and the suitability of the results for their intended applications.

No warranty is provided except as expressly stated in the selected software license.

## Contributions and Contact

Contributions, suggestions, and reports of reproducible software issues are welcome.

Bug reports should include:

- IFEP version or Git commit.
- MATLAB release and operating system.
- Relevant model configuration.
- Error message and associated MATLAB function.
- A minimal reproducible example, where possible.

**Software:** IFEP — Integrated Fast Evolutionary Programming  
**Application:** Automated Material Identification  
**Maintainer:** Asghar Zajkani  
**Contact:** zajkani@eng.ikiu.ac.ir
