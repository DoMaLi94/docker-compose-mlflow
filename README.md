# MLflow with PostgreSQL and MinIO

A complete Docker Compose setup for MLflow tracking server with PostgreSQL backend and MinIO artifact storage. This provides a robust, production-ready MLOps platform for tracking machine learning experiments, models, and artifacts.

## Features

- **MLflow Tracking Server**: Web UI for experiment tracking and model management
- **PostgreSQL 17.6**: Reliable backend database for metadata storage
- **MinIO**: S3-compatible object storage for ML artifacts
- **Nginx**: Reverse proxy with optimized configurations
- **Automated Setup**: Auto-creates buckets and handles initialization
- **Data Persistence**: Named volumes ensure data survives container restarts

## Credits

Based on **"Practical Deep Learning at Scale with MLFlow"** by Packt Publishing ([original repo](https://github.com/PacktPublishing/Practical-Deep-Learning-at-Scale-with-MLFlow/tree/main/chapter03/mlflow_docker_setup)).

**Key Improvements**: 
- Upgraded to PostgreSQL 17.6 (from MySQL) for better performance and compatibility
- Latest software versions: MLflow 3.3.1, MinIO 2025-07-23, Python 3.11

## Prerequisites

- Docker and Docker Compose installed
- At least 4GB RAM available for containers
- Ports 80, 9000, and 9001 available on your system

## Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/DoMaLi94/docker-compose-mlflow.git
   cd docker-compose-mlflow
   ```

2. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your preferred credentials
   ```

3. **Start all services**
   ```bash
   docker compose up -d
   ```

## Services & Access Points

| Service | URL | Purpose | Credentials |
|---------|-----|---------|-------------|
| **MLflow UI** | http://localhost | Experiment tracking & model management | None required |
| **MinIO Console** | http://localhost:9001 | Object storage management | Use AWS credentials from .env |
| **MinIO API** | http://localhost:9000 | S3-compatible API endpoint | Use AWS credentials from .env |

## Configuration

### Environment Variables

Create a `.env` file in the root directory:

```env
# MinIO configuration
AWS_ACCESS_KEY_ID=minio
AWS_SECRET_ACCESS_KEY=minio123
MLFLOW_BUCKET_NAME=mlflow
DATA_REPO_BUCKET_NAME=data

# PostgreSQL configuration
POSTGRES_DATABASE=mlflow_database
POSTGRES_USER=mlflow_user
POSTGRES_PASSWORD=mlflow
```

### Variable Explanations

- **AWS_ACCESS_KEY_ID/AWS_SECRET_ACCESS_KEY**: MinIO credentials for S3-compatible storage
- **MLFLOW_BUCKET_NAME**: Stores MLflow artifacts (models, plots, metrics)
- **DATA_REPO_BUCKET_NAME**: Additional bucket for datasets and custom files
- **POSTGRES_DATABASE**: Database name for MLflow metadata storage
- **POSTGRES_USER**: PostgreSQL username for MLflow database access
- **POSTGRES_PASSWORD**: PostgreSQL password for MLflow database access

### Default Network Ports

- **Port 80**: MLflow web interface (via Nginx)
- **Port 9000**: MinIO S3 API (via Nginx) 
- **Port 9001**: MinIO web console (via Nginx)
- **Port 5432**: PostgreSQL (internal network only)

## Usage

### Basic Operations

```bash
# Start all services
docker compose up -d

# View real-time logs
docker compose logs -f

# View logs for specific service
docker compose logs -f mlflow

# Check service status
docker compose ps

# Stop all services
docker compose down

# Stop and remove all data
docker compose down -v
```

## Data Persistence & Storage

### Volume Management

The setup uses Docker named volumes for persistent data:

- **`postgres_data`**: Contains all MLflow metadata
  - Experiments, runs, parameters, metrics
  - Model registry information
  - User data and configurations

- **`minio_data`**: Contains all artifact storage
  - Trained models and model artifacts
  - Plots, images, and visualizations  
  - Datasets and custom files
  - Logged artifacts from experiments