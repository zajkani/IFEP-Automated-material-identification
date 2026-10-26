# IFEP User Guide

## 1. Purpose and scope

IFEP (Integrated Fast Evolutionary Programming) is a MATLAB framework for identifying parameters in nonlinear material constitutive models using evolutionary search. The supplied source files are organized around model configuration, parameter transformations, population initialization, mutation and population-management strategies, fitness evaluation, and post-processing.

The accompanying manuscript describes an extended fast evolutionary programming architecture and its application to entropy-based creep constitutive-model identification. This guide records the workflow visible in the supplied files. It does not claim that the currently supplied subset is a complete, independently runnable distribution.

## 2. Source files identified in the supplied set

- `FE_Main.m` — initializes settings, reads experimental MAT files, configures the model, selects material/data, runs the strategy loop, and invokes post-processing.
- `FE0_Config_Model.m` — defines default options and model-specific configuration, including parameter bounds, normalization types, fitness options, mutation settings, and restart/selection settings.
- `FE15_1_DenormalizeParameters.m` — maps normalized parameters back to physical values using model bounds and parameter-specific linear/logarithmic transformations.
- `FE8_Run_Sterategy_Loop.m` — contains the evolutionary strategy loop, including population initialization, mutation strategies, fitness evaluation, immigrant/restart handling, survivor selection, global-best tracking, and result saving.
- `Paper 5 - (FEPS) - V3.pdf` — research manuscript describing the method; rename or replace this file for the public release as appropriate.

The full code may call additional MATLAB functions that must also be included for a working release. Check all function calls and file-loading statements before publication.

## 3. Installation and folder setup

1. Install a compatible MATLAB release. The minimum supported release has not yet been established.
2. Clone or download the complete IFEP repository.
3. Keep all source files and helper functions in the documented folder structure.
4. Open the repository root in MATLAB, or add the complete source directory and its subdirectories to the MATLAB path.
5. Place authorized experimental `.mat` files in the expected input directory, or update the input path in the main script.
6. Run a small test case before a full calibration.

**Dependency check:** The supplied main script refers to `2-EXP_Mat_Entropy_Strain_folder`. Confirm the exact required filenames, MAT-file variable names, and any toolbox or external-function requirements from the complete codebase.

## 4. High-level execution workflow

The main script follows this sequence:

1. Initialize model-level settings, including population size and maximum generations.
2. Read experimental MAT files from the configured data directory.
3. Create or prepare output folders.
4. Configure the constitutive model through `FE0_Config_Model`.
5. Select the material and experimental curves.
6. Configure plotting and retrieve fitting data.
7. Nominate mutation scenarios.
8. Run the evolutionary search through `FE8_Run_Sterategy_Loop`.
9. Perform post-processing and inspect saved results.

Verify helper-function names and signatures against the complete repository. Do not remove or rename files without checking their callers.

## 5. Configuration

The principal configuration is in `FE0_Config_Model.m`.

### Algorithm controls

The supplied main script initializes `pop_size = 20` and `max_gen = 50`. The configuration includes `N_order`, thresholds, generation-diversity controls, mutation settings, restart settings, and selection strategy. These are source defaults, not universal recommendations.

### Constitutive-model selection

The supplied configuration currently selects `Zajkani-Khonsari model` by default. Other model branches are present. Select a model only if its forward model, fitness logic, parameter mappings, and required data are included and tested.

### Optimization space and parameter transformations

The active configuration uses normalized optimization space. Parameters may use linear or logarithmic transformations, with inverse mapping to physical values. The denormalization helper uses `model.bounds` and `model.normalized_parameters`; each transformation must match the intended physical parameter domain.

Logarithmic transformations require positive parameter values and positive bounds. Review these bounds before running the search.

### Fitness settings

The supplied configuration selects `sampled_distance` and enables normalized curve fitness. It also includes options related to strain-rate, angle, and end-time effects, along with weights and model-specific settings. Their exact meaning depends on the fitness implementation included in the full source tree.

### Mutation, diversity, and restart

