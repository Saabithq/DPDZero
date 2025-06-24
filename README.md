# 🧩 Multi-Service Reverse Proxy System

## 📝 Overview
This project demonstrates a production-style **microservices** setup using **Docker Compose**. It includes:

- **Nginx reverse proxy** (in a container)
- **Service 1**: Golang API (on port `8001`)
- **Service 2**: Python Flask API (on port `8002`)
- All services are accessible via a single port: `localhost:8080` with **path-based routing**

---

## 📁 Project Structure

```
.
├── docker-compose.yml
├── nginx/
│   ├── Dockerfile
│   └── nginx.conf
├── service_1/
│   ├── Dockerfile
│   ├── main.go
│   └── README.md
├── service_2/
│   ├── Dockerfile
│   ├── app.py
│   ├── pyproject.toml
│   ├── uv.lock
│   └── README.md
└── readme.md
```

---

## ⚙️ Setup Instructions

### 1. Clone the repository:
```bash
git clone https://github.com/<your-username>/DPDZero.git
cd DPDZero
```

### 2. Build and run all services:
```bash
docker-compose up --build
```

> If using older Docker Compose syntax:
```bash
docker compose up --build
```

---

## 🌐 Access the Services

Use your browser or `curl`:

- [http://localhost:8080/service1/ping](http://localhost:8080/service1/ping)
- [http://localhost:8080/service1/hello](http://localhost:8080/service1/hello)
- [http://localhost:8080/service2/ping](http://localhost:8080/service2/ping)
- [http://localhost:8080/service2/hello](http://localhost:8080/service2/hello)

> 💡 If using a remote server, replace `localhost` with your server's IP.

---

## 🛑 Stopping the System

```bash
docker-compose down
```

---

## 🔀 How Routing Works

Nginx (on port `8080`) routes based on path:

- `/service1/*` → Go service (`8001`)
- `/service2/*` → Python service (`8002`)

Nginx acts as a **reverse proxy**, forwarding requests to the appropriate backend.

---

## ❤️ Health Checks

Both services expose a `/ping` endpoint.

**Docker Compose** uses healthchecks to verify service status.

Example responses:
- Go Service → `{ "status": "ok", "service": "1" }`
- Python Service → `{ "status": "ok", "service": "2" }`

---

## 📊 Logging

- Nginx logs all incoming requests with timestamp and path
- Logs are stored at `/var/log/nginx/access.log` in the Nginx container

To view logs:
```bash
docker-compose logs nginx
```

or
```bash
docker logs <nginx_container_id>
```

---

## 🐳 Docker Compose Details

- **nginx**: Custom image from `nginx/`, uses `nginx.conf` for routing and logging.
- **service1**: Go app in `service_1/`, exposed on port `8001`.
- **service2**: Flask app in `service_2/`, exposed on port `8002`.
- All services use a custom Docker network.

---

## 🎁 Bonus Features

- Built-in **healthchecks**
- Clean, modular setup
- Centralized **logging** via Nginx

---

## 🛠️ Troubleshooting

| Issue                  | Solution                                   |
|------------------------|--------------------------------------------|
| Nginx won’t start      | Check `nginx.conf` for syntax errors       |
| Services not accessible| Ensure Docker is running and port 8080 is open |
| Permission errors      | Use `sudo` with Docker commands            |

---

## 🚀 Submission

- Push your project to **GitHub** or **GitLab**
- Include this `README.md` in the root directory
- Submit your repository link as instructed

---

## 👨‍💻 Author Notes

This project is for **learning and demonstration** only.

> For production:
- Use a production-ready WSGI server (e.g., Gunicorn) for Python.
- Apply **security best practices** for Nginx and Docker.

---
