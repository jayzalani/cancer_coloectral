# cancer_coloectral Project 
## Tech stack 
    Python
    Jupyter notebook
    Github
    Dagshub
    mlflow
    Kubernetes
    kubeflow
    Minikube

## Setup Instruction

    Install python on you Local Machine

    Check installation 
    run this command on your terminal first 
    `python --version`
    After running this output must be appear if not then there's problem in Installations
    `Python 3.11.9 `

    After proper installation of python 
    
    Git Clone this porject 
    make a folder then inside that folder run this command in vs code terminal
    `git clone <github url>`
    
    generate env setup used for Python this is IMP 
    `python -m venv .venv`
    after succcessfull of this command there must be a folder name .venv in your project directory
    Now do Start the env system by running this command
    `.venv/Scripts/Activate`
    if done correctly then samll green Test should appear like this 
    [image]

    Now actual project setup
    now First run this command to download every requirements listed on requirements.txt file
    ` pip install -e . `
    copy this command and past into the vs code terminal where the env setup is donne

    Once every thing install run this command to start ypur application
    `python application.py`
    
## Mlflow Expirement Setup
### We have used mlflow for local experiement tracking to start this dashboard use this command flow
and for online tracking we have used Dagshub, 
first setup envirement variable by copying this commands and past into the vs code terminal where envirement setup is started
`$env:MLFLOW_TRACKING_PASSWORD = "c1c7ea37e46eaaf3415d10baa9b057ca0c9a6aeb"
$env:MLFLOW_TRACKING_USERNAME = "jayzalani"
$env:MLFLOW_TRACKING_URI = "https://dagshub.com/jayzalani/cancer_coloectral.mlflow"`

### Once this is setup run this commands to get started with the dashboard locally 
    first check for the code is working on file model_training
    `python src/model_training.py`
    
    and for the dashboard
    `mlflow ui`

    for more understand follow this image after everything done correctly there will be link for dashboard press ctrl and click on that link this will open mlflow dashboard

    mlflow allow for the local experiement tracking while the dagshub allow online tracking which is most used in industry grade software


# Flow and diagrams are in the PDF and NOTES.pdf file check it!
 