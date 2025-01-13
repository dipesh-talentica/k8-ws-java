
# Set Up WordPress Using Docker Compose

This guide will help you set up a WordPress instance with a MySQL database using Docker Compose.

---

## Prerequisites

Before starting, ensure you have the following installed on your system:
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

## Directory Structure

Create a directory for the setup:
```
wordpress-docker/
├── docker-compose.yml
└── db-data/ (empty directory for database persistence)
```

---

## Step 1: Create `docker-compose.yml`

Inside the `wordpress-docker/` directory, create a file named `docker-compose.yml` and paste the following content:

```yaml
name: wordpress-demo

services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress
    ports:
      - "8080:80" # Map port 80 in the container to port 8080 on the host
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - ./wordpress-data:/var/www/html

  db:
    image: mysql:5.7
    container_name: wordpress-db
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    volumes:
      - ./db-data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin:latest
    container_name: phpmyadmin
    ports:
      - "8081:80" # Map port 80 in the container to port 8081 on the host
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: rootpassword

volumes:
  wordpress-data:
  db-data:
```

---

## Step 2: Start the Containers

Run the following commands to start the services:

```bash
cd wordpress-docker
docker-compose up -d
```

---

## Step 3: Access the Application

1. **WordPress:**
   - Open your browser and navigate to [http://localhost:8080](http://localhost:8080).
   - Complete the WordPress setup wizard (e.g., site title, admin username, and password).

2. **phpMyAdmin (Optional):**
   - Navigate to [http://localhost:8081](http://localhost:8081).
   - Log in using:
     - **Username:** `root`
     - **Password:** `rootpassword`

---

## Step 4: Persistent Data

The data for WordPress and the database is stored in the `wordpress-data/` and `db-data/` directories respectively. This ensures your data persists even if the containers are restarted.

---

## Stopping the Containers

To stop the containers, run:
```bash
docker-compose down
```

---

## Cleaning Up

To remove containers, networks, and volumes:
```bash
docker-compose down --volumes
```

---

## Troubleshooting

- If you encounter any issues, use the following command to check logs:
  ```bash
  docker-compose logs
  ```

---

Enjoy your WordPress setup powered by Docker Compose!
