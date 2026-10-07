# VELORA — Dockerized Website

This is a website I built while learning Docker and cloud engineering.

I created the website with HTML and CSS, then used Nginx to serve it inside a Docker container.

The main goal of this project was to understand how a website can go from my local computer to Docker Hub and then be deployed on AWS EC2.

## Technologies I Used

* HTML
* CSS
* Nginx
* Docker
* Docker Compose
* Git
* GitHub
* Docker Hub
* Ubuntu Linux
* AWS EC2

## Project Structure

```text id="kz2l0w"
docker-site/
├── Dockerfile
├── compose.yaml
├── index.html
├── README.md
└── .gitignore
```

## Docker

I created a Dockerfile using Nginx:

```dockerfile id="zsp6yt"
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
```

The Dockerfile uses Nginx as the base image and copies my `index.html` into the Nginx web directory.

I built the image with:

```bash id="c3w5q9"
docker build -t my-docker-site .
```

## Docker Compose

I also used Docker Compose to run the website.

My `compose.yaml` mapped:

```text id="9g6q4k"
8083:80
```

I started it with:

```bash id="p0j4c5"
docker compose up -d
```

Then I checked it with:

```bash id="b4v3f1"
docker compose ps
```

I accessed the website locally at:

```text id="8s3v9c"
http://localhost:8083
```

Here, `8083` is the port on my computer and `80` is the port inside the Docker container.

## Docker Hub

After building and testing the Docker image, I pushed it to Docker Hub.

My Docker Hub image is:

```text id="f3r6y1"
feranmi2468/my-docker-site:latest
```

I used:

```bash id="j4k7m2"
docker login
```

Then tagged the image:

```bash id="a8d2x5"
docker tag my-docker-site:latest feranmi2468/my-docker-site:latest
```

And pushed it:

```bash id="q7m1s8"
docker push feranmi2468/my-docker-site:latest
```

I also tested pulling the image back from Docker Hub:

```bash id="n6c2v4"
docker pull feranmi2468/my-docker-site:latest
```

## Testing the Docker Hub Image

I ran the Docker Hub image locally using port `8084`:

```bash id="r5t8k3"
docker run -d --name velora-test -p 8084:80 feranmi2468/my-docker-site:latest
```

Then I opened:

```text id="w2h7p9"
http://localhost:8084
```

This helped me confirm that the image I pushed to Docker Hub could be pulled and run successfully.

The reason I used `8084` here instead of `8083` was simply to avoid using the same host port as my Docker Compose container.

## AWS EC2 Deployment

After testing the Docker Hub image locally, I deployed the same image to an Ubuntu EC2 instance.

First, I installed Docker on the EC2 server:

```bash id="m9k4x2"
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable --now docker
```

Then I pulled my Docker Hub image:

```bash id="z6p3n8"
sudo docker pull feranmi2468/my-docker-site:latest
```

Finally, I ran the container:

```bash id="t4v7c1"
sudo docker run -d --name velora -p 80:80 feranmi2468/my-docker-site:latest
```

I checked that the container was running with:

```bash id="h8q2m6"
sudo docker ps
```

The EC2 deployment used `80:80`.

This means:

```text id="d1f5s7"
EC2 port 80 → Docker container port 80
```

I also configured the EC2 security group to allow HTTP traffic on port 80 so the website could be accessed through the EC2 public IP.

## My Docker Workflow

This project helped me understand the complete workflow:

```text id="v8k3p2"
Build website
     ↓
Create Dockerfile
     ↓
Build Docker image
     ↓
Run container locally
     ↓
Use Docker Compose
     ↓
Push image to Docker Hub
     ↓
Pull image from Docker Hub
     ↓
Deploy image to AWS EC2
     ↓
Run container on EC2
```

## What I Learned

Through this project, I learned how to:

* Build a Docker image
* Create and run containers
* Use Nginx with Docker
* Use Docker Compose
* Understand Docker port mapping
* Push images to Docker Hub
* Pull images from Docker Hub
* Use Git and GitHub
* Work with Ubuntu Linux
* Connect to an EC2 server using SSH
* Install Docker on EC2
* Deploy a Docker image to AWS EC2
* Allow HTTP traffic through an EC2 security group

## Next Step

This project has helped me understand Docker and how containers can be deployed to AWS.

My next step in my cloud engineering journey is Terraform and Infrastructure as Code (IaC). 🚀

## Author

 Adenuga Oluwaferanmi

Cloud Engineering Journey
