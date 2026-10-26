# IFEP — Integrated Fast Evolutionary Programming

> **Research software.** Validate numerical results independently before using them for engineering decisions.

IFEP (Integrated Fast Evolutionary Programming) is a MATLAB-based framework for evolutionary identification of material parameters in nonlinear constitutive models. The supplied implementation includes model configuration, parameter bounds and transformations, and an evolutionary strategy loop. The accompanying research manuscript describes an extended evolutionary architecture for identifying entropy-based creep constitutive-model parameters from experimental creep histories.

## Main capabilities

The current code and manuscript describe a framework combining:

- Bounded material-parameter identification.
- Linear and logarithmic parameter transformations.
- Population-based search with Gaussian and/or Cauchy mutation strategies.
- Adaptive mutation-step handling.
- Diversity support through random immigrants.
- Restart mechanisms intended to mitigate stagnation.
- Elitist survivor selection and preservation of the best solution found.
- Response-based fitness evaluation, including a shortest sampled-distance (SSD) objective described in the manuscript.
- Model-specific configuration for supported constitutive models.

**Note:** The exact capabilities available in a public release depend on the complete set of MATLAB source files included. This documentation does not by itself establish that the repository is a complete, runnable distribution.

## Recommended repository structure

```text
IFEP/
├── README.md
├── USER_GUIDE.md
├── LICENSE
├── CITATION.cff
├── CHANGELOG.md
├── .gitignore
├── src/                 # MATLAB source files and dependencies
├── examples/            # Small, distributable example inputs and scripts
├── data/                # Only data you have permission to redistribute
└── results/             # Optional small example outputs; avoid large raw outputs
```

## Requirements

- MATLAB.
- All MATLAB helper functions called by the main script and other functions.
- Any required MATLAB toolboxes or external functions, once identified from the complete codebase.

The minimum MATLAB release and toolbox requirements have not yet been verified. Before publishing, test IFEP from a clean MATLAB session and record the MATLAB release, operating system, and toolbox requirements.

## Getting started

1. Clone or download the complete IFEP repository.
2. Open the repository root in MATLAB, or add the complete source tree and its subdirectories to the MATLAB path.
3. Read `USER_GUIDE.md`, especially the input-data and configuration sections.
4. Put required experimental input files in the expected data folder, or update the paths in the main script.
5. Confirm that all called MATLAB functions and input files are present.
6. Run a small test case before attempting a full calibration.
7. Inspect saved optimization results and compare the identified response against experimental curves.

The currently supplied main script refers to a folder named `2-EXP_Mat_Entropy_Strain_folder`, calls `FE8_Run_Sterategy_Loop`, and then performs post-processing. Verify these names and paths against the final source release.

## Constitutive models and configuration

The supplied configuration currently selects the **Zajkani–Khonsari model** by default and includes other model-specific branches. Use a model only when its forward model, fitness evaluation, parameter mapping, and required input data are included and tested.

Parameter bounds and transformations are part of the inverse problem. Changing them can affect the identified parameters and should be recorded with reported results.

## Reproducibility

For each calibration, record:

- IFEP version or Git commit.
- MATLAB release and operating system.
- Constitutive model and configuration.
- Input dataset identifiers and preprocessing.
- Parameter bounds and normalization choices.
- Population size, generation limit, and mutation/restart settings.
- Random-number-generator seed, if supported and fixed by the implementation.
- Best objective value, identified parameters, and comparison plots.

Evolutionary optimization is stochastic. Repeat runs with different seeds where possible. A low objective value alone does not establish that parameters are unique or physically identifiable.

## Data and publication ethics

Do not upload experimental datasets, figures, or supplementary material unless you have permission to redistribute them. Where data are restricted, cite the source and explain how authorized users can obtain them.

## Citation

If you use IFEP in academic work, cite the associated publication or preprint once its bibliographic details and public URL/DOI are confirmed. See `CITATION.cff` for a metadata template; replace all placeholders before release.

## License

Choose a license only after confirming that you have the authority to license the code and that co-author, institutional, sponsor, and third-party requirements are satisfied. Do not publish a placeholder or selection note as if it were a final license.

## Disclaimer

IFEP is research software. Users are responsible for checking numerical correctness, constitutive assumptions, input data, and suitability of results for their intended application. No warranty is provided except as expressly stated in the selected license.

## Contact and contributions

Before public release, add a maintainer contact and contribution policy. Bug reports should include the IFEP version or commit, MATLAB release, relevant configuration, error message, and a minimal reproducible example where possible.

Contact:

1 - Asghar Zajkani: zajkani@eng.ikiu.ac.ir
   Department of Mechanical Engineering, Faculty of Engineering, Imam Khomeini International University, Qazvin, Iran 
   
2 - Michael Khonsari: khonsari@lsu.edu
   Department of Mechanical and Industrial Engineering, Louisiana State University, Baton Rouge, LA, USA
