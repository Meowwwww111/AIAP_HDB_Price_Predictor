# 🏠 HDB Price Predictor

A machine learning project for predicting Singapore HDB resale flat prices using historical resale transaction data. The project covers data cleaning, feature engineering, preprocessing, model training, hyperparameter tuning, validation, and final test-set evaluation.

## 📌 Project Overview

This project uses HDB resale transaction data to build and compare several regression models for predicting `resale_price`.

The workflow is:

1. Load the resale transaction dataset
2. Clean and transform the data
3. Engineer useful features such as lease duration and storey level
4. Build a preprocessing pipeline for numerical, nominal, ordinal, and passthrough features
5. Train baseline regression models
6. Tune Ridge and Lasso regression using `GridSearchCV`
7. Compare models using validation metrics
8. Select the model with the highest validation R²
9. Evaluate the selected model on the held-out test set

## 🤖 Models

The project currently evaluates:

- Linear Regression
- Ridge Regression
- Lasso Regression
- Tuned Ridge Regression
- Tuned Lasso Regression

Ridge and Lasso models are tuned using a grid of:

- `alpha`: `0.1`, `1`, `10`, `100`, `1000`
- `fit_intercept`: `True`, `False`
- 5-fold cross-validation
- R² scoring

## 🧹 Data Preparation

The preprocessing pipeline includes:

- Removing duplicate records
- Standardising flat-type naming such as `FOUR ROOM` → `4 ROOM`
- Cleaning lease commencement dates
- Converting storey ranges into average storey values
- Filling missing town and flat-model names using their corresponding IDs
- Removing identifier columns that are not used for modelling
- Extracting year and month from the transaction month
- Converting remaining lease information into months
- Removing unused columns such as block and street name
- Standardising numerical features
- One-hot encoding nominal categorical features
- Ordinal encoding flat type

## 📊 Features

The model uses the following feature groups:

### Numerical

- `floor_area_sqm`
- `remaining_lease_months`
- `lease_commence_date`
- `year`

### Nominal categorical

- `month`
- `town_name`
- `flatm_name`

### Ordinal categorical

- `flat_type`

### Passthrough

- `storey_range`

### Target

- `resale_price`

## 📈 Evaluation

Models are evaluated using:

- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- R² Score

The dataset is split into training, validation, and test sets. The final model is selected using validation R² before being evaluated on the unseen test set.

## 📁 Project Structure

```text
AIAP_HDB_Price_Predictor/
│
├── data/
│   └── resale_transactions.csv
│
├── src/
│   ├── config.yaml
│   ├── data_preparation.py
│   └── model_training.py
│
├── eda.ipynb
├── main.py
├── requirements.txt
├── .gitignore
└── README.md
```

## 📄 File Description

| File | Description |
|---|---|
| `main.py` | Main entry point for data loading, training, model selection and evaluation |
| `src/data_preparation.py` | Data cleaning, feature engineering and preprocessing pipeline |
| `src/model_training.py` | Model definitions, hyperparameter tuning and evaluation |
| `src/config.yaml` | Dataset path, target, features, split settings and model parameters |
| `eda.ipynb` | Exploratory data analysis notebook |
| `data/resale_transactions.csv` | HDB resale transaction dataset |
| `requirements.txt` | Python dependencies |

## ⚙️ Configuration

Model and preprocessing settings are stored in `src/config.yaml`, including:

- Dataset path
- Target variable
- Train/validation/test split settings
- Ridge and Lasso hyperparameter grids
- Cross-validation settings
- Numerical features
- Categorical features
- Flat-type category ordering

This makes it possible to adjust the experiment without changing the main Python code.

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Meowwwww111/AIAP_HDB_Price_Predictor.git
cd AIAP_HDB_Price_Predictor
```

### 2. Create a Python environment

Using Conda:

```bash
conda create -n hdb-price python=3.11 -y
conda activate hdb-price
```

Or using Python's built-in virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the model pipeline

```bash
python main.py
```

The program will load the configured dataset, prepare the data, train the models, tune Ridge and Lasso, compare validation performance, and evaluate the selected model on the test set.

## 🔎 Exploratory Data Analysis

The `eda.ipynb` notebook can be opened with Jupyter Notebook or VS Code to explore the dataset and understand relationships between HDB resale prices and the available features.

For example:

```bash
jupyter notebook eda.ipynb
```

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- PyYAML
- Jupyter Notebook
- Matplotlib
- Seaborn

## ⚠️ Notes & Limitations

- The model is trained on historical HDB resale transactions and should not be treated as a guaranteed valuation of a property.
- Model performance depends on the quality, coverage, and time period of the dataset.
- Market conditions, location-specific factors, amenities, renovation condition, and other information not represented in the dataset may affect actual resale prices.
- Hyperparameter tuning is currently focused on Ridge and Lasso regression.

## 🔮 Potential Improvements

Future versions could explore:

- Tree-based models such as Random Forest and Gradient Boosting
- XGBoost or other advanced boosting methods
- More detailed location-based features
- Distance to MRT stations, schools and amenities
- Additional temporal features
- Feature importance and model interpretability
- Automated model comparison
- A web interface for interactive HDB price prediction

## 👨‍💻 Author

**Jasper Ng (Ng Jing Heng)**  
NTU Mechanical Engineering — Intelligent Manufacturing

Interested in robotics, automation, machine learning and data-driven engineering solutions.

## 📜 License

This project is intended for educational and portfolio purposes.
