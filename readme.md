# 🏥 Colorectal Cancer Survival Prediction — MLOps Pipeline

An end-to-end production-grade MLOps pipeline for predicting colorectal cancer survival probability from patient clinical data. The project emphasizes pipeline automation, experiment tracking, and containerized deployment over raw model performance.

---

## 📌 Project Highlights

- Trained on **167,497 patient records** across 27 clinical features
- **Chi-square feature selection** reduced 27 features to 5 most significant
- **100% recall** on survival class — critical for medical prediction use cases
- Full **MLOps pipeline** from data ingestion to containerized deployment
- **Experiment tracking** via MLflow + DagsHub for versioned model management
- **Kubeflow pipeline** for orchestrated, reproducible ML workflows on Kubernetes

---

## 🛠️ Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.11 |
| ML & Data | Scikit-learn, Pandas, NumPy, Matplotlib, Seaborn |
| Experiment Tracking | MLflow, DagsHub |
| Pipeline Orchestration | Kubeflow (KFP), Minikube |
| Containerization | Docker |
| Version Control | GitHub |
| Web Framework | Flask |
| Notebook | Jupyter |

---

## 🏗️ Architecture

```
Raw Data (CSV)
      │
      ▼
┌─────────────────┐
│  ETL Pipeline   │  ← Label Encoding, Chi-Square Feature Selection,
│ data_processing │    Stratified Split, Standard Scaling
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Training Pipeline│  ← Gradient Boosting Classifier
│ model_training  │    MLflow Experiment Tracking
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Flask App     │  ← REST API for real-time predictions
│  application.py │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│Kubeflow Pipeline│  ← Containerized DAG orchestration
│  on Kubernetes  │    via Minikube
└─────────────────┘
```

---

## 📊 Model Performance

| Metric | Value |
|---|---|
| Dataset Size | 167,497 records |
| Features Selected | 5 of 27 (chi-square) |
| Algorithm | Gradient Boosting Classifier |
| Recall (Survival class) | 100% |
| Precision (Survival class) | 60% |

> **Note:** High recall is prioritized over precision in this medical context — missing a true survivor carries higher cost than a false positive. Known improvement for next iteration: address class imbalance using SMOTE and apply One-Hot Encoding for nominal categorical features.

---

## 📁 Project Structure

```
├── artifacts/
│   ├── raw/                  # Raw input data
│   ├── processed/            # Processed features, scaler
│   └── models/               # Trained model pickle
├── kubeflow_pipeline/
│   └── mlops_pipeline.py     # Kubeflow DAG definition
├── notebook/
│   └── notebook.ipynb        # EDA and experimentation
├── src/
│   ├── data_processing.py    # ETL pipeline
│   ├── model_training.py     # Training + MLflow logging
│   ├── logger.py             # Centralized logging
│   └── custom_exception.py   # Error handling
├── static/                   # Flask CSS
├── templates/                # Flask HTML templates
├── application.py            # Flask prediction app
├── dockerfile                # Container definition
├── mlops_pipeline.yaml       # Compiled Kubeflow pipeline
├── requirements.txt
└── setup.py
```

---

## ⚙️ Setup Instructions

### Prerequisites
- Python 3.11.9
- Git

### 1. Clone the Repository

```bash
git clone https://github.com/jayzalani/cancer_coloectral.git
cd cancer_coloectral
```

### 2. Create Virtual Environment

```bash
python -m venv .venv
```

### 3. Activate Virtual Environment

**Windows:**
```bash
.venv\Scripts\Activate
```

**Mac/Linux:**
```bash
source .venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -e .
```

### 5. Run ETL Pipeline

```bash
python src/data_processing.py
```

### 6. Train Model

```bash
python src/model_training.py
```

### 7. Start Flask App

```bash
python application.py
```

The app will be available at `http://localhost:5000`

---

## 📈 MLflow Experiment Tracking

This project uses MLflow locally and DagsHub for remote tracking — a common industry pattern for collaborative ML teams.

### Configure DagsHub Tracking (Optional)

```bash
# Windows PowerShell
$env:MLFLOW_TRACKING_URI = "https://dagshub.com/<your_username>/<your_repo>.mlflow"
$env:MLFLOW_TRACKING_USERNAME = "<your_username>"
$env:MLFLOW_TRACKING_PASSWORD = "<your_token>"
```

### Run Training with Tracking

```bash
python src/model_training.py
```

### Launch MLflow Dashboard

```bash
mlflow ui
```

Navigate to `http://127.0.0.1:5000` to view experiment runs, metrics, and model versions.

---

## ☸️ Kubeflow Pipeline (Kubernetes Orchestration)

The pipeline is defined as a DAG using Kubeflow Pipelines SDK:

```
[Data Processing] ──→ [Model Training]
```

Each step runs in an isolated Docker container, enabling reproducible and scalable ML workflows.

### Compile Pipeline

```bash
python kubeflow_pipeline/mlops_pipeline.py
```

This generates `mlops_pipeline.yaml` which can be uploaded to a Kubeflow dashboard running on Minikube or any Kubernetes cluster.

---

## 🔬 ETL Pipeline Details

The `DataProcessing` class in `src/data_processing.py` handles:

1. **Data Loading** — reads raw CSV from `artifacts/raw/`
2. **Preprocessing** — drops identifier columns, label encodes categorical features
3. **Feature Selection** — chi-square test selects top 5 most significant features
4. **Train/Test Split** — stratified 80/20 split preserving class distribution
5. **Standard Scaling** — scales features; scaler fitted only on training data to prevent leakage
6. **Artifact Saving** — persists processed data and scaler as pickle files

---

## 🤖 Model Training Details

The `ModelTraining` class in `src/model_training.py` handles:

1. **Load Processed Data** — reads pickle artifacts from ETL pipeline
2. **Train** — Gradient Boosting Classifier (n_estimators=100, learning_rate=0.1, max_depth=3)
3. **Evaluate** — logs accuracy, precision, recall, F1, ROC-AUC to MLflow
4. **Save Model** — persists trained model to `artifacts/models/model.pkl`

---

## 🌐 Flask Prediction App

Users input 5 clinical features via a web form:
- Healthcare Costs
- Tumor Size (mm)
- Treatment Type
- Diabetes (0/1)
- Mortality Rate per 100K

The app loads the trained model and the **same scaler used during training** to ensure consistent feature transformation at inference time.

---

## 🔮 Known Limitations & Next Iterations

- [ ] Address class imbalance using SMOTE or class_weight parameter
- [ ] Add k-fold cross-validation for more robust evaluation
- [ ] Replace Label Encoding with One-Hot Encoding for nominal features (e.g. Country)
- [ ] Implement hyperparameter tuning via GridSearchCV
- [ ] Add CI/CD pipeline with Jenkins or GitHub Actions
- [ ] Add model monitoring and drift detection in production

---

## 📄 License

This project is open source and available under the MIT License.
