# Anomaly Detection using Autoencoder for Insider Threat Behaviour

## Overview
This project implements an unsupervised anomaly detection system using a deep autoencoder to identify unusual user behaviour from system activity logs. The approach is based on the idea that insider threats often do not appear as explicit attacks, but as subtle deviations from normal behaviour patterns.

The system not only detects anomalous behaviour but also enhances interpretability by mapping anomalies to psychology-inspired behavioural constructs such as boundary crossing, behavioural volatility, impulsive spikes, and persistence. This makes the output more meaningful and aligned with real-world Security Operations Centre (SOC) workflows.

---

## Methodology

### 1. Data Processing and Feature Engineering
The project uses the CERT insider threat dataset, specifically focusing on logon and logoff activity. Since raw logs are event-based, they are first transformed into structured behavioural profiles.

- Each row in the final dataset represents **one user on one day**
- Raw logs are grouped using `(user, day)`
- Aggregation is performed to extract behavioural features

Key features include:
- Total number of events (activity volume)
- Logon and logoff counts
- Number of unique hosts accessed
- First login hour and last activity hour
- After-hours activity count and ratio
- Temporal variability (standard deviation of activity hours)

This transformation converts variable-length event logs into fixed-size feature vectors suitable for machine learning.

---

### 2. Feature Scaling
All features are standardised using `StandardScaler` to ensure that differences in numeric scale do not bias the model.

This step is critical because:
- Features like event counts and ratios are on different ranges
- Scaling ensures equal contribution during training

---

### 3. Autoencoder Model
A dense autoencoder is used to learn normal behavioural patterns.

Architecture:
# Anomaly Detection using Autoencoder for Insider Threat Behaviour

## Overview
This project implements an unsupervised anomaly detection system using a deep autoencoder to identify unusual user behaviour from system activity logs. The approach is based on the idea that insider threats often do not appear as explicit attacks, but as subtle deviations from normal behaviour patterns.

The system not only detects anomalous behaviour but also enhances interpretability by mapping anomalies to psychology-inspired behavioural constructs such as boundary crossing, behavioural volatility, impulsive spikes, and persistence. This makes the output more meaningful and aligned with real-world Security Operations Centre (SOC) workflows.

---

## Methodology

### 1. Data Processing and Feature Engineering
The project uses the CERT insider threat dataset, specifically focusing on logon and logoff activity. Since raw logs are event-based, they are first transformed into structured behavioural profiles.

- Each row in the final dataset represents **one user on one day**
- Raw logs are grouped using `(user, day)`
- Aggregation is performed to extract behavioural features

Key features include:
- Total number of events (activity volume)
- Logon and logoff counts
- Number of unique hosts accessed
- First login hour and last activity hour
- After-hours activity count and ratio
- Temporal variability (standard deviation of activity hours)

This transformation converts variable-length event logs into fixed-size feature vectors suitable for machine learning.

---

### 2. Feature Scaling
All features are standardised using `StandardScaler` to ensure that differences in numeric scale do not bias the model.

This step is critical because:
- Features like event counts and ratios are on different ranges
- Scaling ensures equal contribution during training

---

### 3. Autoencoder Model
A dense autoencoder is used to learn normal behavioural patterns.

Architecture:
# Anomaly Detection using Autoencoder for Insider Threat Behaviour

## Overview
This project implements an unsupervised anomaly detection system using a deep autoencoder to identify unusual user behaviour from system activity logs. The approach is based on the idea that insider threats often do not appear as explicit attacks, but as subtle deviations from normal behaviour patterns.

The system not only detects anomalous behaviour but also enhances interpretability by mapping anomalies to psychology-inspired behavioural constructs such as boundary crossing, behavioural volatility, impulsive spikes, and persistence. This makes the output more meaningful and aligned with real-world Security Operations Centre (SOC) workflows.

---

## Methodology

