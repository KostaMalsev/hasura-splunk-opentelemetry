# Hasura OpenTelemetry to Splunk

This repository demonstrates how to send Hasura logs wrapped as traces in OpenTelemetry format to Splunk.

## Prerequisites

- Docker Engine

## Running the Project

To run the project, use the following command:

```bash
docker compose up
```

This command will start the following services:

1. Hasura with a sidecar that sends logs in OpenTelemetry format
2. Prometheus for metric gathering
3. Grafana for metric presentation
4. OpenTelemetry collector
5. Splunk service listening on port 8088, which gathers traces sent from the OpenTelemetry collector

## Components

### 1. Hasura with OpenTelemetry Sidecar
Sends logs in OpenTelemetry format.

### 2. Prometheus
Gathers metrics from the system.

### 3. Grafana
Presents metrics in a visual dashboard.

### 4. OpenTelemetry Collector
Collects and processes telemetry data.

### 5. Splunk
Listens on port 8088 and receives traces from the OpenTelemetry collector.

## Viewing Traces in Splunk

To see the traces in Splunk:

1. Open the browser at http://localhost:18000/
2. Go to Settings -> Indexes: Look for an index named "traces" and check if any records are registered.
3. If not, configure a new "Data Input":
   - Go to Settings -> "Data Inputs" -> "HTTP Event Collector"
   - Choose "splunk_hec_token" and press edit
   - Choose "traces" for Allowed Indexes

To view the traces themselves:
- Go to "Apps" -> "Search & Reporting" -> "Datasets" -> "Create Table View"
- Choose "traces" -> "all source types..." 
- The table will preview the traces collected in Splunk

## Note

The tokens mentioned in `docker-compose.yml` and `otel-collector-config.yaml` should be the same, and you would need to configure the tokens according to your environment.