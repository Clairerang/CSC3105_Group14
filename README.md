
# CSC3105 Group 14 Mini Project

This repository contains our CSC3105 mini project on machine learning for Ultra-Wideband (UWB) indoor ranging under Line-of-Sight (LOS) and Non-Line-of-Sight (NLOS) conditions. The project studies whether UWB measurements can be used to:

1. classify LOS vs NLOS channel conditions
2. predict range more accurately from signal-derived features

The repository includes the full notebook workflow, processed data, trained-model outputs, and generated figures used to support the final analysis.

## Demo

YouTube demo link: [https://youtu.be/a1iQ6uTfpCA?si=ou_JR9OnATRMqqKe](https://youtu.be/a1iQ6uTfpCA?si=ou_JR9OnATRMqqKe)

## Team Members

| Name | SIT ID | GUID |
| --- | --- | --- |
| Koh Shi Min | 2401793 | 3070670K |
| Ang Jing Yi Clairer | 2402610 | 3070699A |
| Oon Zhen Wei William | 2401532 | 3070657O |
| Lucas Lee Jing Yi | 2401107 | 3070629L |
| Phoebe Lau | 2403551 | 3070576L |

## Project Goal

Indoor positioning systems often suffer when walls, furniture, and reflections create NLOS signal paths. These effects distort the channel impulse response (CIR) and reduce the reliability of raw time-of-flight range measurements.

This project applies supervised learning to UWB signal measurements so that we can:

- detect whether a measurement is LOS or NLOS
- estimate range using learned regression models
- compare traditional machine learning methods with neural-network-based approaches

## Dataset

The project uses the bundled **UWB LOS and NLOS Data Set** stored in `Dataset/UWB-LOS-NLOS-Data-Set/`.

Dataset summary:

- Total samples: `42,000`
- LOS samples: `21,000`
- NLOS samples: `21,000`
- Indoor environments: `7`
- Main classification label: `NLOS`
- Main regression target: `RANGE`
- Processed dataset used by the notebooks: `data/uwb_preprocessed_for_ml.csv`

The original dataset README states that measurements were collected using the SNPN-UWB board with the DecaWave DWM1000 UWB radio module across seven indoor environments, with balanced LOS and NLOS samples.

## Workflow

The project is organized as a notebook-based pipeline:

1. `Exploratory_Data_Analysis.ipynb`
   Explores class balance, metadata distributions, CIR behavior, PCA plots, and feature relationships.
2. `00_Data_Prep.ipynb`
   Cleans data, prepares engineered features, and writes the processed dataset used for training.
3. `01_Classification.ipynb`
   Trains and evaluates LOS/NLOS classification models.
4. `02_Regression.ipynb`
   Trains and evaluates range-prediction regression models.

## Results

The results below are aligned with the final summary sections in `01_Classification.ipynb` and `02_Regression.ipynb`.

### Classification

Top classification models: `MLP` and `XGBoost`

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
| --- | ---: | ---: | ---: | ---: | ---: |
| MLP | 0.9217 | 0.9397 | 0.9012 | 0.9200 | 0.9780 |
| XGBoost | 0.9225 | 0.9383 | 0.9045 | 0.9211 | 0.9771 |
| Random Forest | 0.9155 | 0.9258 | 0.9033 | 0.9144 | 0.9739 |
| Logistic Regression | 0.8589 | 0.8835 | 0.8269 | 0.8543 | 0.9238 |
| Linear SVM | 0.8589 | 0.8880 | 0.8214 | 0.8534 | 0.9234 |
| 1D CNN | 0.8500 | 0.8820 | 0.8081 | 0.8434 | 0.9204 |

### Regression

Task 2 best model: `MLP`

| Model | RMSE | MAE | R^2 |
| --- | ---: | ---: | ---: |
| MLP | 1.3036 | 0.9809 | 0.6931 |
| Random Forest | 1.3419 | 1.0132 | 0.6748 |
| XGBoost | 1.3604 | 1.0332 | 0.6657 |

Task 2b best model: `MLP`

| Model | RMSE | MAE | R^2 |
| --- | ---: | ---: | ---: |
| MLP | 1.2973 | 0.9753 | 0.8274 |
| XGBoost | 1.3589 | 1.0081 | 0.8106 |
| Random Forest | 1.3839 | 1.0138 | 0.8035 |

### Key Takeaways

- `XGBoost` achieved the strongest overall LOS/NLOS classification result in the final notebook, with `92.25%` accuracy and `0.9211` F1-score.
- `MLP` recorded the highest reported `ROC-AUC` at `0.9780`, showing similarly strong classification performance.
- `MLP` delivered the best regression results for both Task 2 and Task 2b.
- Task 2b produced a higher `R^2` than Task 2, although the notebook notes this should be interpreted carefully because the target distributions differ across the two tasks.

### Output Artifacts

Generated outputs are stored in `results/`, including:

- `results/classification/` for model comparison plots, ROC curves, confusion matrices, and CNN training curves
- `results/regression/` for regression comparison and range-analysis plots
- `results/figures/eda/` for exploratory data analysis figures
- `results/model_comparison.csv` for classifier metrics
- `results/feature_importance.csv` for feature-importance rankings

## Repository Structure

```text
CSC3105_Group14/
|-- Exploratory_Data_Analysis.ipynb    # exploratory analysis and visualization
|-- 00_Data_Prep.ipynb                 # preprocessing and feature engineering
|-- 01_Classification.ipynb            # LOS/NLOS classification experiments
|-- 02_Regression.ipynb                # range prediction experiments
|-- Dataset/
|   `-- UWB-LOS-NLOS-Data-Set/         # original bundled dataset and license
|-- data/
|   `-- uwb_preprocessed_for_ml.csv    # processed dataset used by the notebooks
|-- results/
|   |-- classification/                # classifier plots and evaluation outputs
|   |-- regression/                    # regression plots and analysis outputs
|   |-- figures/eda/                   # EDA figures
|   |-- feature_importance.csv         # feature ranking summary
|   |-- model_comparison.csv           # model performance summary
|-- CSC3105_Mini_Project_2026.pdf      # project brief
|-- pyproject.toml                     # dependency and tool configuration
`-- uv.lock                            # locked dependency versions
```

## Setup

This project uses Python `3.13` and `uv`.

```bash
python -m pip install uv
uv venv --python 3.13
uv sync
uv run jupyter lab
```

## Recommended Run Order

Run the notebooks in this order:

1. `Exploratory_Data_Analysis.ipynb`
2. `00_Data_Prep.ipynb`
3. `01_Classification.ipynb`
4. `02_Regression.ipynb`

## Tech Stack

- Python `3.13`
- Jupyter
- NumPy
- pandas
- SciPy
- scikit-learn
- TensorFlow
- XGBoost
- Matplotlib
- seaborn

## Dataset Attribution and Citation

This repository includes the **UWB LOS and NLOS Data Set** by **Klemen Bregar** from SensorLab, Jozef Stefan Institute, under the `CC BY 4.0` license. The bundled license text is available at `Dataset/UWB-LOS-NLOS-Data-Set/LICENSE.txt`.

If you use this project or the underlying dataset in reports, presentations, or derivative work, please cite the original dataset paper referenced by the dataset authors:

> Klemen Bregar, Andrej Hrovat, Mihael Mohorcic, "NLOS Channel Detection with Multilayer Perceptron in Low-Rate Personal Area Networks for Indoor Localization Accuracy Improvement," Proceedings of the 8th Jozef Stefan International Postgraduate School Students' Conference, Ljubljana, Slovenia, May 31-June 1, 2016.

Reference link:

- https://www.researchgate.net/publication/308986067_NLOS_Channel_Detection_with_Multilayer_Perceptron_in_Low-Rate_Personal_Area_Networks_for_Indoor_Localization_Accuracy_Improvement

For completeness, the dataset package also credits funding from the European Horizon 2020 Programme project eWINE, grant agreement No. `688116`.

## Notes

- The repository already contains both raw and processed data.
- Results reported here are taken from the final summary tables in `01_Classification.ipynb` and `02_Regression.ipynb`.
- If the environment uses Python newer than `3.13`, dependency resolution may fail because `pyproject.toml` requires `>=3.13,<3.14`.
