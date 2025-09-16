# Dataset for paper: "Self-Organizing Complex Networks with AI-Driven Adaptive Nodes for Optimized Connectivity and Energy Efficiency"

## Overview
This repository contains the datasets used to train the MLP models reported in the paper. The data are simulation outputs collected at different numbers of simulation steps.

## Folder structure
datasets_for_train_mlps/
├─ outputs_for_10000_step/ # simulation outputs after 10,000 steps (approx. 43.5 MB)
└─ outputs_for_50000_step/ # simulation outputs after 50,000 steps (approx. 223 MB)

Each `outputs-density=<value>/` subfolder contains CSV files used to train MLP models.

## Files and formats

**`local_data_for_mlp1.csv`** (per-row columns)
- `0: id` — integer, node identifier.
- `1: density` — float, node density parameter used in simulation.
- `2: T` — integer, control parameter.
- `3: degree` — integer, node degree (number of neighbors).
- `4: range` — float, current transmission range.
- `5: nextRange` — float, target/next transmission range (label).

**`local_data_for_mlp2.csv`** (per-row columns)
- `0: id` — integer, node identifier.
- `1: density` — float, node density parameter used in simulation.
- `2: T` — control parameter.
- `3: range` — float, current transmission range.
- `4: degree` — integer, node degree.
- `5: distance` — float, distance to a reference (units: same as `range`).
- `6: connectionStatus` — integer or boolean-like (0/1), whether the node is connected to a target/neighbor.

> **Note:** all CSV files are comma-separated, include a header row (if applicable), and use UTF-8 encoding. If any file lacks a header, the column indices above map to the CSV columns.

## How these files are used
- `local_data_for_mlp1.csv` files were used to train **MLP1** (predict nextRange from local features).  
- `local_data_for_mlp2.csv` files were used to train **MLP2** (predict connection status or other local outcomes based on local features).

## Quick example: loading a file (Python / pandas)
```python
import pandas as pd
p = "datasets_for_train_mlps/outputs_for_50000_step/outputs-density=0.100/local_data_for_mlp2.csv"
df = pd.read_csv(p)
print(df.columns)
print(df.head())
