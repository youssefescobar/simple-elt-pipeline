Here’s a **README** for your ELT (Extract, Load, Transform) pipeline project based on the files you shared:

---

# ELT Pipeline with PostgreSQL and Docker

## Project Overview
This project implements an ELT (Extract, Load, Transform) pipeline using Docker containers to manage two PostgreSQL databases and a Python script to handle the data movement. The pipeline extracts data from a source PostgreSQL database, transfers it, and loads it into a destination PostgreSQL database.

The project is containerized using Docker Compose, ensuring easy setup, isolation, and scalability.

---

## Features
- **Data Extraction**: Extracts data from the source PostgreSQL database using `pg_dump`.
- **Data Loading**: Loads the extracted data into the destination PostgreSQL database using `psql`.
- **Containerization**: Fully containerized using Docker and Docker Compose.
- **PostgreSQL Initialization**: Source database is pre-populated with an initial schema/data via SQL scripts.
- **Error Handling**: Retries connection to the database to ensure robust execution.

---

## Project Structure
```plaintext
.
├── docker-compose.yml    # Defines the Docker Compose configuration
├── source_db_init/
│   └── init.sql          # SQL script to initialize the source database
├── elt/
│   ├── elt_script.py     # Python script implementing the ELT logic
│   └── Dockerfile        # Dockerfile for the ELT container
```

---

## Technologies Used
- **Docker**: For containerization.
- **PostgreSQL**: For managing the source and destination databases.
- **Python**: For implementing the ELT script.
- **pg_dump and psql**: For database dump and load operations.

---

## Getting Started

### Prerequisites
- Docker and Docker Compose installed on your system.

### Setup and Run

1. **Clone the repository**:
   ```bash
   git clone https://github.com/youssefescobar/simple-elt-pipeline.git
   cd simple-elt-pipeline
   ```

2. **Initialize the Source Database**:
   Modify `source_db_init/init.sql` to set up the initial schema or data.

3. **Start the Containers**:
   Run the following command to start all services:
   ```bash
   docker-compose up --build
   ```
   This will:
   - Start two PostgreSQL containers (`source_postgres` and `destination_postgres`).
   - Execute the ELT pipeline script in the `elt_script` container.

4. **Verify the Data Transfer**:
   After the pipeline completes, you can connect to the destination database to verify the transferred data:
   ```bash
   docker exec -it <destination_postgres_container_id> psql -U postgres -d destination_db
   ```

5. **Stop the Containers**:
   To stop the pipeline and containers, run:
   ```bash
   docker-compose down
   ```

---

## Configuration
- Database credentials and configurations are hardcoded in the `elt_script.py`. You can externalize these into environment variables or configuration files for better security and flexibility.

---

## Challenges and Solutions
1. **Database Connection Handling**:
   - Implemented a retry mechanism using `pg_isready` to ensure the database is ready before executing commands.
2. **Container Communication**:
   - Configured all services on the same Docker network (`elt_network`) for seamless inter-container communication.


---

## License
This project is licensed under the MIT License.

---
