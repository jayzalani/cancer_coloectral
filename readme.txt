# Cancer Colorectal Project 

## Tech Stack 
- Python
- Jupyter Notebook
- GitHub
- DagsHub
- MLflow
- Kubernetes
- Kubeflow
- Minikube

## Setup Instructions

### Install Python on Your Local Machine

Check installation by running this command in your terminal:
```
python --version
```
After running, this output should appear (if not, there's a problem with the installation):
```
Python 3.11.9
```

### Project Setup

1. **Clone the project**
   - Make a folder, then inside that folder run this command in VS Code terminal:
   ```
   git clone <github url>
   ```

2. **Generate Python virtual environment**
   - This step is important:
   ```
   python -m venv .venv
   ```
   - After successful execution of this command, there should be a folder named `.venv` in your project directory.

3. **Start the virtual environment**
   ```
   .venv\Scripts\Activate
   ```
   - If done correctly, you'll see a small green text with the environment name.

4. **Install requirements**
   - Run this command to download all requirements listed in the requirements.txt file:
   ```
   pip install -e .
   ```
   - Copy this command and paste it into the VS Code terminal where the environment setup is done.

5. **Start the application**
   - Once everything is installed, run this command:
   ```
   python application.py
   ```

## MLflow Experiment Setup

We use MLflow for local experiment tracking and DagsHub for online tracking, which is common in industry-grade software.

### Configure Environment Variables

First, set up environment variables by copying these commands and pasting them into the VS Code terminal where the environment is activated:

```
$env:MLFLOW_TRACKING_PASSWORD = "c1c7ea37e46eaaf3415d10baa9b057ca0c9a6aeb"
$env:MLFLOW_TRACKING_USERNAME = "jayzalani"
$env:MLFLOW_TRACKING_URI = "https://dagshub.com/jayzalani/cancer_coloectral.mlflow"
```

### Start MLflow and Run Experiments

Once the variables are set up, run these commands:

1. **Check if the code is working on model_training**
   ```
   python src/model_training.py
   ```

2. **Start the MLflow dashboard**
   ```
   mlflow ui
   ```

After everything is done correctly, there will be a link for the dashboard in your terminal. Press Ctrl and click on that link to open the MLflow dashboard.

## Project Workflow

For detailed information about the project workflow and architecture, please refer to the PDF and NOTES.pdf files included in the repository.
