# 🐳 Docker: A Complete Guide

**Docker** is a platform and tool that allows developers to automate the deployment of applications inside **lightweight, portable containers**. Containers bundle an application along with its dependencies (libraries, configuration files, etc.) into a single package that can run consistently across various environments (local, staging, production, etc.).

---

## 🔑 Key Concepts in Docker

### 1. Containers
- Containers are **isolated environments** where applications run.
- They are lightweight, fast, and share the host system's kernel while running their own processes.
- Unlike virtual machines, containers **do not require a full OS**, making them more efficient.

### 2. Images
- A **Docker image** is a **read-only template** containing the application's code, libraries, and dependencies.
- Images are used to create containers.
- Images are built from **Dockerfiles**.

### 3. Dockerfile
- A **Dockerfile** is a text file containing instructions to build a Docker image.
- Example Dockerfile:

```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy current directory contents into the container at /app
COPY . /app

# Install packages from requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Expose port 80
EXPOSE 80

# Environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
