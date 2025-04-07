# V-Patrol: Network Anomaly Detection 🛡️

[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/Naereen/StrapDown.js/graphs/commit-activity)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/dwmkerr/effective-java/blob/master/CONTRIBUTING.md)

## Overview 💡

V-Patrol is a network anomaly detection system designed to identify suspicious activities 🕵️‍♂️, assess network health 🩺, and mitigate potential security threats 🚨. It leverages feature extraction ⚙️, data analysis 📊, and machine learning techniques 🤖 to proactively detect anomalies and bolster network defenses 🛡️.

## Features ✨

*   **Comprehensive Feature Extraction ⚙️:** Extracts a wide range of network traffic and device metadata features.
*   **Real-time Threat Detection ⏱️:** Monitor various threats, like DDoS Attack, Phishing Attacks and credential-stuffing.
*   **Haversine Formula Implementation 🗺️:** Uses a formula to find the different between IP Geolocation and device GPS.
*   **Iterative Model Refinement 🔄:** Employs an iterative process to refine hyperparmeters of model.
*   **BERT-Based Analysis 🧠:** Utilizes BERT embeddings to assess User-Agent string and metadata consistency.
*   **Anomaly Detection 🤖:** Leverages the Isolation Forest algorithm for anomaly detection.
*   **Geolocation Analysis 📍:** Identifies location-based anomalies, including impossible travel and mismatched country codes.

## Project Structure 📂


V-Patrol/
├── anomaly_map.html # 🌍 Interactive map of anomalies
├── CombinedCountryData_2.0-IPv4_Cleaned.xlsx # 📊 Cleaned IPv4 dataset
├── final.csv # 🧾 Final processed dataset
├── ip_api.ipynb # 📍 IP geolocation notebook
├── uniqueIPs.csv # 📑 Unique IP addresses
├── V-Patrol Final Report.docx.pdf # 📄 Final project report
│
├── featureData/ # 💾 Extracted features
│ ├── feature_1_2.csv
│ ├── feature_1_2_graph.csv
│ ├── feature_3.csv
│ ├── feature_4_5_6.csv
│ ├── feature_7.csv
│ ├── feature_8.csv
│ └── feature_9.csv
│
├── forEachFeature/ # 📓 Feature-wise notebooks
│ ├── feature1n2.ipynb
│ ├── feature3.ipynb
│ ├── feature4n5n6.ipynb
│ ├── feature7.ipynb
│ ├── feature8.ipynb
│ └── feature9.ipynb
│
└── modeling/ # 🧠 Modeling experiments
├── model.ipynb
├── model1.ipynb
└── model2.ipynb

## Methodology 🧪

The V-Patrol project follows these key steps:

1.  **Data Acquisition 📥:** Obtain network traffic data and device metadata from relevant sources.
2.  **Feature Extraction ⚙️:** Extract key features from the raw data, including:
    *   Request frequencies, device contribution ratios, and burstiness metrics.
    *   IP geolocation data and device location information.
    *   User-Agent strings and device metadata.
3.  **Data Preprocessing 🧹:** Clean and normalize the data to ensure data quality and consistency.
4.  **Feature Engineering 🛠️:** Create new features to enhance anomaly detection capabilities (e.g., rolling unique counts, difference calculations).
5.  **Model Training 🏋️:** Train an Isolation Forest model to identify anomalies based on the extracted and engineered features.
6.  **Model Evaluation ✅:** Evaluate the model's performance using appropriate metrics (e.g., silhouette score) and visualizations.
7.  **Iterative Refinement 🔄:** Refine the model by adjusting hyperparameters, selecting relevant features, and exploring alternative modeling techniques.
8.  **Deployment (Optional) 🚀:** Deploy the trained model for real-time anomaly detection in a production environment.

## Feature Analysis 🕵️

### Network Traffic Metrics 🌐

*   **Requests Per Device Per Second:** Used to identify devices generating unusually high traffic, indicating malicious activity or misconfiguration.
*   **Device Contribution Ratio:** Helps identify dominant devices and assess their impact on network load.
*   **Burstiness Analysis:** Detects irregular traffic patterns that may signal botnet activity or automated scanning.

### Anomaly Detection Features 🚨

