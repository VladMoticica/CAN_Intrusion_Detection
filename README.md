# 🚗 Random Forest IDS for Automotive CAN Networks  
This project implements a Machine Learning-based Intrusion Detection System (IDS) specifically designed to protect the Controller Area Network (CAN) of modern vehicles.  

The system leverages an optimized Random Forest classifier to detect malicious injections, such as Fuzzing and Replay attacks, which exploit the lack of inherent security in the CAN protocol.  

## 🚀 Key Features  
Custom Data Pipeline: A dedicated Python-based preprocessing routine that converts raw hexadecimal CAN frames into decimal integers for mathematical processing.  

Embedded Optimization: The model is constrained to 100 estimators to balance high-speed detection latency with the limited memory footprint of automotive ECUs.  

Attack Detection: Specifically identifies Fuzzing attacks (random data injection) and Replay attacks (re-transmitting valid sequences to disrupt system states). 

High Performance: Achieves a high True Positive rate by identifying statistical anomalies in message frequency and payload data.  

## 🛠️ Tech Stack  
Language: Python   
Environment: Jupyter Notebook   
Algorithms: Random Forest Classifier (Ensemble Learning)   
Dataset: CloudIDS Dataset — raw CAN frames from real-world vehicles.  

## 📊 Performance Metrics
The model was evaluated using a 20% hold-out test split consisting of 265,584 frames. To handle the unbalanced nature of CAN traffic, the class_weight='balanced' parameter was utilized.  
| Metric   | Score  |
|----------|--------|
| Accuracy | 94.39% |
| Recall   | 85.32% |
| F1-Score | 81.64% |

## Confusion Matrix Summary  
True Negatives: 217,521 (Legitimate frames correctly identified)  
True Positives: 33,153 (Attacks successfully caught)  
False Negatives: 5,702 (Missed attacks - critical safety risk)  
False Positives: 9,208 (False alarms)  

## 📂 Methodology Workflow  
Data Acquisition: Loading the CloudIDS dataset featuring CAN IDs, DLC, and 8-byte data payloads. 

Preprocessing: * Hexadecimal conversion using a custom hex_converter function.  

Feature (CAN heartbeat) and Label (Ground truth) separation.  

Model Training: Training the Random Forest with optimizations for real-time embedded execution.  

Validation: Analyzing ROC and Precision-Recall curves to ensure reliability across detection thresholds.  

## 🔮 Future Work & References
Temporal Features: Integrating precise inter-arrival times between messages to reduce false positives.  

Hybrid Architectures: Combining Random Forest with Long Short-Term Memory (LSTM) neural networks to track long-term sequences and secure against Advanced Persistent Threats (APTs).  

Dataset Source: Andreica and B. Groza, "CloudIDS: A Cloud-based Intrusion Detection System for Vehicles".  
