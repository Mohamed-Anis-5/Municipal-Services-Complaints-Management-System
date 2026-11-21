# Municipal Services Complaints Management System

A full-stack web application designed to streamline the reporting, tracking, and resolution of municipal service complaints. Built as an academic **Projet de Fin d'Année (PFA)** at the **Faculté des Sciences de Monastir (FSM)**, the platform connects citizens with local municipal services using geospatial data to map and manage issues efficiently.

## Key Features

- **Citizen Complaint Submission:** Submit detailed reports for municipal issues (e.g., road damage, street lighting, waste management) with geographic coordinates.
- **Geospatial Mapping:** Powered by **PostgreSQL 16 + PostGIS 3.4**, supporting spatial queries and location-based tracking of reported incidents.
- **Status Tracking:** Follow complaints through their lifecycle from submission to resolution.
- **Municipal Administration:** Review incoming complaints, manage assignments, and update resolution statuses.
- **Containerized Stack:** Orchestrated with **Docker Compose**, including database healthchecks and persistent storage.

## Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Backend** | Java, Spring Boot, Spring Data JPA, REST API |
| **Frontend** | React, Vite (served via container port `80` → `5173`) |
| **Database** | PostgreSQL 16, PostGIS 3.4 |
| **DevOps** | Docker, Docker Compose |

## Project Structure

```text
Municipal-Services-Complaints-Management-System/
├── backend/              # Spring Boot REST API & Dockerfile
├── frontend/             # React frontend & Dockerfile
├── docker-compose.yml    # Multi-container setup (db, backend, frontend)
├── .gitignore
└── README.md
```

## Getting Started

### Prerequisites

- [Docker](https://www.docker.com/) & Docker Compose
- *(Optional for local dev without Docker)* Java 17+, Maven, Node.js, PostgreSQL with PostGIS

### Run with Docker (Recommended)

1. **Clone the repository:**
   ```bash
   git clone git@github.com:Mohamed-Anis-5/Municipal-Services-Complaints-Management-System.git
   cd Municipal-Services-Complaints-Management-System
   ```

2. **Build and start all services:**
   ```bash
   docker compose up --build
   ```
   Docker will start the PostGIS database first, wait for it to pass the healthcheck, and then launch the Spring Boot backend and React frontend.

3. **Access the application:**
   - **Frontend:** `http://localhost:5173`
   - **Backend API:** `http://localhost:8080`
   - **PostgreSQL / PostGIS:** `localhost:5432`

4. **Stop the services:**
   ```bash
   docker compose down
   ```
   *(Add `-v` if you also want to wipe the `pgdata` database volume.)*

### Environment & Configuration

Default credentials and behavior are configured in `docker-compose.yml`:

| Variable | Default Value | Description |
| :--- | :--- | :--- |
| `POSTGRES_DB` | `municipal_db` | Database name |
| `POSTGRES_USER` | `municipal_user` | Database user |
| `POSTGRES_PASSWORD` | `municipal_pass` | Database password |
| `SPRING_JPA_HIBERNATE_DDL_AUTO` | `update` | Automatic schema updates |
| `APP_SEED_ENABLED` | `false` | Set to `"true"` to enable initial data seeding |

### Local Development (Without Docker)

1. **Database:** Start a local PostgreSQL instance with the `postgis` extension enabled, or run only the database container:
   ```bash
   docker compose up -d db
   ```
2. **Backend:**
   ```bash
   cd backend
   ./mvnw spring-boot:run
   ```
3. **Frontend:**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```

## Author

**Mohamed Anis Bahri**
- GitHub: [@Mohamed-Anis-5](https://github.com/Mohamed-Anis-5)
- LinkedIn: [Mohamed Anis Bahri](https://www.linkedin.com/in/mohamed-anis-bahri)
