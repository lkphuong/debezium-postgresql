# Project Overview

This project sets up a Debezium environment using Docker Compose to capture changes from a PostgreSQL database and stream them to Kafka. The setup includes Zookeeper, Kafka, Kafka Connect, Debezium UI, and Kafka UI.

## Project Structure

- `docker-compose.yml`: Docker Compose configuration for setting up the Debezium environment.
- `postgres-connector.json`: Configuration file for the PostgreSQL Debezium connector.
- `note`: Instructions for running the connector.
- `README.md`: Project overview and setup instructions.

## Prerequisites

- Docker
- Docker Compose

## Setup and Run

### Step 1: Clone the Repository

```sh
git clone <url>
cd <repository-directory>
```

### Step 2: Start the Docker Containers

Run the following command to start all the services defined in the `docker-compose.yml` file:

```sh
docker-compose pull
docker-compose up -d
```

### Step 3: Configure the PostgreSQL Connector

Use the following `curl` command to configure the PostgreSQL connector:

```sh
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" \
  http://localhost:8083/connectors/ -d @postgres-connector.json
```

### Step 4: Access the UIs

- **Debezium UI**: [http://localhost:8080](http://localhost:8080)
- **Kafka UI**: [http://localhost:8085](http://localhost:8085)

## Configuration Details

### `postgres-connector.json`

This file contains the configuration for the PostgreSQL Debezium connector. Key properties include:

- `database.hostname`: Hostname of the PostgreSQL database.
- `database.port`: Port of the PostgreSQL database.
- `database.user`: Username for the PostgreSQL database.
- `database.password`: Password for the PostgreSQL database.
- `database.dbname`: Name of the PostgreSQL database.
- `database.server.name`: Logical name for the database server.
- `plugin.name`: Plugin to use for capturing changes.
- `slot.name`: Replication slot name.
- `publication.name`: Publication name.
- `database.history.kafka.bootstrap.servers`: Kafka bootstrap servers.
- `database.history.kafka.topic`: Kafka topic for schema changes.
- `topic.prefix`: Prefix for Kafka topics.
- `table.include.list`: List of tables to include.

### `docker-compose.yml`

This file defines the services required for the Debezium environment:

- **Zookeeper**: Manages Kafka brokers.
- **Kafka**: Message broker.
- **Kafka Connect**: Connects Kafka with external systems.
- **Debezium UI**: Web interface for managing Debezium connectors.
- **Kafka UI**: Web interface for managing Kafka topics and messages.
