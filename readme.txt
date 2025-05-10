# Colorectal Cancer Analysis Project

![Project Banner](https://img.shields.io/badge/Project-Colorectal%20Cancer%20Analysis-blue)
![Python](https://img.shields.io/badge/Python-3.11.9-brightgreen)
![MLflow](https://img.shields.io/badge/MLflow-Tracking-red)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 📋 Overview

This project provides an end-to-end machine learning pipeline for colorectal cancer analysis using a modern MLOps stack. The pipeline includes data preprocessing, feature engineering, model training, evaluation, and deployment capabilities using MLflow and Kubernetes.

## 🛠️ Tech Stack

- **Programming Language**: Python
- **Development Environment**: Jupyter Notebook
- **Version Control**: Git & GitHub
- **Experiment Tracking**: MLflow
- **Remote Experiment Repository**: DagsHub
- **Deployment Tools**: Kubernetes, Kubeflow, Minikube

## 🚀 Installation & Setup

### Prerequisites

- Python 3.11.9 or higher
- Git
- VS Code (recommended)

### Step 1: Check Python Installation

```bash
python --version
```

Expected output:
```
Python 3.11.9
```

### Step 2: Clone the Repository

```bash
git clone <github url>
cd cancer_colorectal
```

### Step 3: Set Up Python Virtual Environment

```bash
python -m venv .venv
```

### Step 4: Activate the Virtual Environment

**On Windows:**
```bash
.venv\Scripts\Activate
```

**On macOS/Linux:**
```bash
source .venv/bin/activate
```

When activated correctly, you'll see the environment name in your terminal prompt:
```
(.venv) PS C:\Users\YourName\cancer_colorectal>
```

### Step 5: Install Dependencies

```bash
pip install -e .
```

### Step 6: Run the Application

```bash
python application.py
```

## 📊 MLflow Experiment Setup

The project uses MLflow for both local experiment tracking and remote tracking through DagsHub.

### Setting Up Environment Variables for Remote Tracking

**On Windows PowerShell:**
```powershell
$env:MLFLOW_TRACKING_PASSWORD = "c1c7ea37e46eaaf3415d10baa9b057ca0c9a6aeb"
$env:MLFLOW_TRACKING_USERNAME = "jayzalani"
$env:MLFLOW_TRACKING_URI = "https://dagshub.com/jayzalani/cancer_coloectral.mlflow"
```

**On macOS/Linux:**
```bash
export MLFLOW_TRACKING_PASSWORD="c1c7ea37e46eaaf3415d10baa9b057ca0c9a6aeb"
export MLFLOW_TRACKING_USERNAME="jayzalani"
export MLFLOW_TRACKING_URI="https://dagshub.com/jayzalani/cancer_coloectral.mlflow"
```

### Running Model Training

To test that the training pipeline works correctly:

```bash
python src/model_training.py
```

### Viewing MLflow Dashboard

Start the MLflow user interface:

```bash
mlflow ui
```

After running the command, you'll see a URL (typically `http://127.0.0.1:5000`) in your terminal. Press `Ctrl` + click on this link to open the MLflow dashboard in your browser.

## 📐 Project Architecture

The project follows a modular architecture for training and deploying machine learning models:

```
cancer_colorectal/
├── .venv/                  # Virtual environment
├── src/                    # Source code
│   ├── data_processing/    # Data preprocessing modules
│   ├── model_training.py   # Model training script
│   └── utils/              # Utility functions
├── notebooks/              # Jupyter notebooks for exploration
├── tests/                  # Unit tests
├── models/                 # Saved model artifacts
├── configs/                # Configuration files
├── k8s/                    # Kubernetes deployment files
├── application.py          # Main application entry point
├── setup.py                # Package setup file
└── README.md               # Project documentation
```

## 🔄 MLOps Workflow

1. **Data Ingestion**: Load and preprocess the colorectal cancer dataset
2. **Feature Engineering**: Extract meaningful features from raw data
3. **Model Training**: Train various ML models with hyperparameter tuning
4. **Evaluation**: Assess model performance using appropriate metrics
5. **Experiment Tracking**: Log all parameters, metrics, and artifacts with MLflow
6. **Deployment**: Deploy models using Kubernetes and Kubeflow

## 🧪 Running Tests

```bash
pytest tests/
```

## 🚢 Kubernetes Deployment

The project includes configuration for deploying the model as a service using Kubernetes:

1. Ensure Minikube is installed and running
2. Apply the Kubernetes configurations:

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

## 📈 DagsHub Integration

The project uses DagsHub for remote experiment tracking. View experiments at:
[https://dagshub.com/jayzalani/cancer_coloectral](https://dagshub.com/jayzalani/cancer_coloectral)

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👥 Contributors

- Jay Zalani

## 📫 Contact

For any questions or suggestions, please open an issue on GitHub or contact the maintainers.

---

**Note**: For detailed information about the project workflow and architecture, please refer to the `NOTES.pdf` file included in the repository.
