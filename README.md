# Weather Data Quality Pipeline

Automated weather data processing workflow built with n8n.

This project was developed while completing the Intermediate Workflow Automation with n8n course. The workflow demonstrates an end-to-end ETL process including scheduled data ingestion, transformation, deduplication, batch processing, and quality validation.

## Repository Description

Weather data quality pipeline built in n8n as part of the Intermediate Workflow Automation with n8n course.

## Features

* Hourly scheduled execution
* Weather API integration
* Data transformation and normalization
* Duplicate detection
* Batch processing
* Data quality validation
* Conditional success/failure routing
* Workflow orchestration using n8n

## Technologies

* n8n
* JavaScript
* HTTP Request
* Data Tables
* Workflow Automation
* REST APIs

## Workflow Architecture

``` text
Hourly Schedule
       │
       ▼
Fetch Weather API
       │
       ▼
Transform Data
       │
       ▼
Check Existing Records
       │
       ▼
Filter New Records
       │
       ▼
Batch Process Records
       │
       ├─────────────┐
       ▼             │
Add Batch Timestamp  │
       │             │
       └─────────────┘
       │
       ▼
Evaluate Output
       │
       ▼
Quality Gate
    ┌──┴───────────┐
    │              │
    ▼              ▼
Store Data   Log Pipeline Error
    │
    ▼
Success
```

## Workflow Steps

<p align="left">
  <img src="images\workflow-overview (1).png" width="1000">
</p>

### 1. Data Ingestion

The workflow runs automatically every hour and retrieves weather data from the wttr.in API.

### 2. Data Transformation

Raw weather data is normalized into a structured format containing:

* city
* temperature
* humidity
* weather description
* timestamp
* unique date key

### 3. Duplicate Detection

Existing records are checked against stored data using a generated date key. Previously processed records are excluded.

### 4. Batch Processing

New records are processed through a batching mechanism to support scalable workflow execution.

### 5. Data Quality Validation

The workflow validates:

* city name presence
* valid temperature values
* expected data structure

### 6. Conditional Routing

Quality checks determine whether execution continues through the Success path or Failure path.

## Sample Output

{
"city": "London",
"temp_c": 18,
"humidity": 72,
"description": "Partly cloudy",
"fetched_at": "2026-05-28T14:00:00Z",
"date_key": "London_2026-05-28"
}

## Learning Context

This project was created while completing the Intermediate Workflow Automation with n8n course.

Skills practiced:

* Workflow design
* API integration
* Data transformation
* Deduplication logic
* Batch processing
* Data quality validation
* Conditional workflow routing
* End-to-end workflow orchestration

## Future Improvements

* Store validated records in a database
* Send Telegram notifications on success/failure
* Add execution monitoring and alerts
* Support multiple cities
* Create weather trend reporting dashboards
* Add error logging and retry mechanisms
