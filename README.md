# Arpit-CLO835-Assignment2

Video Link - https://drive.google.com/file/d/1JRnIMA1DW_gm6F-M9nHn80vo8EsjQSl4/view?usp=sharing

# Kubernetes Deployment with Kind for CLO835 Assignment 2

## Author: Arpit Gupta  

## Description
This project deploys a Flask-based web application with a MySQL database backend on a single-node Kubernetes cluster using Kind, hosted on an Amazon Linux 2 EC2 instance. The setup leverages Terraform for infrastructure provisioning, Docker for containerization, and AWS ECR for image storage. The Flask app supports CRUD operations on an `employees` database and dynamically changes its UI color based on the `APP_COLOR` environment variable (e.g., pink for version 2, blue for local testing).

**Note:** This project was tested on an Amazon Linux 2 EC2 instance. Ensure you have the necessary tools installed and AWS credentials configured before proceeding. Refer to the error report section for common issues and their resolutions.

---

## Prerequisites
- `kind` and `kubectl` installed on the EC2 instance.
- AWS CLI installed and configured with necessary permissions (`ecr:CreateRepository`, `ecr:PutLifecyclePolicy`, etc.).
- Docker installed for building and pushing images.
- Terraform installed for infrastructure provisioning.
- SSH key pair for accessing the EC2 instance.

---

## Infrastructure Deployment

1. **Clone the Repository:**
   ```sh
   git clone https://github.com/Arpit-commits/Arpit-CLO835-Assignment2.git
