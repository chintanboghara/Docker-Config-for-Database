# Local MongoDB Setup

This project uses Docker Compose to run a local MongoDB instance with the following configurations:

- **MongoDB Version:** 5.0 (pinned for consistency)
- **Container Name:** `mongo`
- **Credentials:**  
  - Username: `root`  
  - Password: `example`
- **Persistent Storage:** Uses a named volume `mongo_data` for data persistence
- **Healthcheck:** A healthcheck is configured to ensure the service is responsive

## Starting MongoDB

### If the Docker Compose file is in the Root Folder

```bash
docker-compose up
```

### If the Docker Compose file is in a Nested Folder

```bash
docker-compose -f ./mongodb/docker-compose.yml up
```

This command will build and start your MongoDB container.

## Connection String

Use the following connection string to connect to MongoDB:

```bash
mongodb://<username>:<password>@localhost:27017
```

Replace `<username>` and `<password>` with the credentials provided above (default: `root` and `example`).

## Connecting with MongoDB Compass

1. Download and install [MongoDB Compass](https://www.mongodb.com/products/tools/compass).
2. Open MongoDB Compass.
3. Enter the connection string (with the proper username and password).
4. Click **Connect**.

## Accessing the Mongo Shell via Docker

### Without Authentication

If you start a shell without specifying credentials, you might see an error when listing databases due to missing authentication:

```bash
docker-compose run mongo mongosh --host mongo
```

- **Note:** This command runs the `mongosh` shell inside the `mongo` container. Since no credentials are provided, trying to list databases (e.g., with `show dbs`) will result in an authentication error.

### With Authentication

To access the Mongo shell with the correct credentials, run:

```bash
docker-compose run mongo mongosh -u root -p example --host mongo
```

- `-u root` specifies the username.
- `-p example` specifies the password.

After executing the command, you should see output similar to:

```bash
Current Mongosh Log ID: <log_id>
Connecting to:          mongodb://<credentials>@mongo:27017/?directConnection=true&appName=mongosh+<version>
Using MongoDB:          6.0.8
Using Mongosh:          1.10.1

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

test>
```

At the `mongosh` prompt, list the databases by running:

```bash
show dbs
```

## Stopping MongoDB

To stop and remove the containers, run:

```bash
docker-compose down
```

This command stops the MongoDB container and removes the associated network.
