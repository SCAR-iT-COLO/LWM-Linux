# Docker

## 1. Introduction to Docker
Docker is a platform for developing, shipping, and running applications in containers. Containers allow developers to package an application with all its dependencies and configurations, ensuring it works consistently across different environments.

## 2. Key Concepts
- Container: A lightweight, standalone, executable package that includes everything needed to run an application.
- Image: A read-only template used to create containers.
- Dockerfile: A text file containing instructions to build a Docker image.
- Docker Hub: A cloud-based registry for sharing and storing Docker images.
- Docker Compose: A tool for defining and running multi-container Docker applications.

## 3. Installing Docker
- For Windows and Mac: Download Docker Desktop from the official website.
- For Linux: Use your distribution's package manager or follow the official installation guide.

## 4. Basic Docker Commands
- `docker run`: Create and start a container
- `docker pull`: Download an image from a registry
- `docker build`: Build an image from a Dockerfile
- `docker ps`: List running containers
- `docker images`: List available images
- `docker stop`: Stop a running container
- `docker rm`: Remove a container
- `docker rmi`: Remove an image

## 5. Creating a Dockerfile
A Dockerfile typically includes:
- Base image (`FROM`)
- Working directory (`WORKDIR`)
- Copying files (`COPY`)
- Running commands (`RUN`)
- Exposing ports (`EXPOSE`)
- Setting environment variables (`ENV`)
- Specifying the command to run (`CMD`)

Example Dockerfile:
```dockerfile
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```

## 6. Building and Running Images
- Build: `docker build -t myapp:1.0 .`
- Run: `docker run -p 3000:3000 myapp:1.0`

## 7. Docker Compose
Docker Compose allows you to define multi-container applications in a YAML file.

Example docker-compose.yml:
```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "3000:3000"
  db:
    image: mongo:latest
    volumes:
      - ./data:/data/db
```

Run with: `docker-compose up`

## 8. Docker Networking
- Bridge: Default network driver
- Host: Removes network isolation between container and host
- Overlay: Connects multiple Docker daemons
- Macvlan: Assigns a MAC address to a container

## 9. Docker Volumes
Volumes are used for persistent data storage:
- Create: `docker volume create myvolume`
- Use: `docker run -v myvolume:/app/data myapp:1.0`

## 10. Docker Security Best Practices
- Use official base images
- Scan images for vulnerabilities
- Limit container resources
- Use non-root users inside containers
- Implement network segmentation

## 11. Docker in Production
- Orchestration tools: Kubernetes, Docker Swarm
- Monitoring: Prometheus, Grafana
- Logging: ELK stack (Elasticsearch, Logstash, Kibana)

## 12. Advanced Topics
- Multi-stage builds
- Docker content trust
- Docker registry
- CI/CD integration
