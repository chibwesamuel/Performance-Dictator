# Performance Dictator

**Developer**: Samuel Mukosa Chibwe

## Overview

**Performance Dictator** is a student performance prediction system that utilizes machine learning to predict student outcomes based on factors such as attendance, grades, and study hours. The project leverages Python for machine learning, SQL for data management, and various Azure Cloud Services for scalability and deployment.

This application is containerized using Docker and orchestrated with Kubernetes (AKS) for deployment at scale. It also features integration with Azure DevOps for continuous integration and delivery, and Azure Machine Learning for model training and deployment.

## Features
- **Student Performance Prediction**: Predict student grades or pass/fail outcomes.
- **Data Storage**: Securely store and manage student data with SQL.
- **Machine Learning Integration**: Train and deploy models using Azure Machine Learning.
- **Containerization**: Dockerized for portability and easy deployment.
- **Scalable Orchestration**: Deployed and managed on Azure Kubernetes Service (AKS).
- **CI/CD Pipelines**: Automated deployment pipelines using Azure DevOps.

---

## Tech Stack
- **Languages**: Python, SQL
- **Frameworks**: Flask/Django (backend), scikit-learn (machine learning)
- **Cloud**: 
  - Azure Machine Learning
  - Azure Kubernetes Service (AKS)
  - Azure DevOps (CI/CD)
  - Azure Functions (serverless automation)
- **Containerization**: Docker, Kubernetes
- **Version Control**: Git, GitHub
- **Tools**: VS Code, Docker, Azure CLI, Kubernetes, Azure ML SDK

---

## Project Setup

### Prerequisites

Before you begin, ensure you have the following installed:
- **Python 3.x**
- **Git**
- **Docker**
- **Azure CLI**
- **VS Code**
- **Azure DevOps account** (optional for CI/CD)
- **Azure ML account**

### 1. Clone the repository

```bash
git clone https://github.com/chibwesamuel/PerformanceDictator.git
cd PerformanceDictator
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On macOS/Linux
.\venv\Scripts\activate  # On Windows
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the Application Locally

To run the Python app (Flask or Django), use the following:

```bash
python src/main.py
```

### 5. Docker Setup

1. **Build the Docker Image**:

```bash
docker build -t performance-dictator .
```

2. **Run the Docker Container**:

```bash
docker run -p 5000:5000 performance-dictator
```

### 6. Azure Kubernetes Service (AKS) Deployment

1. **Create an AKS Cluster**:

```bash
az aks create --resource-group <resource-group> --name <aks-cluster-name> --node-count 1 --enable-addons monitoring --generate-ssh-keys
```

2. **Deploy the Docker Image to AKS**:

```bash
az acr build --registry <your-registry-name> --image performance-dictator .
kubectl apply -f k8s-deployment.yaml
```

### 7. CI/CD with Azure DevOps

1. **Set up a pipeline in Azure DevOps** to automate building, testing, and deploying to AKS or other environments.
2. **Pipeline Example**:
   ```yaml
   pool:
     vmImage: 'ubuntu-latest'

   steps:
   - task: UsePythonVersion@0
     inputs:
       versionSpec: '3.x'
   - script: |
       python -m venv venv
       source venv/bin/activate
       pip install -r requirements.txt
       python -m unittest discover
     displayName: 'Run Tests'
   - script: |
       docker build -t performance-dictator .
       docker push <your-registry-url>/performance-dictator
     displayName: 'Build and Push Docker Image'
   ```

---

## Azure Machine Learning Integration

You can integrate Azure Machine Learning for model training:

1. **Configure Workspace**:
   ```python
   from azureml.core import Workspace
   ws = Workspace.from_config()
   print("Workspace loaded successfully")
   ```

2. **Train the Model on Azure**:
   ```python
   from azureml.core import Experiment
   experiment = Experiment(ws, 'performance-predictor')
   run = experiment.start_logging()
   ```

---

## Folder Structure

```
PerformanceDictator/
├── data/               # Student data files
├── models/             # Saved ML models
├── src/
    ├── main.py         # Application entry point
    ├── data_prep.py    # Data processing
    ├── train_model.py  # Model training
    ├── app/            # Flask/Django app
├── requirements.txt    # Project dependencies
├── Dockerfile          # Docker image setup
├── k8s-deployment.yaml # Kubernetes deployment config
└── azure-pipelines.yml # Azure DevOps pipeline config
```

---

## Contributing

Contributions are welcome! If you want to contribute, please open an issue or submit a pull request with detailed descriptions of the changes made.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Contact

For any inquiries or support, please reach out to:

**Samuel Mukosa Chibwe**