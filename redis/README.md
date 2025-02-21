# Local Redis and Redis Insight Setup

This setup deploys a Redis instance along with Redis Insight for monitoring, all managed through Docker Compose. The configuration ensures proper port mapping, persistence, and connectivity within the Docker network.

## Starting the Containers

### If the `docker-compose.yml` File is in the Root Folder

```bash
docker-compose up
```

### If the `docker-compose.yml` File is in a Nested Folder

```bash
docker-compose -f ./redis/docker-compose.yml up
```

This command will start both the Redis server and the Redis Insight dashboard.

## Accessing the Redis Insight Dashboard

1. Open your browser and navigate to [http://localhost:8001](http://localhost:8001).
2. Accept the necessary Terms & Conditions.
3. Click **"I already have a database"**.
4. Click **"Connect to Redis database"**.
5. Enter the following configuration:
   - **Host:** `redis`  
     *(Since both containers run on the same Docker network, you can use the service name `redis` to connect.)*
   - **Port:** `6379`
6. Click **"Add Redis Database"**.

You are now connected to your Redis instance via the Redis Insight dashboard!
