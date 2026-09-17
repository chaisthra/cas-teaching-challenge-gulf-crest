# Environment Setup

## What is a Jupyter Notebook

A Jupyter Notebook combines explanatory text with runnable code, organized into cells. Run a code cell (click it, press Shift+Enter), the result appears below it, then move to the next cell. Most cells are pre-written and explained; the focus is on running them, reading the output, and answering the corresponding questions in the Workbook.

## Step 1: Install Python and Jupyter

The recommended route is Anaconda, a free bundle that includes Python, Jupyter, and the required data science libraries in one installer:

1. Go to https://www.anaconda.com/download and download the installer for your operating system (Windows/Mac/Linux).
2. Run the installer, accepting the default options.
3. Open "Anaconda Navigator" (installed alongside it) and launch Jupyter Notebook or JupyterLab from there.

If Python is already installed, run this instead in a terminal:
```
pip install -r requirements.txt
jupyter notebook
```

## Step 2: Notebook Sequence

The notebooks in this folder are numbered and designed to run in sequence:

1. `01_Introduction.ipynb`
2. `02_EDA.ipynb`
3. `03_Prediction.ipynb`
4. `04_Fraud_Detection.ipynb`
5. `05_Reserve_Estimation.ipynb`
6. `06_Optimization.ipynb`
7. `07_Scenario_Analysis.ipynb`
8. `08_Final_Recommendation.ipynb`

Each notebook builds on results and concepts from the one before it.

## Step 3: Running a Notebook

1. Open the notebook file in Jupyter.
2. Click on the first cell.
3. Press Shift + Enter to run it and move to the next cell. Repeat for every cell, top to bottom.
4. Read the markdown (text) cells: they explain the reasoning behind each step, not only the mechanics. Code comments serve the same purpose.
5. If a cell errors out, it's almost always because an earlier cell wasn't run yet. Use "Kernel" then "Restart & Run All" to reset and re-run everything in order.

## Key Terms

- DataFrame: a table loaded into the notebook, rows and columns, similar to a spreadsheet, but filtered, sorted, and calculated on with code.
- NaN / missing value: an empty cell where the data wasn't available for that row. Common in real-world data, and part of what this module works with rather than something to delete outright.
- Model: a mathematical formula fitted to past data (for example, "properties with a higher insured value tend to have higher-cost claims") that produces predictions on new data.

## Data Location

Every notebook expects the datasets in `../04_Datasets/` (one folder up, then into `04_Datasets`). If the notebooks folder moves, keep it alongside `04_Datasets`.
