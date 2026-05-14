# Purpose of this repository

This repository contains the **experimental implementation used in the article** on Deep Reinforcement Learning for Production Scheduling in Sea Cage Aquaculture.

The code reproduces the DeepRL framework proposed in the study for optimizing production lot durations in aquaculture systems, considering biological growth, sea surface temperature dynamics, feed consumption, mortality, and economic returns.

Two sale-price settings are included:

- **Fixed sale-price setting**, where sale prices remain constant across the planning horizon.
- **Variable sale-price setting**, where sale prices depend on the harvest period through seasonal price multipliers.

The repository allows the reviewer to:

- run the **DeepRL training procedure**,
- evaluate trained policies for each production region,
- compare DeepRL policies against the heuristic benchmark,
- reproduce the fixed-price and variable-price experimental settings,
- inspect the datasets and trained models used in the study.

---

# Main components

## `FixedPriceCode.ipynb`

Notebook containing the full experimental pipeline for the **fixed sale-price setting**.

It includes:

1. dataset loading and preprocessing,
2. aquaculture environment definition,
3. hyperparameter optimization with Optuna,
4. final MaskablePPO training,
5. deterministic validation and testing,
6. comparison against the heuristic benchmark,
7. generation of figures and result summaries.

---

## `VarPriceCode.ipynb`

Notebook containing the full experimental pipeline for the **variable sale-price setting**.

It follows the same general structure as the fixed-price version, but modifies the reward function so that sale prices depend on the harvest week through seasonal multipliers.

---

# Datasets

The repository includes the datasets required to reproduce the experiments:

- **`SST_3loc_weekly.csv`**  
  Weekly sea surface temperature data for the three production regions.

- **`feed_prices.csv`**  
  Feed price data used to compute feeding costs.

- **`sale_prices.csv`**  
  Sale price data by fish weight category.

- **`feed_rates.csv`**  
  Feed-rate, mortality, and growth-related technical data used by the aquaculture simulation environment.

---

# Trained models

The repository also includes the trained DeepRL models used in the experimental evaluation.

## Fixed sale-price models

- `best_model_val_fixed_price_Valencia.zip`
- `best_model_val_fixed_price_Adriatico.zip`
- `best_model_val_fixed_price_Grecia.zip`

## Variable sale-price models

- `best_model_val_var_price_Valencia.zip`
- `best_model_val_var_price_Adriatico.zip`
- `best_model_val_var_price_Grecia.zip`

Each model corresponds to the best validation policy obtained for the associated region and pricing setting.

---

# Running an experiment

To reproduce the experiments, open either:

```python
FixedPriceCode.ipynb
```

or

```python
VarPriceCode.ipynb
```

At the beginning of each notebook, select the region to train and evaluate by modifying:

```python
chosen_region = "Valencia"
```

Available regions are:

```python
["Adriatico", "Valencia", "Grecia"]
```

Then execute the corresponding training, validation, and evaluation cells of the notebook.
