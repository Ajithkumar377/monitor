
# 🚀 DevOps Monitoring Project using EC2, GitHub, Jenkins, Docker, Kubernetes, Ansible, Prometheus, Grafana

This is a complete DevOps CI/CD pipeline project to deploy and monitor a Python Flask application using the following tools:

- **AWS EC2** – Hosting the entire environment
- **Git & GitHub** – Version control and source code hosting
- **Jenkins** – Continuous Integration and Continuous Deployment
- **Docker** – Containerizing the application
- **Kubernetes (Minikube)** – Container orchestration
- **Ansible** – Automated provisioning of Jenkins, Docker, and Minikube
- **Prometheus** – Monitoring metrics
- **Grafana** – Visualizing metrics

---

## 📁 Project Structure


devops-monitoring-project/
├── app/                    # Flask application
│   ├── app.py
│   ├── Dockerfile
│   └── requirements.txt
├── jenkins/                # Jenkins pipeline script
│   └── Jenkinsfile
├── k8s/                    # Kubernetes deployment + service files
│   ├── deployment.yaml
│   └── service.yaml
├── ansible/                # Ansible playbook to set up Jenkins, Docker, Minikube
│   └── setup.yml
├── prometheus/             # Prometheus & Grafana configuration
│   ├── prometheus.yml
│   ├── config-map.yaml
│   ├── prometheus-deployment.yaml
│   ├── prometheus-service.yaml
│   ├── grafana-deployment.yaml
│   └── grafana-service.yaml
└── README.md


---

## ✅ How to Run This Project

### 1. Launch an EC2 Instance
- Use Amazon Linux 2
- Type: t2.medium or higher
- Connect using:
```bash
ssh -i "your-key.pem" ec2-user@<your-ec2-ip>
````

---

### 2. Clone the Repository on EC2

```bash
git clone https://github.com/your-username/devops-monitoring-project.git
cd devops-monitoring-project
```

---

### 3. Run Ansible Playbook to Install Jenkins, Docker, Minikube

```bash
sudo yum install -y ansible
ansible-playbook ansible/setup.yml -i "localhost,"
```

---

### 4. Build Docker Image for Flask App

```bash
cd app/
docker build -t flask-app .
```

---

### 5. Start Minikube and Deploy App on Kubernetes

```bash
minikube start
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

---

### 6. Access Flask App

```bash
minikube service flask-service --url
```

---

### 7. Setup Jenkins Pipeline

* Open Jenkins in browser: `http://<EC2-IP>:8080`
* Create a pipeline job and use `jenkins/Jenkinsfile`
* Add your GitHub repo URL

---

### 8. Deploy Prometheus & Grafana

```bash
cd prometheus/
kubectl apply -f config-map.yaml
kubectl apply -f prometheus-deployment.yaml
kubectl apply -f prometheus-service.yaml
kubectl apply -f grafana-deployment.yaml
kubectl apply -f grafana-service.yaml
```

---

### 9. Access Monitoring Dashboards

#### Prometheus:

```bash
minikube service prometheus-service --url
```

#### Grafana:

```bash
minikube service grafana-service --url
```

Then login:

* Username: `admin`
* Password: `admin`

Add Prometheus as a data source in Grafana:

```
http://prometheus-service.default.svc.cluster.local:9090
```

---

## 📊 Metrics You Can Visualize

* Pod uptime
* CPU & memory usage
* Number of app requests
* Node performance metrics

---

## 🧠 Technologies Used

| Tool         | Purpose                                |
| ------------ | -------------------------------------- |
| AWS EC2      | Cloud VM host for the whole stack      |
| Git + GitHub | Version control & source hosting       |
| Jenkins      | CI/CD pipeline automation              |
| Docker       | Containerization                       |
| Kubernetes   | Container orchestration (via Minikube) |
| Ansible      | Automated tool installation/setup      |
| Prometheus   | Collects metrics                       |
| Grafana      | Visualizes metrics in dashboards       |

---

## 👨‍💻 Author

**Ajith Kumar**
DevOps Cloud Engineer –  AWS | CI/CD | Docker | Kubernetes | Monitoring 

---


