# 🚗 Random Forest IDS for Automotive CAN Networks  
This project implements a Machine Learning-based Intrusion Detection System (IDS) specifically designed to protect the Controller Area Network (CAN) of modern vehicles.

The system leverages an optimized Random Forest classifier to detect malicious injections, such as Fuzzing and Replay attacks, which exploit the lack of inherent security (no encryption or authentication) in the broadcast-based CAN protocol.

## 🚀 Key Features  
Custom Data Pipeline: A dedicated Python-based preprocessing routine that scales and translates raw hexadecimal CAN values (such as 0x181) into base-10 decimal integers for machine learning computation.

Embedded Optimization Constraints: The tree model complexity is strictly constrained to 100 estimators (n_estimators=100), a maximum depth of 12 (max_depth=12), and 500 maximum leaf nodes (max_leaf_nodes=500). This balances fast, real-time message checking latency with a tiny storage size footprint suitable for edge automotive electronic control units (ECUs).

Targeted Attack Detection: Specifically flags Fuzzing attacks (random payload injections into message IDs) and Replay attacks (re-transmitting valid byte sequences to manipulate system states).

High Operational Sensitivity: Achieves an exceptional True Positive rate by recognizing sudden, non-linear payload adjustments and statistical anomalies in message transmission frequency on the bus.

## 🛠️ Tech Stack  
Language: Python

Environment: Jupyter Notebook / VS Code Interactive Mode

Algorithms: Random Forest Classifier (Ensemble Model)

Dataset Pool: CloudIDS Dataset matrix — raw CAN frames gathered from real-world vehicles.

## 📊 Performance Metrics
The model was evaluated using a 20% hold-out test split consisting of 265,584 frames. To handle the unbalanced nature of CAN traffic, the class_weight='balanced' parameter was utilized.  
| Metric    | Score  |
|-----------|--------|
| Accuracy  | 91.65% |
| Precision | 65.99% |
| Recall    | 85.55% |
| F1-Score  | 75.62% |

| Footprint | 14.55 MB |

## Confusion Matrix Summary  
True Negatives (TN): 208,994 (Benign automotive traffic allowed unhindered)

True Positives (TP): 34,408 (Malicious injections successfully caught and isolated)

False Negatives (FN): 4,447 (Missed attack frames — Critical vehicle safety risk managed)

False Positives (FP): 17,735 (False alarms triggered on legitimate messages)

## 📂 Methodology Workflow  
Data Acquisition: Loading the multi-column space-separated log dataset featuring CAN timestamp tracking indices, identifiers, Data Length Codes (DLC), and 8-byte data payloads ($1,327,919$ frames, $14$ structural columns).

Preprocessing Pipeline: Element-wise string parsing to integer decimals via a custom hex_converter utility.

Data Matrix Separation: Extracting independent operational features ($X$) representing the "heartbeat" of the vehicle while segregating the terminal "ground truth" tracking index ($y$).

Model Training: Fitting the ensemble Random Forest decision tree matrix with explicit real-time embedded hyperparameter limits.

System Validation: Plotting the visual Receiver Operating Characteristic (ROC) curve and the Precision-Recall (P-R) data curves side-by-side to ensure alert integrity despite severe data imbalance.

## 🔮 Future Work & References
Temporal Feature Extraction: Incorporating fine-grained inter-arrival times (delta time parameters between message transfers) to drive down false alarms during unusual vehicle driving modes.

Hybrid Classification Models: Combining Random Forest with recurrent neural networks, such as Long Short-Term Memory (LSTM) layers, to trace complex temporal dependencies and counter sequence-based cyber attacks.

Dataset Reference Source: T. Andreica and B. Groza, "CloudIDS: A Cloud-based Intrusion Detection System for Vehicles," GitHub Repository, 2021. [Online]. Available: https://github.com/andrtu2/CloudIDS.
