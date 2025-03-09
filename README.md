# Create a README.md file with the provided content

readme_content = """\
# CLO835 Assignment 2: Flask and MySQL on Kubernetes

## 📌 Project Overview
Hey there! This project is my take on **CLO835 Assignment 2**. I’ve set up a **Flask web app** that displays a "Hello, World!" message and a **MySQL database**, all running on a **Kubernetes cluster (Kind) inside an AWS EC2 instance**.

The **Flask app is accessible on port `30000`**, while MySQL stays in the backend.  
I started with **Version 1 (Blue)** and later upgraded it to **Version 2 (Green)**.  
Stick around to see how I set it up and how you can try it yourself!

---

## ✅ **Prerequisites**
Before jumping in, make sure your **EC2 instance** has these tools installed:

### **1️⃣ Install AWS CLI**
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

### 2️⃣ Install Docker
sudo yum install -y docker
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user

3️⃣ Install Kind (Kubernetes in Docker)
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

4️⃣ Install kubectl (Kubernetes CLI)
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

📥 Cloning the Project
git clone https://github.com/Arpit-commits/Arpit-CLO835-Assignment2.git
cd Arpit-CLO835-Assignment2


🚀 Step 1: Deploy Version 1 (Blue Theme)
1️⃣ Switch to Version 1
git checkout version1
git reset --hard version1


2️⃣ Create the Kubernetes Cluster
kind create cluster --config k8s-manifests/kind-config.yaml --name clo835-cluster

3️⃣ Verify the Cluster
kubectl cluster-info --context kind-clo835-cluster

4️⃣ Create Kubernetes Namespaces
kubectl create namespace flask
kubectl create namespace sql

5️⃣ Create ECR Secrets
kubectl create secret docker-registry ecr-secret --docker-server=135893829551.dkr.ecr.us-east-1.amazonaws.com --docker-username=AWS --docker-password=$(aws ecr get-login-password --region us-east-1) -n flask
kubectl create secret docker-registry ecr-secret --docker-server=135893829551.dkr.ecr.us-east-1.amazonaws.com --docker-username=AWS --docker-password=$(aws ecr get-login-password --region us-east-1) -n sql

6️⃣ Deploy MySQL & Flask Services
kubectl apply -f k8s-manifests/sql-service.yaml
kubectl apply -f k8s-manifests/flask-service.yaml

7️⃣ Deploy the Flask & MySQL Applications
kubectl apply -f k8s-manifests/mysql-deployment.yaml
kubectl apply -f k8s-manifests/flask-deployment.yaml

8️⃣ Check Running Pods
kubectl get pods -n flask
kubectl get pods -n sql

9️⃣ Test Version 1
curl http://<EC2-Public-IP>:30000

✅ Expected Output:
Hello from WebApp - Version 1 (Blue)


🚀 Step 2: Upgrade to Version 2 (Green Theme)

1️⃣ Switch to Version 2
git checkout version2
git reset --hard version2


2️⃣ Apply the Updated Flask Deployment

kubectl apply -f k8s-manifests/flask-deployment.yaml
kubectl rollout status deployment/flask-deployment -n flask

3️⃣ Test Version 2
curl http://<EC2-Public-IP>:30000
✅ Expected Output:
Hello from WebApp - Version 2 (Green)


🎥 Final Notes

    Security Groups: Make sure port 30000 is open in AWS EC2 Security Groups.
    GitHub Branches: Version 1 = Blue Theme, Version 2 = Green Theme.
    Video Submission: Check out my demo video here: [Insert Link Here].

