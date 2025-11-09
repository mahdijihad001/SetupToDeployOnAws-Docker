# Steps to deploy on aws(Docker)

## Step 1: Build Docker Image Locally

```bash
docker build -t dockerhub-username/your-image-name:latest .
```

## Step 2: Login to Docker Hub

```bash
docker login
```

## Step 3: Tag the Image for Docker Hub

```bash
docker tag your-image-name dockerhub-username/your-image-name:latest
```

## Step 4: Push Image to Docker Hub

```bash
docker push dockerhub-username/your-image-name:latest
```

## Step 5: Connect to AWS EC2

```bash
ssh -i "your-key.pem" ubuntu@your-ec2-public-ip
```

## Step 6: Install Docker on EC2 (if not installed)

```bash
sudo apt-get update
sudo apt-get install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
```

## Step 7: Pull Image from Docker Hub on EC2

```bash
docker pull dockerhub-username/your-image-name:latest
```

## Step 8: Run the Container

```bash
docker run -d -p 80:80 --name myapp dockerhub-username/your-image-name:latest
```

## Step 9: Update After Code Changes

Whenever you change code:

1. Rebuild image locally
2. Push to Docker Hub
3. On EC2, run the following commands:

```bash
./setup.sh
docker pull dockerhub-username/your-image-name:latest
docker stop myapp|True
docker rm myapp|True
docker run -d -p 80:80 --name myapp dockerhub-username/your-image-name:latest
```

