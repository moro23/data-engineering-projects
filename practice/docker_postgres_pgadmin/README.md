# Docker Compose Setup: PostgreSQL and pgAdmin

This repository contains a `docker-compose.yml` configuration to set up PostgreSQL and pgAdmin on the same network using Docker Compose.

## Prerequisites

Ensure you have the following installed on your system:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## Services Configured

### PostgreSQL
- **Image**: `postgres:13`
- **Container Name**: `postgres_container`
- **Default Database**: `ny_taxi_db`
- **Username**: `root`
- **Password**: `password`
- **Data Volume**: `./ny_taxi_postgres_data:/var/lib/postgresql/data`
- **Exposed Port**: `5432` (changeable if already in use on the host)

### pgAdmin
- **Image**: `dpage/pgadmin4`
- **Container Name**: `pgadmin_container`
- **Default Email**: `admin@admin.com`
- **Default Password**: `password`
- **Depends On**: `pgdatabase` service
- **Exposed Port**: `8080`

## Network
Both services are connected on a custom Docker network named `my_network`.

## Usage

### 1. Clone the Repository
```bash
git clone <repository-url>
cd <repository-directory>
```

### 2. Start the Services
Run the following command to start the PostgreSQL and pgAdmin services:
```bash
docker-compose up -d
```

### 3. Access pgAdmin
Open your browser and navigate to:
```
http://localhost:8080
```

- **Login Credentials**:
  - Email: `admin@admin.com`
  - Password: `password`

### 4. Add PostgreSQL Server in pgAdmin
1. Log in to pgAdmin.
2. Create a new server:
   - **Name**: `Postgres Server`
   - **Connection**:
     - **Host**: `pgdatabase`
     - **Port**: `5432` (or the updated port if changed in `docker-compose.yml`)
     - **Username**: `root`
     - **Password**: `password`

### 5. Stop the Services
To stop the running services:
```bash
docker-compose down
```

## Troubleshooting

### Port 5432 Already in Use
If you encounter a `bind: address already in use` error for port `5432`:
- Change the host port in the `docker-compose.yml` file to another port (e.g., `5433`).
- Restart the setup with:
  ```bash
  docker-compose up -d
  ```

### Data Persistence
The PostgreSQL data is stored in the `./ny_taxi_postgres_data` directory on the host machine. This ensures that data remains intact even if the container is stopped or removed.

## Cleanup
To remove all containers, networks, and volumes created by this setup:
```bash
docker-compose down -v
```

## License
This project is licensed under the MIT License.
