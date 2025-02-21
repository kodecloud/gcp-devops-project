
### **GCP DevOps Project - CI/CD Pipeline**
This repository documents the CI/CD pipeline steps for deploying a **Flask application** using **GitHub, Docker, GCP, GKE, and Cloud Build**.

## **🚀 Sprint-01: Create GitHub Repository & Flask Application**  
### **1️⃣ Create a GitHub Repository**
- Visit [GitHub](https://github.com/) and log in with:  
  - **Username**: `sreeharigaddam`  
  - **Email**: `gsreeharigaddam@gmail.com`
- Create a **new repository**: [kodecloud/gcp-devops-project](https://github.com/kodecloud/gcp-devops-project)

### **2️⃣ Clone the Repository**
```bash
git clone https://github.com/kodecloud/gcp-devops-project.git
cd /d/gsreehari/Learnings/GCPDevOpsProject_KodeCloud/gcp-devops-project
code .  # Opens VS Code
```

### **3️⃣ Enable Branch Protection**  
- Configure branch protection to **allow merges only via Pull Requests** with **reviewers (optional).**

### **4️⃣ Create a Feature Branch & Push Changes**
```bash
git checkout -b "feature/task-2"
create the file: README.md, add somecontent
# Modify any file
git status   # Shows modified files
git commit -m "Updated README.md"
git push origin feature/task-2
```
- **Create & Merge** a Pull Request from GitHub UI.

### **5️⃣ Create the Flask Application**
- Run the Flask application **locally**:
```bash
create flask application with app.py and requirements.txt 
flask run
```
- **Verify from browser**:  
  [http://127.0.0.1:5000/](http://127.0.0.1:5000/)

### **6️⃣ Install Docker & Run Flask App in a Container**
```bash
# Install & Start Docker Desktop
docker build --tag python-docker-image .   # Build Docker Image
docker images  # Verify Image
docker run -p 5000:5000 python-docker-image   # Run Flask App
```
- **Access Flask App** from browser:  
  [http://127.0.0.1:5000/](http://127.0.0.1:5000/)

---

## **🚀 Sprint-02: Setup GCP Account & Create GKE Cluster**  
### **1️⃣ Create a GCP Account**
- Sign up at [Google Cloud Console](https://console.cloud.google.com/)
- Create a **GKE Standard Cluster**:
  - **Cluster Name**: `cluster-1`
  - **Type**: **Standard Cluster**
  - **Node Type**: `e2-medium`
  - **Regional** Deployment  

### **2️⃣ Connect to GKE Cluster**
```bash
# Connect to GKE Cluster
gcloud container clusters get-credentials devops-gke-prod --zone <your-zone> --project <your-project>
```

### **3️⃣ Verify Cluster Connectivity**
```bash
kubectl get nodes
```

---

## **🚀 Sprint-04: Setup Cloud Build & Trigger**
### **1️⃣ Create `cloudbuild.yaml`**
- This file defines **Cloud Build pipeline** for **automated deployments**.
```yaml
steps:
  - name: 'gcr.io/cloud-builders/docker'
    args: ['build', '-t', 'gcr.io/$PROJECT_ID/python-docker-image', '.']
  - name: 'gcr.io/cloud-builders/docker'
    args: ['push', 'gcr.io/$PROJECT_ID/python-docker-image']
```

### **2️⃣ Configure Cloud Build Trigger**
- **Connect Cloud Build with GitHub**:
  - Automatically triggers **Cloud Build** for each **commit**.

---

## **🚀 Sprint-05: Create Namespace & Deploy to GKE**
### **1️⃣ Create Kubernetes Namespace**
```bash
kubectl create namespace gcp-devops-prod
```

### **2️⃣ Create `gke.yaml` for Deployment**
- Define **Deployment & Service**.
- add gke.yaml with deployment

### **3️⃣ Deploy the Application to GKE, though Cloud run and verify the pods**
```bash

# kubectl apply -f gke.yaml
kubectl get pods -n gcp-devops-prod
kubectl get svc -n gcp-devops-prod
```

---

## **🚀 Sprint-06: Update Code & Configure Load Balancer**
### **1️⃣ Modify `gke.yaml` to Include LoadBalancer Service**
- Ensure **Service type** is set to **LoadBalancer**.

### **2️⃣ Redeploy & Verify Load Balancer Endpoint**
```bash
#kubectl apply -f gke.yaml
kubectl get svc -n gcp-devops-prod
```
- Copy **External IP** and access the app in the browser.

---

## **🚀 Sprint-07: Setup Dev Branch
### **1️⃣ Create a `dev` Branch**
```bash
git checkout -b dev
git push origin dev
```

### **2️⃣ Setup Cloud Build Trigger for `dev`**
- Configure Cloud Build to **deploy changes** in **Dev Cluster** upon commits to the `dev` branch.

---

## **🎯 Summary of CI/CD Pipeline**
✔ **Sprint-01**: Setup **GitHub, Flask, Docker**  
✔ **Sprint-02**: Setup **GCP, GKE Cluster**  
✔ **Sprint-04**: Configure **Cloud Build & Triggers**  
✔ **Sprint-05**: Deploy **Flask App to GKE**  
✔ **Sprint-06**: Setup **Load Balancer** for external access  
✔ **Sprint-07**: Automate **Cloud Build for Dev Cluster**  

---

## **📌 Next Steps**
🚀 **Enhancements:**  
- **Integrate Cloud SQL** for database  
- **Enable Auto-scaling in GKE**  
- **Implement CI/CD with ArgoCD**  

### **Happy DevOps! 🎉**  
Let me know if you need any modifications. 🚀
