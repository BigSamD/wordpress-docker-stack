```
# Installation and Startup of WordPress, MySQL, and PhpMyAdmin using Docker Compose

## Prerequisites

- Have Docker and Docker Compose installed on your machine.

## Instructions

1. **Download the configuration file**:
   - Clone this repository or download the `docker-compose.yml` file.

2. **Start the services**:
```

   docker-compose up -d

```

3. **Access the services**:
   - WordPress: Open a browser and visit `http://localhost:8000`
   - PhpMyAdmin: Open a browser and visit `http://localhost:8080`

## Stopping the Services

To stop and remove the services:
```

docker-compose down

```

If you also wish to remove the volumes (data):
```

docker-compose down -v

```

```