The model also accounts for certain anomalies which includes:
*   **Height and Width Mismatch.**
*   **IP Address Count Difference & Carrier Count Difference.**
*   **Carrier Count Difference & App Bundle Count Difference.**
*   **Impossible IPs & Country Code Mismatch.**
*   **Country Code Mismatch & Normalized Distance.**
*   **IP Address Count Diff & Connection Type Count Diff.**

### Device Data Cleaning and Anomaly Detection 📱

*   **Missing Vendor Information:** Flags devices lacking vendor details, potentially indicating anonymization.
*   **Device Consistency Checks:** Identifies inconsistencies in OS, OS version, height, and width.
*   **OS Version Normalization:** Flags mismatches between OS version and normalized OS version.

### IP Address and Carrier Data Cleaning 📡

*   **Missing Carrier Information Detection:** Identifies rows where carrier information is missing.
*   **Impossible IP Addresses:** Flags fake or invalid IP addresses.
*   **Country Code Mismatch Detection:** Flags mismatches between IP-based geolocation and device country code.

### IP Geolocation and Distance Normalization 📍

*   **Haversine Distance Calculation:** Measures the distance between device GPS coordinates and IP-based geolocation.
*   **Distance Normalization:** Normalizes Haversine distances for comparison.

### Rolling Unique Counts 🔄

*   **Rolling counts on diverse features**: A pandas rolling window was created to make a count of distinct IP addresses, carrier networks, app bundles, and connections per minute.

### BERT-Based Embedding and Similarity 💬

*   **BERT Embeddings:** Uses natural language processing to generate vector representations of User-Agent (UA) strings and device metadata.
*   **Cosine Similarity:** Calculates the cosine similarity between UA and metadata embeddings to detect mismatches.

## Results and Visualizations 📈

*   **Iterative Model Improvement:**
    *   Best parameters: {'n_estimators': 100, 'max_samples': 256, 'contamination': 0.1, 'max_features': 0.9, 'bootstrap': False} Best score: 0.6556688332880479:
*   A feature selection step was performed after obtaining output2:
    *   Best parameters: {'n_estimators': 150, 'max_samples': 128, 'contamination': 0.1602582555413908, 'max_features': 0.9, 'bootstrap': False} Best score: 0.719502379676749
*   The final iteration served to validate the optimal hyperparameter configuration identified in the previous stage:
    *   Best parameters: {'n_estimators': 150, 'max_samples': 64, 'contamination': 0.1, 'max_features': 0.9, 'bootstrap': False} Best score: 0.7301869661156942
*   Final Results: Silhouette Score of 0.76 and A total of 10.23% Anomalies flagged.

These helped detect :
*   **Device spoofing is suggested by strong correlations between height and width mismatches. 📱**
*   **Geo-spoofing is potentially indicated by impossible IPs and country mismatches. 📍**
*   **Normal network behavior can account for some changes, such as IP and connection type differences for mobile users. 📶**

## Setup ⚙️

1.  **Clone the repository:**

    ```bash
    git clone [repository_url]
    cd V-Patrol
    ```

2.  **Create a virtual environment (recommended) 📦:**

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Linux/macOS 🐧🍎
    venv\Scripts\activate  # On Windows 🪟
    ```

3.  **Install the required dependencies 🐍:**

    ```bash
    pip install -r requirements.txt
    ```

## Usage 🚀

1.  **Data Preparation 📝:** Ensure your network traffic data is in a compatible format (e.g., CSV, Excel). Place your data files in the `data/` directory.

2.  **Run the Analysis 🏃:**

    *   Utilize the Jupyter notebooks in the `notebooks/` directory to perform feature extraction, data analysis, and model training.
    *   Alternatively, run the Python scripts in the `scripts/` directory to automate specific tasks.

3.  **Explore the Results 🔭:**

    *   View the generated visualizations in the `visualizations/` directory.
    *   Examine the model outputs and anomaly reports.

## Future Scope 🔮

V-Patrol is always improving! Here are some possible extensions to add in. Contributors are Welcome!:

*   **Neural Network Models:** Investigate the application of neural network models, such as autoencoders, to better capture temporal dependencies and identify more subtle anomalies.
*   **Reconstruction Error Analysis:** Utilize the reconstruction error from autoencoders to identify anomalies. Higher reconstruction errors for temporal data will imply the data point as anomalies.

## License 📜

This project is licensed under the MIT License - see the `LICENSE` file for details.
