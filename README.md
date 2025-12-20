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
This project studies short-term heat-load forecasting in an operational setting, covering day-ahead and week-ahead horizons across five target series.
Models use historical heat-load signals with exogenous weather drivers. In experiments, future weather covariates are treated as known (in practice replaced by weather forecasts).
The time series were derived from project data and reworked to mimic realistic behaviour, representing different scenarios (e.g. residential areas, industrial areas, and public buildings).

Main components of the work:
- Built reproducible end-to-end statistical and deep-learning pipelines for data preparation, training, and evaluation (Python, PyTorch, StatsForecast, Darts)
- Benchmarked statistical, traditional machine-learning, and deep-learning approaches (e.g. SARIMAX, XGBoost, encoder--decoder LSTM, TFT)
- Applied an operationally realistic and rigorous validation protocol (rolling cross-validation, residual diagnostics, and Circular Block Bootstrap significance testing)
- Conducted a focused literature review on time-series forecasting with exogenous drivers, Bayesian optimisation, and evaluation protocols

## Modelling approaches and benchmarks

Implemented forecasting pipelines:
- Statistical benchmarks: MSTL-ETS (via StatsForecast and Statsmodels), SARIMAX (via StatsForecast)
- Deep-learning models: encoder-decoder LSTM (implemented in PyTorch), Temporal Fusion Transformer (via Darts)

Additional company benchmarks (provided as forecasts from existing production models):
- Machine-learning models: XGBoost, SVMR

## Main results (preliminary)

**What worked best**
- LSTM is the most accurate model on structured (clear seasonality) series, with improvements confirmed by Circular Block Bootstrap significance tests, and maintains accuracy better at week-ahead horizons.
- XGBoost is the most competitive benchmark across settings and is substantially faster to train and easier to scale.

**Where models struggle**
- SARIMAX degrades in transitional periods but performs strongly in winter, at a substantially higher computational cost than the machine-learning benchmarks.
- On noisier series, performance gaps narrow, suggesting limited signal in the available inputs or a need for different training strategies (e.g. cross-series training and/or transfer learning).

**Key driver**
- Temperature provides most of the exogenous predictive value; other weather variables show little benefit.

**Limitations**
Evaluation uses historical weather rather than true forecast inputs, and tuning objectives differ slightly between thesis models (week-ahead focus) and company baselines (day-ahead focus).

## Repository structure
Tracked in this repository:
- `notebooks/`: exploratory analysis and modelling notebooks
- `src/heat_forecast/`: Python modules for data handling, modelling, and evaluation
- `pyproject.toml`: project metadata and configuration for installing the `heat_forecast` package

Expected local folders (shown via `.keep` placeholders, ignored by design):
- `data/`: user-provided datasets (stored under `data/timeseries/`)
- `models/`: saved model parameters
- `results/`: training and testing outputs, including runtime metrics (training and inference times on CPU and GPU)
- `logs/`: training and experiment logs

## Running the notebooks

To run the notebooks end-to-end, you will need to provide your own dataset. Some notebooks (e.g. results comparison) assume that intermediate outputs have been generated and saved locally (e.g. results files). This repository includes the expected folder structure via `.keep` placeholder files, while data and generated artefacts are ignored by design.

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