### 1. Data Processing and Feature Engineering
The project uses the CERT insider threat dataset, specifically focusing on logon and logoff activity. Since raw logs are event-based, they are first transformed into structured behavioural profiles.

- Each row in the final dataset represents **one user on one day**
- Raw logs are grouped using `(user, day)`
- Aggregation is performed to extract behavioural features

Key features include:
- Total number of events (activity volume)
- Logon and logoff counts
- Number of unique hosts accessed
- First login hour and last activity hour
- After-hours activity count and ratio
- Temporal variability (standard deviation of activity hours)

This transformation converts variable-length event logs into fixed-size feature vectors suitable for machine learning.

---

### 2. Feature Scaling
All features are standardised using `StandardScaler` to ensure that differences in numeric scale do not bias the model.

This step is critical because:
- Features like event counts and ratios are on different ranges
- Scaling ensures equal contribution during training

---

### 3. Autoencoder Model
A dense autoencoder is used to learn normal behavioural patterns.

Architecture:
Input → 32 → 16 → 8 → 16 → 32 → Output


- The encoder compresses behavioural features into a lower-dimensional representation
- The decoder reconstructs the original input
- Model is trained using Mean Squared Error (MSE) loss and Adam optimizer

The key idea is:
> The model becomes good at reconstructing normal behaviour but struggles with unusual patterns.

---

### 4. Anomaly Detection
After training, anomaly scores are computed using reconstruction error:
MSE = mean((original - reconstructed)^2)


- Low reconstruction error → normal behaviour
- High reconstruction error → anomalous behaviour

A threshold is defined as:
Threshold = mean(training error) + 2 × std(training error)


- Values above this threshold are classified as anomalies

---

### 5. Interpretation Layer (Psychology-Informed Mapping)
To improve interpretability, a rule-based layer maps anomalies to behavioural constructs:

- **Boundary Crossing** → high after-hours activity or multiple host access  
- **Behavioural Volatility** → high variability in activity timing  
- **Impulsive Spike** → significantly high anomaly score  
- **Persistence** → repeated anomalies for the same user  

Additionally, feature-wise reconstruction error is used to identify the **top contributing features** for each anomaly.

This step bridges the gap between detection and explanation.

---

## Results

- Total user-day records generated: **61,198**
- Number of behavioural features: **11**
- Training loss reduced from **1.03 → 0.84**, indicating successful learning of normal patterns

### Anomaly Detection
- Threshold value: **3.43**
- Total anomalies detected: **643**

### Observations
- Most anomaly scores were concentrated near lower values, representing normal behaviour
- A small number of records had significantly high scores (above 18), indicating strong deviation
- Detected anomalies often showed:
  - high after-hours activity
  - unusual host access patterns
  - irregular activity timing

### Interpretation
The psychology-informed layer provided meaningful explanations for anomalies:
- Not just identifying *what is anomalous*
- But explaining *how the behaviour deviates*

This improves usability in SOC environments, where analysts require context for investigation.

---

## Technologies Used

- Python
- Pandas (data processing)
- Scikit-learn (scaling and preprocessing)
- PyTorch (autoencoder model)
- Matplotlib (visualization)

---

## How to Run

1. Open the notebook in Jupyter or Google Colab  
2. Upload the dataset (CERT logon/logoff data: https://doi.org/10.1184/R1/12841247)  
3. Run all cells sequentially  
4. View:
   - training loss curve  
   - anomaly score distribution  
   - final results table  

---

## Key Takeaways

- Behavioural modelling is effective for detecting insider threats  
- Autoencoders can identify anomalies without labelled data  
- Reconstruction error is a strong signal for deviation  
- Interpretation is essential — anomaly scores alone are not sufficient  
- Combining machine learning with behavioural mapping improves real-world usability  

---

## Future Work

- Extend to other data streams (HTTP, removable devices)
- Build multi-stream ensemble models
- Incorporate contextual features (user role, department)
- Improve thresholding using adaptive methods
