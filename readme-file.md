# End-to-End ETL Pipeline with PostgreSQL, Pandas, and Apache Airflow

This project implements a complete ETL (Extract, Transform, Load) pipeline that:
- Extracts weather data from the OpenWeather API
- Transforms it using Pandas
- Loads it into a PostgreSQL database
- Orchestrates the entire workflow with Apache Airflow
- Runs everything in Docker containers

## Features

- **Data Extraction**: Fetches current weather data from OpenWeather API for multiple cities
- **Data Transformation**: Processes and structures the data using Pandas
- **Data Loading**: Stores the data in a PostgreSQL database with proper relationships
- **Workflow Orchestration**: Uses Apache Airflow for task scheduling and management
- **Containerization**: Runs in Docker containers for easy deployment and portability
- **Error Handling**: Comprehensive logging and error recovery
- **Database Structure**: Well-designed schema with appropriate relationships and indexes

## Tech Stack

- Python 3.9+
- Pandas for data manipulation
- PostgreSQL for data storage
- Apache Airflow for orchestration
- Docker for containerization

## Project Structure

```
etl_pipeline/
│
├── docker-compose.yml
├── Dockerfile
├── requirements.txt
│
├── dags/
│   ├── weather_etl_dag.py
│   └── sql/
│       └── create_tables.sql
│
├── scripts/
│   ├── extract.py
│   ├── transform.py
│   └── load.py
│
└── config/
    └── config.py
```

## Setup Instructions

### Prerequisites

- Docker and Docker Compose
- OpenWeather API key (sign up at [OpenWeatherMap](https://openweathermap.org/api))

### Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/etl-pipeline.git
   cd etl-pipeline
   ```

2. Set your OpenWeather API key as an environment variable:
   ```bash
   export OPENWEATHER_API_KEY=your_api_key_here
   ```

3. Start the containers:
   ```bash
   docker-compose up -d
   ```

4. Access the Airflow web interface at `http://localhost:8080` 
   - Username: `admin`
   - Password: `admin`

5. The DAG should be visible in the Airflow UI and ready to run

## How It Works

### Extract

The pipeline fetches current weather data for multiple cities defined in the configuration file using the OpenWeather API. The data is stored as raw JSON files with timestamps.

### Transform

The raw JSON data is processed using Pandas:
- Structures the data into a normalized format
- Creates separate datasets for cities and weather measurements
- Cleans and formats the data for database loading
- Outputs CSV files for each dataset

### Load

The transformed data is loaded into PostgreSQL:
- Cities are loaded first to establish primary keys
- Weather data is loaded with proper foreign key relationships
- Duplicate handling is implemented for data integrity

### Orchestration

Apache Airflow manages the entire workflow:
- Initializes the database schema if needed
- Schedules daily runs of the pipeline
- Handles dependencies between tasks
- Provides monitoring and failure recovery

## Customization

You can customize the pipeline by:

1. Modifying the list of cities in `config.py`
2. Changing the schedule interval in the DAG file
3. Adding more data transformations in `transform.py`
4. Extending the database schema in `create_tables.sql`

## License

This project is licensed under the MIT License - see the LICENSE file for details.