The strategy loop supports Gaussian, Cauchy, or combined mutation scenarios, along with random immigrants, restart candidates, and elitist/diversity-based selection. These mechanisms are stochastic and can affect convergence and identified solutions.

## 6. Input data

The main script reads `.mat` files from `2-EXP_Mat_Entropy_Strain_folder`. Confirm the exact data schema from the loading and preprocessing functions before publishing.

Document the following for each supported model:

- Required file names and units.
- Required variables and array dimensions.
- How separate creep curves are represented.
- How stress, temperature, time, strain, strain rate, and rupture information are encoded, where applicable.
- Missing-data and interpolation rules.
- Preprocessing and exclusion rules.

Do not assume every field is required for every model; verify the actual data contract.

## 7. Running a calibration

1. Start with a small example case, once one has been included.
2. Confirm MATLAB can locate all source functions.
3. Confirm input data load and are interpreted correctly.
4. Verify the model selection and parameter bounds.
5. Use a modest population and generation count for an initial smoke test.
6. Run the main script.
7. Check the command window for errors and warnings.
8. Inspect generated plots and saved result files.
9. Repeat with different random seeds, if supported, to assess variability.
10. Run the full calibration only after the smoke test succeeds.

The current strategy loop saves files named `Strategy_plot.fig` and `Strategy_results.mat` in its output workflow. Confirm their exact locations and MAT-file fields in the final release.

## 8. Outputs and interpretation

For each run, retain the identified physical parameter values, best objective value, convergence history, experimental-versus-simulated plots, configuration and bounds, and random seed/software environment where available.

A single best fit does not establish parameter uniqueness. Strong parameter correlations, limited experimental coverage, and non-identifiability may allow different parameter sets to produce similar responses. Assess repeatability and independent responses where possible.

## 9. Troubleshooting

### MATLAB reports an undefined function

A helper file may be missing or outside the MATLAB path. Search the source tree for the function definition and add its directory to the path.

### Input MAT files are not found

Check the current working folder and the `2-EXP_Mat_Entropy_Strain_folder` path. Confirm the expected files exist and that the path is valid on your operating system.

### A parameter reaches a bound

Review the bounds, normalization type, data, and fitness function. A bound-hitting result can reflect a boundary optimum, poor identifiability, or a configuration/data problem; it should not automatically be accepted.

### Different runs return different parameter sets

Evolutionary algorithms are stochastic. Compare objective values and predicted responses, run multiple seeds, and assess identifiability rather than comparing parameters alone.

### A run fails during constitutive evaluation

Inspect the error message, parameter admissibility constraints, and input values. Confirm logarithms and other model operations receive valid arguments. Do not suppress numerical failures without understanding their cause.

## 10. Reproducibility checklist

Archive the IFEP commit hash, MATLAB release, data source and preprocessing, model selection, parameter bounds, normalization types, population size, generation limit, mutation/restart settings, random seed, best fitness, identified parameters, and response plots.

## 11. License and redistribution

Choose a license only after confirming authority to license the code and satisfying co-author, employer/university, sponsor, and third-party conditions.

- **MIT:** permissive reuse, including commercial use, subject to its terms.
- **BSD-3-Clause:** permissive reuse with an additional non-endorsement condition.
- **GPL-3.0:** requires compliance with copyleft conditions for covered redistributions.
- **No license:** public visibility alone does not grant broad permission to copy, modify, or redistribute the code.

This is general information, not legal advice. Do not publish a license file until the choice is deliberate.

## 12. Before public release

- [ ] Include all required MATLAB source files and helper functions.
- [ ] Test the repository from a clean clone.
- [ ] Add a minimal example input and documented run script.
- [ ] Verify MATLAB release and toolbox requirements.
- [ ] Remove local absolute paths, private data, credentials, and temporary outputs.
- [ ] Confirm permission to redistribute experimental data and figures.
- [ ] Choose and add the intended license.
- [ ] Complete `CITATION.cff` with the correct author, title, version, and DOI/URL.
- [ ] Add contact or issue-reporting instructions.
- [ ] Tag a versioned release after testing.
