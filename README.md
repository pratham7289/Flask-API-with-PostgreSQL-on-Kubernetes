
# Flask API with PostgreSQL on Kubernetes

A production-ready template for deploying a Flask API with a PostgreSQL backend on Kubernetes. This project demonstrates best practices for containerization, orchestration, and deployment of a web application with a database backend.

## 🚀 Features

- Flask REST API with PostgreSQL database
- Containerized applications using Docker
- Kubernetes deployment configurations
- Database initialization and migration scripts
- Production-ready configuration
- Scalable architecture

## Please refer to the documents and YAML files uploaded above for detailed deployment and configuration instructions.

## 📋 Prerequisites

- Docker (version 20.10.x or higher)
- Kubernetes cluster (version 1.20.x or higher)
- kubectl CLI tool
- Python 3.8+
- RHEL/CentOS 7/8 (for host system)

## 🛠️ Installation

### 1. Set Up Docker on RHEL

```bash
# Update system
sudo yum update -y

# Install required packages
sudo yum install -y yum-utils device-mapper-persistent-data lvm2

# Install Docker
sudo yum install -y docker

# Start and enable Docker
sudo systemctl start docker && sudo systemctl enable docker

# Add user to Docker group (optional but recommended)
sudo usermod -aG docker $USER
```

### 2. Set Up Kubernetes Components

```bash
# Install kubeadm, kubelet, and kubectl
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

# Start and enable Kubernetes services
sudo systemctl start kubelet && sudo systemctl enable kubelet

# Install Flannel CNI plugin (on master node)
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

## 📦 Project Structure

```plaintext
├── flask-api/
│   ├── Dockerfile
│   ├── requirements.txt
│   └── app.py
├── postgres-db/
│   ├── init.sql
│   └── docker-compose.yml
├── k8s/
│   ├── flask-deployment.yaml
│   ├── flask-service.yaml
│   ├── postgres-deployment.yaml
│   └── postgres-service.yaml
└── README.md
```

## 🚀 Deployment

### 1. Deploy PostgreSQL

```bash
# Create PostgreSQL deployment and service
kubectl apply -f k8s/postgres-deployment.yaml
kubectl apply -f k8s/postgres-service.yaml
```

### 2. Deploy Flask API

```bash
# Create Flask API deployment and service
kubectl apply -f k8s/flask-deployment.yaml
kubectl apply -f k8s/flask-service.yaml
```

### 3. Verify Deployment

```bash
# Check running pods
kubectl get pods

# Check services
kubectl get svc
```

## 🔍 Testing the API

### Using NodePort:

```bash
curl http://<worker-node-ip>:<node-port>/users
```

**Example response:**

```json
[
  {"student_id": 1, "student_name": "Student 1"},
  {"student_id": 2, "student_name": "Student 2"}
]
```

## 📊 Monitoring

Monitor your deployment using:

```bash
# Check pod status
kubectl get pods -w

# View pod logs
kubectl logs <pod-name>

# Describe service
kubectl describe svc flask-api-service
```

## 🔧 Configuration

The application can be configured using the following environment variables:

| Variable        | Description          | Default     |
|-----------------|----------------------|-------------|
| `DB_HOST`       | PostgreSQL host      | `postgres`  |
| `DB_PORT`       | PostgreSQL port      | `5432`      |
| `DB_NAME`       | Database name        | `students`  |
| `DB_USER`       | Database user        | `postgres`  |
| `DB_PASSWORD`   | Database password    | `postgres`  |

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request
