# Heat-Load Forecasting Internship (Work in Progress)

This repository contains the code for my internship project at Optit on heat-load forecasting.  
The work is still in progress, so the material should be considered a draft.

The project includes a simple `pyproject.toml` configuration so that the `heat_forecast` package can be installed locally. From the project root, you can run:

```bash
pip install -e .
```

## Status

Work in progress. Experiments and conclusions may evolve as the project is finalised. 

## Data

The internship dataset is confidential and is not included in this repository.

## Project overview

The project consisted of the following:

- Built reproducible end-to-end statistical and deep-learning pipelines for data preparation, training, and evaluation (Python, PyTorch, StatsForecast, Darts)
- Benchmarked statistical, traditional machine-learning, and deep-learning approaches (eg SARIMAX, XGBoost, LSTM, TFT)
- Applied rigorous validation (rolling cross-validation, residual diagnostics, bootstrap-based significance testing)
- Conducted a focused literature review on time-series forecasting with exogenous drivers, Bayesian optimisation, and evaluation protocols

## Modelling approaches and benchmarks

Implemented forecasting pipelines:
- Statistical benchmarks: MSTL-ETS (via StatsForecast and Statsmodels), SARIMAX (via StatsForecast)
- Deep-learning models: encoder-decoder LSTM (implemented in PyTorch), Temporal Fusion Transformer (via Darts)

Additional company benchmarks (provided as forecasts from existing production models):
- Machine-learning models: XGBoost, SVMR

## Main results (preliminary)

**What worked best**
- LSTM is strongest on structured (clear seasonality) series and maintains accuracy better at week-ahead horizons.
- XGBoost is the most competitive baseline across settings.

**Where models struggle**
- SARIMAX degrades in transitional periods.
- On noisier series, performance gaps narrow, suggesting limited signal in the available inputs.

**Key driver**
- Temperature provides most of the exogenous predictive value; other weather variables show little benefit.

**Limitations**
Evaluation uses historical weather rather than true forecast inputs, and tuning objectives differ slightly between thesis models (week-ahead focus) and company baselines (day-ahead focus).

## Repository structure

- `notebooks/`: exploratory analysis and modelling notebooks  
- `src/heat_forecast/`: Python modules for data handling and model implementations  
- `pyproject.toml`: project metadata and the configuration for installing the `heat_forecast` package

## Running the notebooks

To run the full notebooks end-to-end, you will need to provide your own dataset and you may wish to save outputs (models, logs, results) locally.
This repository includes the expected folder structure via `.keep` placeholder files, while data and generated artefacts are ignored by design.

You can run the notebooks in two ways:

### 1. Google Colab
Place the project folder `heat-forecast` in your Google Drive.  
The setup cell in each notebook will mount Drive and automatically add  
`MyDrive/heat-forecast/src` to `sys.path`, allowing direct import of `heat_forecast`.

### 2. Local machine
Two options are available:

- **Editable install:** from the project root, run  
  ```bash
  pip install -e .
  ```
  After this, the package can be imported normally from any notebook.
- **Without installing:** if you run the notebook from `.../heat-forecast/notebooks/`, the setup cell will detect `../src`
  and add it to `sys.path` automatically.





