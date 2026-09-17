# Gulf Crest Insurance Company: AI-Augmented Catastrophe Claims Management
AI-Augmented Catastrophe Claims Management: An Interactive Teaching Module for Property & Casualty Actuarial Science

A self-contained actuarial and data science teaching module built for the **CAS Global Teaching Materials Innovation Challenge**.

Using a fictional insurer (Gulf Crest Insurance Company) and a fictional hurricane (Marisol), the module walks students through one continuous decision-making process, from raw claims data to an executive recommendation memo: claim severity prediction (Gamma GLM vs. gradient boosting), fraud detection under class imbalance, reserve estimation (Chain Ladder and Bornhuetter-Ferguson), claims triage optimization, and sensitivity analysis. Built around 8 Jupyter notebooks, 8 synthetic datasets, and a Power BI dashboard, designed to run in a single 6-hour classroom block.

Gulf Crest Insurance Company, Hurricane Marisol, and every dataset and figure in this repository are fictional. Underlying assumptions were calibrated against public industry benchmarks and research sources (see References below) so the module behaves the way real insurer data would, without representing any real company, storm, or individual.

This repository holds the module's runnable materials (code, data, dashboard). The full teaching package, including the Instructor Guide, Student Workbook, Presentation, Assessment Package, Teaching Notes, and Solution Manuals, is distributed separately as the submission's Google Drive folder; see that folder's `Gulf_Crest_Submission_Documentation.docx` for the complete package overview and access details.

## Repository Structure

| Folder | Contents |
|---|---|
| `/notebooks` | `01_Introduction.ipynb` through `08_Final_Recommendation.ipynb`, plus `requirements.txt` and a setup guide |
| `/datasets` | The 8 CSV files behind the case (policies, claims, weather, economic indicators, repair costs, fraud labels, reserve history, company financials) |
| `/dashboard` | The Power BI (`.pbip`) project source, plus a build guide and setup notes |
| `LICENSE` | CC BY 4.0 (Creative Commons Attribution 4.0 International) |

## Getting Started

1. **Clone the repository**
   ```
   git clone https://github.com/chaisthra/cas-teaching-challenge-gulf-crest.git
   cd cas-teaching-challenge-gulf-crest
   ```
2. **Set up Python** (3.9 or later)
   ```
   pip install -r notebooks/requirements.txt
   ```
3. **Run the notebooks**, in order, with Jupyter Notebook, JupyterLab, or Google Colab (no local install needed). See `notebooks/00_SETUP_README.md` for details.
4. **Open the dashboard** with Power BI Desktop (free), or use the interactive HTML alternative referenced in `dashboard/README_SETUP.md`.

## Notebook Roadmap

| Notebook | Focus | Learning objective |
|---|---|---|
| 01_Introduction | Understand the portfolio | Understand P&C insurance |
| 02_EDA | Exploratory data analysis | Analyse insurance data |
| 03_Prediction | Claim severity prediction | Estimate claim severity |
| 04_Fraud_Detection | Fraud detection | Identify fraudulent claims |
| 05_Reserve_Estimation | Reserve estimation | Estimate reserves |
| 06_Optimization | Claims triage optimization | Optimize claim handling |
| 07_Scenario_Analysis | Sensitivity analysis | Make actuarial decisions |
| 08_Final_Recommendation | Executive recommendation | Communicate recommendations |

Each notebook maps to one activity in the Student Workbook and one learning objective in the Instructor Guide (see the full teaching package in the Google Drive submission folder for that mapping in detail).

## Software Requirements

- Python 3.9+ with pandas, numpy, scikit-learn, and matplotlib (see `notebooks/requirements.txt`)
- Jupyter Notebook / JupyterLab, or Google Colab
- Power BI Desktop (free), or a browser for the HTML dashboard alternative

No paid software is required to run any part of this module.

## References

This module draws on standard actuarial methods and publicly available industry background for realism. The sources below informed the module's design and are listed for readers who want to go further, not as citations for any specific figure in the module.

- Casualty Actuarial Society (CAS). *Statement of Principles Regarding Property and Casualty Loss and Loss Adjustment Expense Reserves.*
- Bornhuetter, R. L., and Ferguson, R. E. (1972). "The Actuarial Use of Loss Reserve Data." *Proceedings of the Casualty Actuarial Society.*
- Friedland, J. (2010). *Estimating Unpaid Claims Using Basic Techniques.* Casualty Actuarial Society.
- Werner, G., and Modlin, C. (2016). *Basic Ratemaking.* Casualty Actuarial Society.
- National Oceanic and Atmospheric Administration (NOAA). *International Best Track Archive for Climate Stewardship (IBTrACS).*
- Verisk Property Claim Services (PCS). *Catastrophe loss designation methodology.*
- Coalition Against Insurance Fraud. *Annual industry cost-of-fraud estimates.*
- Chawla, N. V., Bowyer, K. W., Hall, L. O., and Kegelmeyer, W. P. (2002). "SMOTE: Synthetic Minority Over-sampling Technique." *Journal of Artificial Intelligence Research.*
- Liu, F. T., Ting, K. M., and Zhou, Z.-H. (2008). "Isolation Forest." *IEEE International Conference on Data Mining.*
- de Jong, P., and Heller, G. Z. (2008). *Generalized Linear Models for Insurance Data.* Cambridge University Press.

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0). You are free to share and adapt this material for any purpose, even commercially, provided you give appropriate credit. See `LICENSE` for details.
