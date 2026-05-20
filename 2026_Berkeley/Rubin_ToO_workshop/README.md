# Rubin ToO Workshop Tutorial

This folder contains a guided Jupyter tutorial for simulating a single Rubin target-of-opportunity kilonova follow-up case.

## Start Here

Open `rubin_too_workshop.ipynb` and run the notebook from top to bottom. The notebook is structured as a workshop tutorial with setup notes, checkpoint questions, editable parameters, and two example runs:

- `100 Mpc`: baseline event distance
- `200 Mpc`: same event moved farther away

The notebook writes new products to `outputs/` so participants can rerun the tutorial without overwriting the provided example files.

## Files

- `rubin_too_workshop.ipynb`: main tutorial notebook
- `S251112cm_obs_vanilla.h5`: Rubin visit table used as the simulation input
- `S251112cm*.csv`: example observation and truth tables from prior runs
- `S251112cm*.png`: example diagnostic plots from prior runs

## Create the Conda Environment

If you already tried creating the environment and it failed, remove the partial environment first:

```bash
conda env remove -n rubin-too-workshop
```

From this folder, run:

```bash
conda env create -f environment.yml
conda activate rubin-too-workshop
python -m ipykernel install --user --name rubin-too-workshop --display-name "Rubin ToO Workshop"
```

Then open `rubin_too_workshop.ipynb` and choose the `Rubin ToO Workshop` kernel.

If imports fail with a NumPy ABI error such as `numpy.core.multiarray failed to import`, make sure you recreated the environment from the latest `environment.yml`. The file pins `numpy=1.26.4` because the Bulla BNS surrogate backend depends on Torch/kilonovanet builds that do not currently work with NumPy 2 in this environment.

The notebook sets `NUMBA_DISABLE_JIT=1` before importing `redback` to avoid Numba cache issues on workshop machines. It uses the Bulla BNS kilonova model through `redback-surrogates`, so the environment pins `numpy=1.26.4` for Torch/kilonovanet compatibility.

## Expected Python Packages

The tutorial expects a Python/Jupyter environment with:

- `numpy`
- `pandas`
- `matplotlib`
- `astropy`
- `lightcurvelynx`
- `redback`
- `tables` or another pandas-compatible HDF5 backend

## Suggested Workshop Flow

1. Run the setup and data-inspection cells.
2. Pause at the settings cell and explain the event parameters.
3. Run the 100 Mpc baseline case.
4. Inspect the saved observation table.
5. Run the 200 Mpc comparison.
6. Discuss how cadence, depth, filter choice, and distance affect detectability.
