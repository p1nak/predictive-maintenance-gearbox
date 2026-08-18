# Gearbox Predictive Maintenance Using Machine Learning

A machine learning-based predictive maintenance system for detecting
gearbox health conditions using multi-sensor vibration data.

The project analyzes vibration signals collected from four sensors,
extracts statistical and signal-based features, performs exploratory
data analysis, and evaluates multiple machine learning classification
models to distinguish between healthy and broken-tooth gearbox
conditions.

---

## Overview

Gearbox failures can be identified through changes in vibration
behavior. This project investigates vibration signals from a gearbox
and develops a data-driven classification pipeline for condition
monitoring.

The complete workflow consists of:

```text
Raw Vibration Data
        |
        v
Data Loading & Signal Analysis
        |
        v
Feature Extraction
        |
        v
Exploratory Data Analysis
        |
        v
Machine Learning
        |
        v
Model Evaluation
        |
        v
Saved Prediction Model
        |
        v
New Gearbox Condition Prediction
````

---

## Objectives

The primary objectives of this project are to:

* Analyze raw gearbox vibration signals from multiple sensors.
* Understand the characteristics of healthy and broken-tooth conditions.
* Extract meaningful statistical and signal-based features.
* Perform exploratory data analysis on the extracted features.
* Compare multiple machine learning classification algorithms.
* Evaluate model performance using cross-validation.
* Save the trained model and preprocessing objects.
* Build a prediction pipeline for new vibration recordings.

---

## Dataset

The dataset consists of gearbox vibration recordings obtained from
four vibration sensors.

Two gearbox conditions are considered:

* **Healthy**
* **Broken Tooth**

The recordings are provided as `.txt` files containing four sensor
channels.

The available recordings include different operating/load conditions,
represented in the source filenames.

Example filenames:

```text
Healthy:
h30hz0.txt
h30hz10.txt
h30hz20.txt
...
h30hz90.txt

Broken Tooth:
b30hz0.txt
b30hz10.txt
b30hz20.txt
...
b30hz90.txt
```

Each recording contains four sensor signals.

The original raw vibration files are not included in this repository
because of their relatively large size. The repository contains the
processed feature dataset and trained model artifacts required for
reproducing the analysis and prediction workflow.

---

## Feature Engineering

The raw vibration recordings contain a large number of individual
measurements. Instead of directly using the complete raw signal as
machine learning input, statistical and signal-based characteristics
are extracted from each sensor.

The following features are calculated for every sensor:

| Feature            | Description                                   |
| ------------------ | --------------------------------------------- |
| Mean               | Average signal value                          |
| Median             | Middle value of the signal                    |
| Standard Deviation | Measures signal variation                     |
| Variance           | Measures squared variation                    |
| Minimum            | Minimum signal value                          |
| Maximum            | Maximum signal value                          |
| Range              | Difference between maximum and minimum        |
| RMS                | Root Mean Square of the signal                |
| Peak               | Maximum absolute signal amplitude             |
| Peak-to-Peak       | Difference between maximum and minimum        |
| Skewness           | Measures distribution asymmetry               |
| Kurtosis           | Measures distribution shape and tail behavior |
| Energy             | Sum of squared signal values                  |

With four sensors and thirteen features per sensor:

```text
4 Sensors × 13 Features = 52 Features
```

Therefore, each vibration recording is represented by **52 extracted
features**.

The resulting feature dataset is stored as:

```text
gearbox_features.csv
```

---

## Exploratory Data Analysis

Exploratory Data Analysis was performed to understand the extracted
features and identify differences between healthy and broken-tooth
conditions.

The analysis includes:

* Raw vibration signal visualization
* Sensor-wise signal analysis
* Feature distributions
* Histograms
* Box plots
* Scatter plots
* Feature correlation analysis
* Correlation heatmaps
* Healthy versus broken-tooth comparisons
* Sensor-level feature analysis

The analysis showed clear differences between the two gearbox
conditions for several extracted features.

For example, the `S1_RMS` feature showed a strong separation between
the healthy and broken-tooth samples in the available dataset.

---

## Machine Learning

Five classification algorithms were evaluated:

1. Logistic Regression
2. K-Nearest Neighbors (KNN)
3. Decision Tree
4. Random Forest
5. Support Vector Machine (SVM)

### Model Performance

| Model                  | Accuracy |
| ---------------------- | -------: |
| Logistic Regression    |     100% |
| K-Nearest Neighbors    |     100% |
| Decision Tree          |     100% |
| Random Forest          |     100% |
| Support Vector Machine |     100% |

The above results represent performance obtained during the project's
current evaluation on the available dataset.

---

## Cross-Validation

Random Forest was further evaluated using **5-fold Stratified
Cross-Validation**.

Results:

```text
Fold 1: 100%
Fold 2: 100%
Fold 3: 100%
Fold 4: 100%
Fold 5: 100%

Mean Accuracy: 100%
Standard Deviation: 0%
```

The model produced consistent results across all five validation folds
on the available feature dataset.

> **Note:** The reported performance is specific to the available
> dataset and evaluation setup. It should not be interpreted as a
> guarantee of 100% accuracy on unseen real-world gearbox data.

---

## Prediction Pipeline

The trained model can be used to classify a new four-channel vibration
recording.

The prediction process is:

```text
New TXT Vibration File
          |
          v
