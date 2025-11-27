# Heat-Load Forecasting Internship (Work in Progress)

This repository contains the code for my internship project at Optit on thermal-load forecasting.  
The work is still in progress, so the material should be considered a draft.

The project compares statistical time-series baselines with modern deep-learning models applied to synthetic yet realistic heat-demand datasets representing different site types.

The project includes a simple `pyproject.toml` configuration so that the `heat_forecast` package can be installed locally. From the project root, you can run:

```bash
pip install -e .
```

## Repository Structure
- `notebooks/`: exploratory analysis and modelling notebooks  
- `src/heat_forecast/`: Python modules for data handling and model implementations  
- `pyproject.toml`: project metadata and the configuration for installing the `heat_forecast` package

## Modelling Approaches
The project implements forecasting pipelines for:
- Statistical benchmarks: MSTL-ETS (via StatsForecast and Statsmodels), SARIMAX (via StatsForecast)
- Deep-learning models: LSTM (implemented in PyTorch), Temporal Fusion Transformer (via the Darts library)

## Running the Notebooks

You can run the notebooks in two ways:

### 1. Google Colab
Place the project folder `heat-forecast` in your Google Drive.  
The setup cell in each notebook will mount Drive and automatically add  
`MyDrive/heat-forecast/src` to `sys.path`, allowing direct import of `heat_forecast`.

### 2. Local Machine
Two options are available:

- **Editable install:** from the project root, run  
  ```bash
  pip install -e .
  ```
  After this, the package can be imported normally from any notebook.
- **Without installing:** if you run the notebook from `.../heat-forecast/notebooks/`, the setup cell will detect `../src`
  and add it to `sys.path` automatically.



