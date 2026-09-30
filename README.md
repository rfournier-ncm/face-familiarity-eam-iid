# Individual differences computational processes in face recognition

**Authors:** Raphaël Fournier, Paul Downing & Richard Ramsey

**Preprint:** \[link\]

**Status:** \[under review\]

------------------------------------------------------------------------

## Overview

## This project contains the raw data, analysis code and manuscript for a the study examining individual differences in computational processes involved in face recognition using evidence accumulation modelling (LBA). Since the model objects are too big to be uploaded on github, model objects can be found in this OSF project: \[link OSF\]

## Workflow components

- [renv](https://rstudio.github.io/renv/articles/renv.html) for R package version management
- [git](https://git-scm.com/) / [GitHub](https://github.com/) for version control and sharing
- [Tidyverse](https://www.tidyverse.org/) for data wrangling and visualisation
- [EMC2](https://github.com/ampl-psych/EMC2) for LBA evidence accumulation modelling
- [Quarto](https://quarto.org/) for reproducible scripts and manuscript rendering
- [preprint-typst](https://github.com/mvuorre/preprint) Quarto extension for manuscript formatting

------------------------------------------------------------------------

## Getting started

1.  Clone or download the repository to your local machine.
2.  Open `face-familiarity-eam-idd.Rproj` — renv will automatically bootstrap itself.
3.  Run `renv::restore()` to install all packages at the recorded versions.
4.  You can now run any of the `.qmd` scripts within each experiment folder.

> **Note on parallel model fitting (macOS Apple Silicon):** R 4.x on macOS aarch64 defaults to Apple's vecLib BLAS, which breaks `mclapply`-based parallelism used by EMC2. To enable parallel fitting, switch to standard BLAS in terminal:
>
> ``` bash
> sudo ln -sf libRblas.0.dylib libRblas.dylib
> ```
>
> (in `/Library/Frameworks/R.framework/Resources/lib/`). To revert: `sudo ln -sf libRblas.vecLib.dylib libRblas.dylib`. Alternatively, set `cores_per_chain = 1` (slow but works without the fix).

------------------------------------------------------------------------

## Data availability

Raw data and fitted model objects are available via this GitHub repo (link) or via the OSF (link). Large files are posted on the OSF and can be downloaded directly via the scripts below whenever necessary. ---

## Repository structure

```         
face-familiarity-eam-iid/
├── code/                         # Folder containing the different analyses script
│   ├── wrangle.qmd               # Reads raw data, applies exclusions, wrangles into analysis-ready format
│   ├── lba_model.qmd             # Fits the confirmatory LBA model(s) using EMC2
│   ├── lba_effects.qmd
│   ├── corr.qmd                  # Fits the confirmatory LBA model(s) using EMC2
│   └── iid_model.qmd             # Fits the confirmatory LBA model(s) using EMC2
│   └── iid_effects.qmd           # Fits the confirmatory LBA model(s) using EMC2
│   └── exploratory_analysis.qmd  # Fits the confirmatory LBA model(s) using EMC2
├── data/                         # Data folder with every data file used in the analysis
│   ├── raw/                      # Data folder containing the raw data files
│   ├── model/                    # Folder containing the different LBA modelling data files
├── figures/                      # Folder with every figures computed from the analysis
│   ├── corr/                     # Folder with correlations figures created with corr.qmd file
│   ├── descriptive/              # Folder with correlations figures created with wrangle.qmd file
│   ├── iid_ppred/                # Folder with correlations figures created with iid_effects.qmd file
│   └── lba/                      # Folder with correlations figures created with lba_effects.qmd file
│   └── exploratory/              # Folder with correlations figures created with exploratory_analysis.qmd file
├── manuscript/                   # Manuscript and supplementary files
│   ├── manuscript.qmd            # Quarto document of manuscript
│   ├── manuscript.pdf            # Manuscript format .pdf
│   ├── manuscript.html           # Manuscript format .html
│   ├── manuscript.docx           # Manuscript format .docx
│   ├── supplementary.qmd         # Quarto document of supplementary materials
│   ├── supplementary.pdf         # Supplementary materials format .pdf
│   ├── bibliography.bib          # Manuscript bibliography .bib
│   ├── supp-bibliography.bib     # Supplementary materials bibliography .bib
│   ├── apa.csl                   # .csl file for rendering the manuscript citations/references style to APA
│   └── figures/                  # Folder containing the .png figures used in the manuscript
├── models/                       # Folder containing the model objects created in lba_model.qmd and iid_model.qmd
│   ├── lba/                      # Folder containing the LBA model object and the posterior distributions
│   ├── iid/                      # Folder containing the preregistered Bayesian linear regression models and the exploratory ones
├── _extensions/             # preprint-typst Quarto extension
├── _freeze/                 # Quarto freeze cache (manuscript)
├── docs/                    # Rendered manuscript output
├── renv/                    # renv infrastructure
├── renv.lock                # Package version lockfile
├── _quarto.yml              # Project-level Quarto config
└── face-familiarity-eam-iid.Rproj
```

------------------------------------------------------------------------

### Data files (`data/`)

| File | Contents |
|-----------------------------|-------------------------------------------|
| `raw/` | Data folder containing the raw data files (1 per subjects) |
| `model/` | Data folder containing the posterior distributions of the LBA model |
| `corr/` | Data folder containing the data frame used for the plausible value correlations|
| `raw_data.csv` | Concatenated raw trial-level data |
| `data.csv` | Processed, analysis-ready data |
| `demo.csv` | Raw demographic data |
| `exclusions.csv` | Participant exclusion log |
| `cambridge_scores.csv` | Cambridge face and car accuracy data (after exclusions) |
| `cambridge_acc_scores_pid.csv` | Cambridge face and car accuracy data (after exclusions) at the pid level|

### Model objects (`models/`)
| File | Contents |
|-----------------------------|-------------------------------------------|
| `lba/` | Data folder containing the LBA model object and the posterior predictions object |
| `iid/b1_drift_face.rds` | Model object for drift rate predicted by face scores |
| `iid/b1_thresh_face.rds` | Model object for threshold predicted by face scores |
| `iid/b2_drift_car.rds` | Model object for drift rate predicted by face and car scores |
| `iid/b2_thresh_car.rds` | Model object for threshold predicted by face and car scores |
| `iid/b3_drift_face.rds` | Model object for drift rate predicted by car scores |
| `iid/b3_thresh_car.rds` | Model object for threshold predicted by car scores |


## Manuscript

The manuscript is written in Quarto (`manuscript/manuscript.qmd`) using the [preprint-typst](https://github.com/mvuorre/preprint) extension. Supplementary materials are in `manuscript/supplementary.qmd`. References are managed via `manuscript/bibliography.bib` for the manuscript and `manuscript/supp-bibliography.bib` for the supplementary materials.

Rendered outputs are written to `manuscript/` and can be viewed without re-running the analyses.

To render the manuscript locally:

``` bash
quarto render manuscript/manuscript.qmd
```

------------------------------------------------------------------------

## How to reproduce the full workflow

Run scripts in this order:

1.  `wrangle.qmd` — process raw data
2.  `lba_model.qmd` — fit confirmatory LBA model *(slow; run chunk by chunk)*
3.  `lba_effects.qmd` — extract estimates and generate figures
4.  `corr.qmd` — compute correlations between the LBA parameters and the Memory scores
5.  `iid_model.qmd` — fit Bayesian linear regression models
6.  `iid_effects.qmd` — extract estimates, compute posterior predictions of the regression models and create figures
7.  `exploratory.qmd` — analyse and create figures of the exploratory analyses

Then render the manuscript:

6.  `quarto render manuscript/manuscript.qmd`

> Model fitting scripts are not designed to be run end-to-end in one go due to long runtimes. Run them chunk by chunk.
