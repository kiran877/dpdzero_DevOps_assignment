# 🚀 DevOps Assignment: Nginx Reverse Proxy + Docker

A complete Docker Compose setup with Nginx reverse proxy routing requests to two backend services (Golang and Python Flask).

## 🏗️ Architecture

```
Internet → Nginx (Port 8081) → Service 1 (Golang:8001) or Service 2 (Flask:8002)
```

- **Nginx**: Reverse proxy with custom routing and logging
- **Service 1**: Golang HTTP service 
- **Service 2**: Python Flask service
- **Docker Compose**: Orchestrates all services with health checks

## 📁 Project Structure

```
.
├── docker-compose.yml
├── nginx/
│   ├── Dockerfile
│   └── default.conf
├── service1/
│   ├── Dockerfile
│   ├── main.go
│
├── service2/
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
└── README.md
```

## 🚀 Quick Start

### Prerequisites
- Docker
- Docker Compose

### Run the System

```bash
docker-compose up --build
```

The system will be available at `http://localhost:8081`

### Stop the System

```bash
docker-compose down
```

## 🔗 API Endpoints

### Through Nginx Reverse Proxy (Port 8080)

| Endpoint | Service | Description |
|----------|---------|-------------|
| `http://localhost:8081/` | Nginx | Service information |
| `http://localhost:8081/health` | Nginx | Nginx health check |
| `http://localhost:8081/service1/ping` | Service 1 | Health check |
| `http://localhost:8081/service1/hello` | Service 1 | Greeting message |
| `http://localhost:8081/service2/ping` | Service 2 | Health check |
| `http://localhost:8081/service2/hello` | Service 2 | Greeting message |

### Direct Service Access (for testing)

- Service 1: `http://localhost:8001`
- Service 2: `http://localhost:8002`

## 📊 Testing the Setup

### 1. Test Nginx Root
```bash
curl http://localhost:8080/
```

### 2. Test Service 1 (Golang)
```bash
curl http://localhost:8080/service1/ping
curl http://localhost:8080/service1/hello
```

### 3. Test Service 2 (Flask)
```bash
curl http://localhost:8080/service2/ping
curl http://localhost:8080/service2/hello
```

## 📋 Features

### ✅ Requirements Met
- Two Dockerized backend services on different ports
- Nginx reverse proxy with path-based routing
-  Single port access (8081)
-  Docker Compose orchestration
-  JSON responses with service identification
-  Custom logging with timestamps and paths
-  One-command startup: `docker-compose up --build`

### 🎯 Bonus Features
-  Health checks for both services
-  Custom Nginx log format with timestamps
-  Proper error handling and timeouts
-  Service identification in responses
-  Bridge networking (no host networking)

## 🔍 Monitoring

### View Logs
```bash
# All services
docker-compose logs -f

# Specific service
docker-compose logs -f nginx
docker-compose logs -f service1
docker-compose logs -f service2
```

### Health Check Status
```bash
docker-compose ps
```

### Nginx Access Logs
Nginx logs are mounted to `./nginx/logs/` directory for easy access.

## 🛠️ Services Details

### Service 1 - Golang
- **Port**: 8001 (internal), accessible via `/service1/*` through Nginx
- **Endpoints**: `/ping`, `/hello`
- **Features**: JSON responses, logging, health checks

### Service 2 - Python Flask
- **Port**: 8002 (internal), accessible via `/service2/*` through Nginx  
- **Endpoints**: `/ping`, `/hello`
- **Features**: JSON responses, logging, health checks

### Nginx Reverse Proxy
- **Port**: 8080 (public)
- **Features**: 
  - Path-based routing (`/service1/*` → Service 1, `/service2/*` → Service 2)
  - Custom logging with timestamps
  - Health check endpoint (`/health`)
  - Proper proxy headers
  - Timeout configuration

Checkout my Projects:https://github.com/kiran-devops-Projects/