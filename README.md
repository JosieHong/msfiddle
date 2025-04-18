# msfiddle

[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa] (free for academic use) 

Source code for the FIDDLE PyPI package featuring:

* Chemical formula prediction from MS/MS spectra
* Formula refinement with confidence score estimation
* Seamless integration with BUDDY and SIRIUS tools

Preprint: https://doi.org/10.1101/2024.11.25.625316

For the complete experimenal codes, please visit the GitHub repository: https://github.com/JosieHong/FIDDLE

## Installation

```bash
# Install msfiddle (without PyTorch)
pip install msfiddle
```

To use `msfiddle`, you need to install `torch>=1.13.0,<2.0.0` separately with the appropriate version for your system. Please refer to the official PyTorch installation guide:
🔗 [PyTorch Installation Guide](https://pytorch.org/get-started/previous-versions/#v1130). 

## Usage 

**Step 1**: Download pre-trained models

```bash
# Download models to the default location (inside the package directory)
msfiddle-download-models

# Or specify a custom location and models
msfiddle-download-models --destination /path/to/models \
                          --models fiddle_tcn_qtof fiddle_fdr_qtof
```

**Step 2**: Run predictions

Using demo data (simplest option): 

```bash
# Run prediction with the built-in demo data
msfiddle --demo --result_path ./output_demo.csv --device 0
```

Using your own data:

```bash
# Run prediction with your data - automatically selects appropriate model
msfiddle --test_data /path/to/data.mgf \
         --instrument_type orbitrap \
         --result_path /path/to/results.csv \
         --device 0
```

The `--instrument_type` parameter can be either `orbitrap` (default) or `qtof`. 

Below is an example of input MS/MS data formatted in `.mgf`. The fields `TITLE`, `PRECURSOR_MZ`, `PRECURSOR_TYPE`, and `COLLISION_ENERGY` are required for msfiddle processing: 

```mgf
BEGIN IONS
TITLE=EMBL_MCF_2_0_HRMS_Library000529
PEPMASS=111.02016
CHARGE=1-
PRECURSOR_TYPE=[M-H]-
PRECURSOR_MZ=111.02016
COLLISION_ENERGY=50.0
SMILES=[H]c1c([H])n([H])c(=O)n([H])c1=O
FORMULA=C4H4N2O2
THEORETICAL_PRECURSOR_MZ=111.019453
PPM=6.368253318682487
SIMULATED_PRECURSOR_MZ=111.01946768634916
41.0148 0.329893 
41.9986 89.226766 
55.8055 0.200544 
56.2625 0.194617 
67.0304 0.330612 
68.0258 0.402906 
111.0203 100.0 
112.0515 1.2809 
END IONS
```

### Additional Options

Show all model paths:

```bash
msfiddle-checkpoint-paths
```

Advanced usage with custom paths:

```bash
msfiddle --test_data /path/to/data.mgf \
         --config_path /path/to/config.yml \
         --resume_path /path/to/tcn_model.pt \
         --fdr_resume_path /path/to/fdr_model.pt \
         --result_path /path/to/results.csv \
         --device 0
```

## Citation

```
@article{hong2024fiddle,
  title={FIDDLE: a deep learning method for chemical formulas prediction from tandem mass spectra},
  author={Hong, Yuhui and Li, Sujun and Ye, Yuzhen and Tang, Haixu},
  journal={bioRxiv},
  pages={2024--11},
  year={2024},
  publisher={Cold Spring Harbor Laboratory}
}
```

## License

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg