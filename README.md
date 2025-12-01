# Huawei Cloud Log Analysis MVP

## Description

This project provides a minimal viable product (MVP) for log analysis on Huawei Cloud. It utilizes Fluent Bit to collect logs, Huawei Cloud LTS for log management, Elasticsearch for indexing and searching, and Kibana for visualization.

## Architecture

The architecture consists of the following components:

*   **Applications/Servers:** The source of the logs.
*   **Fluent Bit Agent:** A lightweight log forwarder that collects logs from applications and sends them to Huawei Cloud LTS.
*   **Huawei Cloud Log Tank Service (LTS):** Huawei Cloud's log management service, responsible for storing and managing logs.
*   **Elasticsearch:** A powerful search and analytics engine used to index and search the logs.
*   **Kibana:** A visualization tool used to create dashboards and explore the logs.
*   **User Dashboard:** The interface for users to interact with the analyzed logs.

## Setup

1.  Install Docker and Docker Compose.
2.  Create a `fluent-bit.conf` file (see example below).
3.  Run `docker-compose up -d` to start the pipeline.

```
[SERVICE]
    Flush        1
    Log_Level    info
    Daemon       off
    Parsers_File parsers.conf

[INPUT]
    Name tail
    Path /tmp/app.log
    Parser  docker
    Tag  app.log

[OUTPUT]
    Name  stdout
    Match * 

#[OUTPUT]
#    Name  lts
#    Match * 
#    lts_url  your_lts_url
#    lts_ak   your_lts_ak
#    lts_sk   your_lts_sk
#    lts_project_id your_lts_project_id
#    lts_log_group_id your_lts_log_group_id
#    lts_log_stream_id your_lts_log_stream_id
```

## Configuration

*   **fluent-bit.conf:** Configure Fluent Bit to collect logs from your applications and forward them to Huawei Cloud LTS.  **Important:** Replace placeholders like `your_lts_url`, `your_lts_ak`, `your_lts_sk`, `your_lts_project_id`, `your_lts_log_group_id`, and `your_lts_log_stream_id` with your actual Huawei Cloud LTS credentials and identifiers. For local testing, the stdout output is enabled.
*   **Elasticsearch:**  Elasticsearch is configured for single-node development. For production environments, a proper cluster configuration is required.
*   **Kibana:** Kibana is configured to connect to Elasticsearch.

## Accessing the Dashboard

Open your web browser and navigate to `http://localhost:5601` to access the Kibana dashboard.
