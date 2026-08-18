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
