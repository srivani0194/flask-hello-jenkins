
# Flask Hello World – Docker & Jenkins Pipeline

This repository contains a simple Python Flask “Hello World” application, containerized using Docker and built using a Jenkins Declarative Pipeline.
The pipeline runs automated tests, builds a Docker image, and performs a security scan on the image.

## Application Overview
```text
Framework: Flask
Language: Python 3
Web Server: Gunicorn
Testing: Pytest
Containerization: Docker
CI/CD: Jenkins (Declarative Pipeline)
Security Scanning: Trivy
```

## Project Structure
```text
.
├── app.py
├── test_app.py
├── requirements.txt
├── requirements-dev.txt
├── Dockerfile
├── .dockerignore
├── Jenkinsfile
└── README.md
```
## Flask Application

Endpoints exposed by the application:

```text
GET /       -> Returns Hello, World!
GET /health -> Health check endpoint
```


## Run Locally
Create a virtual environment

```text
python3 -m venv .venv
source .venv/bin/activate
```

## Install dependencies
``` pip install -r requirements.txt -r requirements-dev.txt ```

## Run the application
``` python app.py ```


## Access:
```http://localhost:5000```

## Run Tests
```pytest -q```


## Expected:
2 passed

## Docker
Build image
``` docker build -t flask-hello:local . ```

## Run container
``` docker run --rm -p 8080:5000 flask-hello:local ```


## Access:

``` http://localhost:8080 ```

## Jenkins Pipeline

The Jenkins Declarative Pipeline performs:
```text
Checkout source code
Run unit tests
Build Docker image
Security scan using Trivy
The pipeline definition is in Jenkinsfile.
Security Scanning
Image scanned using Trivy

Build fails on HIGH or CRITICAL vulnerabilities
```

