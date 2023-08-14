# Docker Compose Setup for WordPress, MySQL, and PhpMyAdmin

This Docker Compose setup allows you to easily get a WordPress site up and running alongside a MySQL database and PhpMyAdmin for database management.

## Version

Docker Compose Version: `3.3`

## Services

### 1. Database (MySQL)

- **Image**: `mysql:5.7`
- **Environment Variables**:

  - Root Password: `password`
  - Database: `wordpress`
  - User: `wordpress`
  - Password: `wordpress`
- **Network**: `wpsite`
- **Data Volume**: `db_data` at `/var/lib/mysql`

### 2. PhpMyAdmin

- **Image**: `phpmyadmin/phpmyadmin`
- **Ports**: `8080` on host mapped to `80` on container
- **Environment Variables**:

  - Host: `db`
  - Root Password: `password`
- **Network**: `wpsite`
- **Dependencies**: Depends on the `db` service to be operational

### 3. WordPress

- **Image**: `wordpress:latest`
- **Ports**: `8000` on host mapped to `80` on container
- **Environment Variables**:

  - DB Host: `db:3306`
  - DB User: `wordpress`
  - DB Password: `wordpress`
  - DB Name: `wordpress`
- **Network**: `wpsite`
- **Dependencies**: Depends on the `db` service to be operational
- **Volume**: Maps current directory to `/var/www/html` in the container

## Networks

- `wpsite`

## Volumes

- `db_data`: A named volume to persist the MySQL database data

## Usage

1. Ensure you have Docker and Docker Compose installed on your machine.
2. Clone this repository or download the `docker-compose.yml` file.
3. Run the command `docker-compose up -d` from the directory containing the file.
4. Access WordPress at `http://localhost:8000` and PhpMyAdmin at `http://localhost:8080`.

## Stopping the Services

To stop the services, run the command `docker-compose down`. If you wish to also remove the volumes (data), run `docker-compose down -v`.
