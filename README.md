# Psychology-Informed-Anomaly-Detection-in-Insider-Threat-Systems
Psychology-Informed Anomaly Detection in Insider Threat Systems

# Anomaly Detection using Autoencoder

## Overview
This project implements an unsupervised anomaly detection system using a deep autoencoder on user activity logs (CERT dataset). It identifies anomalous user behaviour and maps it to psychology-inspired constructs such as boundary crossing, behavioural volatility, and impulsive spikes.

## Methodology
- Data aggregation into user-day behavioural features
- Feature scaling using StandardScaler
- Autoencoder trained using PyTorch
- Reconstruction error used as anomaly score
- Threshold = mean + 2*std (training error)
- Rule-based psychology mapping layer

## Results
- 61,198 user-day records
- 643 anomalies detected
- Threshold: 3.43

## Technologies Used
- Python
- Pandas
- Scikit-learn
- PyTorch
- Matplotlib

## How to Run
1. Open the notebook in Google Colab or Jupyter
2. Upload dataset (https://doi.org/10.1184/R1/12841247)
3. Run all cells sequentially