Read Four Sensor Signals
          |
          v
Extract 52 Features
          |
          v
Apply Feature Scaling
          |
          v
Random Forest Classifier
          |
          v
Healthy / Broken Tooth
```

This allows the trained model to be reused without retraining whenever
a new vibration recording is available.

---

## Model Artifacts

The trained model and preprocessing components are included in the
repository:

| File                | Description                      |
| ------------------- | -------------------------------- |
| `gearbox_model.pkl` | Trained Random Forest classifier |
| `scaler.pkl`        | Feature scaling object           |
| `label_encoder.pkl` | Label encoding object            |

These files are used by the prediction notebook to process new
vibration recordings.

---

## Project Structure

```text
predictive-maintenance-gearbox/
│
├── Data Loading & Visualization.ipynb
├── Feature Extraction.ipynb
├── Exploratory Data Analysis (EDA).ipynb
├── Machine Learning.ipynb
├── Gearbox Prediction.ipynb
│
├── gearbox_features.csv
├── prediction_results.csv
│
├── gearbox_model.pkl
├── scaler.pkl
├── label_encoder.pkl
│
├── .gitignore
└── README.md
```

---

## Notebook Workflow

### 1. Data Loading & Visualization

Loads the raw vibration recordings and performs initial signal
inspection and visualization.

Key activities:

* Loading vibration data
* Inspecting sensor dimensions
* Understanding sensor signals
* Visualizing amplitude
* Comparing healthy and broken signals

### 2. Feature Extraction

Processes the four sensor signals and calculates 13 features per sensor,
resulting in 52 features for every recording.

Output:

```text
gearbox_features.csv
```

### 3. Exploratory Data Analysis

Analyzes the extracted feature dataset using statistical summaries and
visualizations.

Key activities:

* Feature distributions
* Box plots
* Histograms
* Scatter plots
* Correlation analysis
* Healthy versus broken comparisons

### 4. Machine Learning

Trains and evaluates multiple classification algorithms.

Models evaluated:

```text
Logistic Regression
KNN
Decision Tree
Random Forest
SVM
```

The notebook also performs 5-fold stratified cross-validation.

### 5. Gearbox Prediction

Loads the saved model and preprocessing objects and predicts the
condition of a new vibration recording.

---

## Technologies

### Programming Language

* Python

### Data Processing

* NumPy
* Pandas

### Statistical and Signal Analysis

* SciPy

### Data Visualization

* Matplotlib
* Seaborn

### Machine Learning

* Scikit-learn

### Model Serialization

* Joblib

### Development Environment

* Jupyter Notebook
* Visual Studio Code

---

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/predictive-maintenance-gearbox.git
```

Navigate to the project directory:

```bash
cd predictive-maintenance-gearbox
```

Install the required libraries:

```bash
pip install numpy pandas scipy matplotlib seaborn scikit-learn joblib jupyter
```

Start Jupyter Notebook:

```bash
jupyter notebook
```

---

## Running the Project

For the complete workflow, execute the notebooks in the following order:

```text
1. Data Loading & Visualization.ipynb
2. Feature Extraction.ipynb
3. Exploratory Data Analysis (EDA).ipynb
4. Machine Learning.ipynb
5. Gearbox Prediction.ipynb
```

The original vibration dataset should be available locally before
running the data loading and feature extraction notebooks.

---

## Key Results

The project successfully demonstrates a complete vibration-based
machine learning workflow for gearbox condition classification.

### Summary

* Four vibration sensors analyzed
* Thirteen features extracted from each sensor
* 52 features generated per recording
* Healthy and broken-tooth conditions classified
* Five machine learning algorithms evaluated
* Random Forest evaluated using 5-fold stratified cross-validation
* Trained model and preprocessing objects saved
* New vibration recordings can be processed through the prediction
  pipeline

---

## Limitations

The current implementation has several limitations:

* The evaluation is based on the available dataset.
* External gearbox datasets have not been used for validation.
* The system currently handles the available healthy and broken-tooth
  conditions.
* Real-time sensor acquisition has not yet been integrated.
* Industrial deployment would require testing under additional
  operating conditions, noise levels, and gearbox configurations.

Therefore, further validation with independent real-world data would be
required before production deployment.

---

## Future Work

Potential improvements include:

* Real-time vibration data acquisition
* Live gearbox condition monitoring
* Industrial IoT sensor integration
* Web-based monitoring dashboard
* Automated fault notifications
* Detection of additional gearbox fault types
* Real-time prediction
* Edge-device deployment
* Remaining Useful Life (RUL) estimation
* Continuous model improvement using newly collected data

---

## Applications

The developed approach can be applied to:

* Predictive maintenance
* Gearbox condition monitoring
* Vibration-based fault detection
* Industrial equipment monitoring
* Manufacturing systems
* Industrial IoT applications
* Machine health monitoring

---

## Author

**Pinak Chauhan**

Computer Engineering Student

Interested in:

* Artificial Intelligence
* Machine Learning
* Data Analytics
* Python
* Predictive Maintenance

---
