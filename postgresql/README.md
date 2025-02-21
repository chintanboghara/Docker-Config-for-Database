# Local PostgreSQL Setup

This project uses Docker Compose to run a PostgreSQL container along with Adminer for database management. The configuration includes:

- **PostgreSQL Version:** 14
- **Container Name:** `postgres_db`
- **Database:** `rootDB`
- **User:** `root`
- **Password:** `root`
- **Data Persistence:** Uses a named volume `postgres_data`
- **Healthcheck:** Ensures the PostgreSQL service is ready to accept connections

---

## Starting PostgreSQL

### If `docker-compose.yml` is in the Root Folder

```bash
docker-compose up
```

### If `docker-compose.yml` is in a Nested Folder

```bash
docker-compose -f ./postgresql/docker-compose.yml up
```

This command builds and starts the PostgreSQL container along with Adminer.

---

## Accessing Adminer

1. Open your browser and navigate to [http://localhost:8080](http://localhost:8080).
2. In Adminer, select **PostgreSQL** as the system.
3. Enter the following credentials:
   - **Server:** `db` (the service name)
   - **Username:** `root`
   - **Password:** `root`
   - **Database:** `rootDB`
4. Click **Login** to access the PostgreSQL GUI.

---

## Running Commands Inside the PostgreSQL Container

To check the PostgreSQL version, run the following command:

```bash
docker-compose -f postgresql/docker-compose.yml run db psql -U root -d rootDB -h db -c "SELECT version();"
```

**Explanation:**

- **`-f postgresql/docker-compose.yml`**: Specifies the Docker Compose file location. Omit this flag if the file is in the root folder.
- **`run db`**: Executes a one-time command in the `db` service.
- **`psql`**: Launches the PostgreSQL command-line client.
- **`-U root`**: Uses the username `root` (as defined in the Docker Compose file).
- **`-d rootDB`**: Connects to the `rootDB` database.
- **`-h db`**: Specifies the host as `db` (the service name within the Docker network).
- **`-c "SELECT version();"`**: Executes the SQL command to display the PostgreSQL version.

When prompted, enter the password `root` (as defined in the Docker Compose file). The output should resemble:

```bash
                                                      version
---------------------------------------------------------------------------------------------------
 PostgreSQL 14.x on x86_64-pc-linux-gnu, compiled by gcc (Debian ...), 64-bit
(1 row)
```

You can now execute additional PostgreSQL commands as needed.

---

## Stopping the Services

To stop and remove the containers, networks, and volumes created by Docker Compose, run:

```bash
docker-compose down
```
