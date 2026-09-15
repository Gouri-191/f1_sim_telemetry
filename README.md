# Motorsport Telemetry & Operations Platform

A high-performance, distributed, real-time telemetry processing and simulation platform for motorsport engineering. This system simulates multi-car racing environments, streams live telemetry via MQTT, processes physics and vehicle dynamics, and visualizes real-time metrics through a responsive, glassmorphic React dashboard.

## 🚀 Features
- **Real-Time Simulation engine:** Python-based multi-car physics engine running at 10Hz, modeling fuel consumption, tyre wear, brake fade, and dynamic driver styles across world-class circuits (Silverstone, Spa, Monza, Monaco).
- **High-Throughput Messaging:** Eclipse Mosquitto MQTT broker for low-latency pub/sub streaming between the simulator, processor, and API.
- **Robust Telemetry Pipeline:** Python processor subscribing to MQTT streams and persisting structured time-series data and lap records to PostgreSQL.
- **Modern REST API & SignalR:** .NET 10 Web API providing HTTP endpoints for lap history and real-time WebSocket (SignalR) streaming to the frontend. Includes bidirectional control loops for pausing, resuming, or stopping the simulation and injecting mechanical faults.
- **Advanced Frontend Dashboard:** A responsive React application utilizing Vite, Recharts, and a custom CSS design system. Features live telemetry graphs, lap delta comparisons, circular vector gauges, track map tracking, and engineering insights.
- **Observability:** Prometheus and Grafana integration for platform monitoring and metrics visualization.

## 🏗️ Architecture

The platform is fully containerized utilizing Docker Compose, consisting of six primary services:

1. **`mqtt`**: Eclipse Mosquitto message broker (Ports 1883, 9001).
2. **`postgres`**: Relational database for persistent telemetry and lap history storage (Port 5432).
3. **`simulator`**: Python application generating dynamic vehicle telemetry and subscribing to control loops.
4. **`processor`**: Python worker handling data ingestion from MQTT to PostgreSQL.
5. **`api`**: .NET 10 ASP.NET Core backend serving REST routes and SignalR hubs (Port 5000).
6. **`frontend`**: React + TypeScript client served via Nginx (Port 3000).

## 🛠️ Prerequisites
- [Docker](https://docs.docker.com/get-docker/) (with Docker Compose v2)
- Git

## ⚙️ Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/motorsport-telemetry-platform.git
   cd motorsport-telemetry-platform
   ```

2. **Build and start the platform:**
   ```bash
   docker compose up -d --build
   ```

3. **Access the Services:**
   - **Frontend Dashboard:** [http://localhost:3000](http://localhost:3000)
   - **.NET API / Swagger:** [http://localhost:5000/swagger](http://localhost:5000/swagger)
   - **Grafana (admin/admin):** [http://localhost:3001](http://localhost:3001)
   - **Prometheus:** [http://localhost:9090](http://localhost:9090)

## 🎮 Interacting with the Simulation

- **Frontend Controls**: The dashboard allows you to pause, resume, and stop the session.
- **Fault Injection**: Use the frontend "Fault Injection" panel to simulate engine overheating, brake fade, flat spots, or tyre degradation on specific cars and observe the telemetry reactions in real-time.
- **Session Analysis**: Track lap-by-lap history, fastest sectors, and fuel consumption natively via the UI or directly through the REST endpoints.

## 🗄️ Database Management
The PostgreSQL database uses a persistent Docker volume (`postgres_data`). Telemetry records and session history are maintained across container restarts.

## 📜 License
This project is licensed under the MIT License.
