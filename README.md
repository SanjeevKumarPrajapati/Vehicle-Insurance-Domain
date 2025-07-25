# 🚗 Vehicle Data ML Pipeline with MLOps

This project sets up a complete end-to-end **Machine Learning pipeline** with **MongoDB**, **AWS**, **Docker**, and **CI/CD integration** using **GitHub Actions**. It includes data ingestion, transformation, model training, deployment, and monitoring capabilities — all built in a modular and scalable way.

---

## 📁 Project Setup Instructions

### 1️⃣ Project Initialization

```bash
python template.py
2️⃣ Package Setup
Add code to setup.py and pyproject.toml to enable local package imports.

Reference guide: crashcourse.txt

🐍 Virtual Environment & Dependencies
bash
Copy
Edit
conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt
pip list  # Verify local packages
🍃 MongoDB Atlas Setup
Create Project on MongoDB Atlas.

Create Cluster → Select M0 → Default settings → Create Deployment.

Add User: Username + Password.

Network Access: Allow IP 0.0.0.0/0.

Get Connection String: Select Python driver → Copy connection URI.

Save URI (replace <password>).

Create folder notebook → Add dataset + mongoDB_demo.ipynb → Select kernel vehicle.

Push data to MongoDB using notebook.

View data: MongoDB → Database → Browse Collections.

📝 Logging, Exception Handling & EDA
logger.py and exception.py tested via demo.py.

Added EDA & Feature Engineering notebook.

📥 Data Ingestion Pipeline
Declare constants → constants/__init__.py.

Mongo connection setup → configuration/mongo_db_connection.py.

Fetch data → data_access/proj1_data.py.

Update entities:

entity/config_entity.py

entity/artifact_entity.py

Add ingestion logic → components/data_ingestion.py.

Call pipeline from training_pipeline.py.

Set MongoDB URI:

🔗 MongoDB URI Setup
Mac/Linux:

bash
Copy
Edit
export MONGODB_URL="mongodb+srv://<username>:<password>@cluster.mongodb.net"
Windows (PowerShell):

powershell
Copy
Edit
$env:MONGODB_URL = "mongodb+srv://<username>:<password>@cluster.mongodb.net"
Also, add /artifact to .gitignore.

✅ Data Validation, Transformation & Model Training
Write dataset schema → config/schema.yaml

Update utils/main_utils.py

Implement:

DataValidation component

DataTransformation component (add estimator.py)

ModelTrainer component (extend estimator.py)

☁️ AWS Configuration for Model Evaluation
1. IAM Setup
Go to AWS Console → IAM → Create user: firstproj

Attach policy: AdministratorAccess

Generate Access & Secret Key

2. Setup Environment Variables
Linux/macOS:

bash
Copy
Edit
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."
PowerShell:

powershell
Copy
Edit
$env:AWS_ACCESS_KEY_ID="..."
$env:AWS_SECRET_ACCESS_KEY="..."
3. Update constants/__init__.py
python
Copy
Edit
MODEL_EVALUATION_CHANGED_THRESHOLD_SCORE = 0.02
MODEL_BUCKET_NAME = "my-model-mlopsproj"
MODEL_PUSHER_S3_KEY = "model-registry"
4. AWS Services
Create S3 Bucket: my-model-mlopsproj

Add AWS interaction code:

src/configuration/aws_connection.py

src/aws_storage/ logic

entity/s3_estimator.py

📊 Model Evaluation & Pusher
Create components:

ModelEvaluation

ModelPusher

🚀 Prediction Pipeline & Web App
Setup prediction structure and app.py

Add:

/static

/template

🔁 CI/CD Pipeline
1. Docker & GitHub Actions
Add:

Dockerfile

.dockerignore

.github/workflows/aws.yaml

2. AWS IAM for GitHub Actions
IAM User: usvisa-user → Generate Access Keys

3. Create ECR Repository
Repo: vehicleproj

4. Launch EC2 Instance
Name: vehicledata-machine

Image: Ubuntu 24.04

Instance: T2 Medium

Create new key pair

Allow HTTP/HTTPS

Connect via EC2 Connect

🐳 Docker Installation on EC2
bash
Copy
Edit
sudo apt update -y
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
🤖 Setup GitHub Runner on EC2
GitHub → Settings → Actions → Runner → New Self-hosted Runner

Follow instructions:

Download

Configure

Run (./run.sh)

Runner should show as "Idle" on GitHub.

🔐 GitHub Secrets
Set these secrets:

AWS_ACCESS_KEY_ID

AWS_SECRET_ACCESS_KEY

AWS_DEFAULT_REGION

ECR_REPO

🌐 Deploy App on Port 5080
Go to EC2 > Security > Inbound Rules

Add Rule:

Type: Custom TCP

Port: 5080

Source: 0.0.0.0/0

Access App:

cpp
Copy
Edit
http://<public-ip>:5080
🔁 Training Route
You can trigger model training by visiting:

arduino
Copy
Edit
http://<public-ip>:5080/training
📌 Project Highlights
✅ Modular & Scalable ML Pipeline

✅ MongoDB Integration

✅ AWS S3 Support

✅ CI/CD via GitHub Actions + Docker

✅ Deployed on EC2 Ubuntu Server

✅ Environment variables for secure secrets

💬 Contributing
Pull requests are welcome. For major changes, open an issue first to discuss what you'd like to change.

📄 License
MIT