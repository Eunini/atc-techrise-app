# ATC TechRise App – Docker & EC2 Deployment

## 📦 Project Overview
This is a simple Flask-based application that displays a welcome message. It was containerized using Docker, pushed to Docker Hub, and deployed to an AWS EC2 instance for public access via port 5000.

---

## ✅ Requirements
- Docker
- Docker Hub account
- AWS account
- EC2 instance (Amazon Linux 2 or Ubuntu)

---

## 🔧 Local Setup & Dockerization

### 1. Clone the Repository
```bash
git clone https://github.com/YOUR-USERNAME/atc-techrise-app.git
cd atc-techrise-app
```

### 2. Dockerize the Flask App
Ensure you have a valid `Dockerfile`:
```Dockerfile
# Dockerfile
FROM python:3.8
WORKDIR /app
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

Then build the Docker image:
```bash
docker build -t atc-techrise-app .
```

### 3. Run Locally with Docker
```bash
docker run -d -p 5000:5000 atc-techrise-app
```
Check on your browser: `http://localhost:5000`

---

## 🐳 Push Docker Image to Docker Hub

### 1. Log in to Docker Hub
```bash
docker login
```
> ✅ Make sure you're logged in with the correct Docker Hub username.

### 2. Tag the Docker Image
```bash
docker tag atc-techrise-app yourdockerhubusername/atc-techrise-app
```

### 3. Push to Docker Hub
```bash
docker push yourdockerhubusername/atc-techrise-app
```
If you get an error like `unauthorized: access token has insufficient scopes`, make sure you:
- Are logged in properly
- Are using your correct Docker Hub username
- Have permission to push to that repo

---

## 🚀 Deploy on AWS EC2

### 1. Launch an EC2 Instance
- OS: Amazon Linux 2 or Ubuntu
- Allow inbound HTTP on **port 5000** (add it in the security group)

### 2. SSH into EC2
```bash
ssh -i your-key.pem ec2-user@your-ec2-public-ip
```

### 3. Install Docker (Amazon Linux)
```bash
sudo yum update -y
sudo yum install docker -y
sudo service docker start
sudo usermod -aG docker ec2-user
exit
```
Then **SSH back in** to apply the group change.

### 4. Pull and Run Docker Image
```bash
docker pull inioluwa16/atc-techrise-app
docker run -d -p 5000:5000 inioluwa16/atc-techrise-app
```

### 5. Visit in Browser
Open: `http://your-ec2-public-ip:5000`

---

## 📸 Screenshots
- Local deployment: `http://localhost:5000`
- EC2 deployment: `http://<EC2-IP>:5000`

---

## 🧠 Challenges Faced
- Docker Hub authentication issues (`unauthorized: access token has insufficient scopes`)
- EC2 port 5000 not accessible → fixed by updating inbound rules in security group
- Group change for Docker permissions required SSH logout/login

---

## 🔗 Links
- GitHub Repo: https://github.com/Eunini/atc-techrise-app.git
- Docker Hub Image: [https://hub.docker.com/r/inioluwa16/atc-techrise-app](https://hub.docker.com/r/inioluwa16/atc-techrise-app)

---

## 📄 Copyright
Inioluwa Atanda

---

## 🙌 Acknowledgments
Thanks to the ATC TechRise team for the challenge!

---

