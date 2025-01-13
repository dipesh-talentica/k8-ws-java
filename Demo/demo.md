# Set up PostgreSQL database and pg-admin ​using docker compose.


This guide explains how to set up a PostgreSQL database and pgAdmin using Docker Compose and how to connect pgAdmin to the database.

## Prerequisites

Ensure you have the following installed on your machine:
- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/)

---

## Setup Instructions

1.Create a folder demo and inside it create a `docker-compose.yml` file with the following content:

   ```yaml
   
   services:
     postgres:
       image: postgres:latest
       container_name: postgres_db
       restart: always
       environment:
         POSTGRES_USER: admin
         POSTGRES_PASSWORD: admin123
         POSTGRES_DB: my_database
       volumes:
         - postgres_data:/var/lib/postgresql/data
       ports:
         - "5432:5432"
       networks:
         - app_network

     pgadmin:
       image: dpage/pgadmin4:latest
       container_name: pgadmin
       restart: always
       environment:
         PGADMIN_DEFAULT_EMAIL: admin@example.com
         PGADMIN_DEFAULT_PASSWORD: admin123
       ports:
         - "5050:80"
       networks:
         - app_network

   volumes:
     postgres_data:
       driver: local

   networks:
    app_network:
       driver: bridge       
   ```

2. Start the containers:
   ```bash
   docker-compose up
   ```

3. Verify the services are running:
   ```bash
   docker ps
   ```

   You should see both `postgres_db` and `pgadmin` containers running.

---

## Access pgAdmin

1. Open your browser and go to:
   ```
   http://localhost:5050
   ```

2. Log in to pgAdmin using the default credentials:
   - **Email**: `admin@example.com`
   - **Password**: `admin123`

---

## Connect pgAdmin to PostgreSQL

1. In pgAdmin, click **Add New Server**.

2. Fill in the connection details:
   - **Name**: `demo PostgreSQL` (or any name you prefer)
   - **Host**: `postgres` (this is the service name defined in the `docker-compose.yml` file)
   - **Port**: `5432`
   - **Username**: `admin` (set in the environment variables)
   - **Password**: `admin123` (set in the environment variables)

3. Click **Save** to add the server.

4. You should now see your database `my_database` in the left-hand panel of pgAdmin.

---

## Additional Information

- **Data Persistence**:
  The PostgreSQL data is stored in a Docker volume (`postgres_data`), so your data will persist even if the container is stopped or removed.

- **Customizing Configuration**:
  You can modify the `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`, and pgAdmin credentials in the `docker-compose.yml` file to suit your requirements.

- **Stopping the Containers**:
  To stop the running containers, use:
  ```bash
  docker-compose down
  ```

---

## Troubleshooting

- If pgAdmin cannot connect to PostgreSQL, ensure that both services are running and on the same network (`app_network`).
- Check the logs for PostgreSQL or pgAdmin:
  ```bash
  docker logs postgres_db
  docker logs pgadmin
  ```
- If needed, test connectivity between the containers:
  ```bash
  docker exec -it pgadmin ping postgres
  ```

---

Enjoy your PostgreSQL setup with pgAdmin!
