# README.md `BM214-Workshop-3`

This repository contains the Quarto book for BM214 (Being a Biomolecular Scientist) Workshop 3:

## Notes on delivery

### Individualised student data

In this workshop, students are assigned to sessions (AM or PM) and  groups ("lab bays"), and are given individualised IDs. Each student gets a potentially unique sequence and data file, as indicated below.

```bash
% tree sequences                                                                                                           [4:20:46]
sequences
├── AM_Bay_01
│   ├── AM_Bay_01_CD.fasta
│   ├── AM_Bay_01_FD.fasta
│   ├── AM_Bay_01_TB.fasta
│   └── AM_Bay_01_TF.fasta
├── AM_Bay_02
│   ├── AM_Bay_02_CD.fasta
│   ├── AM_Bay_02_FD.fasta
│   ├── AM_Bay_02_TB.fasta
│   └── AM_Bay_02_TF.fasta
[...]
```

```bash
% tree data                                                                                                                [4:20:53]
data
├── AM_Bay_01
│   ├── AM_Bay_01_01.csv
│   ├── AM_Bay_01_02.csv
│   ├── AM_Bay_01_03.csv
│   └── AM_Bay_01_04.csv
├── AM_Bay_02
│   ├── AM_Bay_02_01.csv
│   ├── AM_Bay_02_02.csv
│   ├── AM_Bay_02_03.csv
│   └── AM_Bay_02_04.csv
```

These data files are generated using the Jupyter notebooks provided in the `scripts` subdirectory.

- `generate_16S_datasets.ipynb`: generates data in `assets/sequences` for each lab bay (separate subdirectories) - these are random choices from example 16S marker sequences for four bacteria; each of the four people in a lab bay gets one of the organisms.
- `generate_reporter_data.ipynb`: generates data in `assets/data/reporter_curves.csv` - these are randomly-generated Beta distribution curves which we claim are reporter absorbance curves, in response to variation in concentration of an antibiotic.
- `generate_yeast_growth_data.ipynb`: generates data in `assets/data/` for each lab bay (separate subdirectories) - these are randomly-generated logistic curves, modelling measurement noise and variation in parameters for the curve (within a constrained range) that we claim are OD values for yeast growth under various conditions.

### Generating new datasets

To generate new datasets for each year's presentation:

1. Run each of the Jupyter notebook files. These will change the data in-place.
2. Stage the modified files (`git add assets`)
3. Commit the changes (`git commit`) with a suitable commit message
4. Push the changes (`git push origin`)

### Using the data with `WebR`

In the `exercise-02_yeast.qmd` and `exercise-03_reporter.qmd` interactive exercises we use `WebR` to give students experience in using `R` for data analysis and visualisation, while not requiring any particular setup on their own, or a university, machine.

`WebR` runs in a "sandboxed" form, and is unable to interact with the local filesystem or download arbitrary files to the local machine. Instead we must explicitly preload all the datasets we might need under the `setup` context for `WebR`. In exercise 3 we need only download one such file, as in the (truncated) example below:

~~~r
```{webr-r}
#| context: setup

# Download reporter data
download.file('https://raw.githubusercontent.com/sipbs-compbiol/BM214-Workshop-3/main/assets/data/reporter_curves.csv', 'reporter_curves.csv')
```
~~~

We need to pass the full path to the online resource, and the file will be available within `WebR` as though it is a local file (`reporter_curves.csv`) within the sandboxed version of `R` running in the browser.

