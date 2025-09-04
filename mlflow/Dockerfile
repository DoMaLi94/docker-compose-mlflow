ARG PYTHON_VERSION=3.11-slim

FROM python:${PYTHON_VERSION}

# Re-declare ARG after FROM to make it available in subsequent layers
ARG MLFLOW_VERSION=3.3.1

# Install MLflow and additional packages
RUN pip install mlflow==${MLFLOW_VERSION} boto3 psycopg2-binary