# Microservices Containerization Assessment

## Objective

Containerize a Node.js microservices application using Docker and Docker Compose.

## Project Structure

```text
submission/
├── user-service/
│   └── Dockerfile
├── product-service/
│   └── Dockerfile
├── gateway-service/
│   └── Dockerfile
├── docker-compose.yml
└── README.md
```

## Services

| Service         | Port |
| --------------- | ---- |
| User Service    | 3000 |
| Product Service | 3001 |
| Gateway Service | 3003 |

---

## Prerequisites

Before running the application, ensure the following are installed:

* Docker Desktop
* Docker Compose
* Git (optional)

Verify installation:

```bash
docker --version
docker compose version
```

---

## Setup Instructions

### 1. Clone the Repository

```bash
git clone <repository-url>
cd submission
```

### 2. Build and Start Containers

```bash
docker compose up --build
```

Or, if using an older Docker Compose version:

```bash
docker-compose up --build
```

---

## Verify Running Containers

Check that all containers are running:

```bash
docker ps
```

Expected containers:

* user-service
* product-service
* gateway-service

---

## Access the Services

Open a browser and verify the services:

| Service         | URL                   |
| --------------- | --------------------- |
| User Service    | http://localhost:3000 |
| Product Service | http://localhost:3001 |
| Gateway Service | http://localhost:3003 |

---

## API Testing

Using curl:

### User Service

```bash
curl http://localhost:3000
```

### Product Service

```bash
curl http://localhost:3001
```

### Gateway Service

```bash
curl http://localhost:3003
```

Expected responses should indicate that each service is running successfully.

---

## Docker Compose Configuration

The application uses Docker Compose to:

* Build all services
* Run containers simultaneously
* Create a shared network for communication
* Manage service dependencies

Start services:

```bash
docker compose up --build
```

Stop services:

```bash
docker compose down
```

---

## Troubleshooting

### Port Already in Use

Check which process is using the port:

```bash
netstat -ano
```

Or on Linux/Ubuntu:

```bash
sudo lsof -i :3000
```

Update port mappings in `docker-compose.yml` if required.

---

### Container Exits Immediately

Check logs:

```bash
docker logs user-service
docker logs product-service
docker logs gateway-service
```

---

### Rebuild Containers

If changes are made:

```bash
docker compose up --build
```

---

## Screenshots Included

The following screenshots are attached with the submission:

1. Docker Compose build and startup output
2. Docker containers running (`docker ps`)
3. User Service response in browser
4. Product Service response in browser
5. Gateway Service response in browser

---

## Architecture

```text
                 +------------------+
                 |  Gateway Service |
                 |      :3003       |
                 +---------+--------+
                           |
          ---------------------------------
          |                               |
+---------v--------+          +----------v---------+
|   User Service   |          |  Product Service   |
|      :3000       |          |       :3001        |
+------------------+          +--------------------+

         Docker Compose Shared Network
```

---

## Author

Sonali Patil

Microservices Containerization Assessment Submission
