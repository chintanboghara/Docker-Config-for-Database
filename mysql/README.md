# Local MySQL & Adminer Setup

This setup uses Docker Compose to run a MySQL container alongside Adminer, a lightweight web-based database management tool. The configuration creates a persistent volume for MySQL data and uses the following credentials:

- **MySQL Credentials:**  
  - **Username:** `root`  
  - **Password:** `root`  
  - **Database:** `rootDB`

## Starting the Services

### If `docker-compose.yml` Is in the Root Folder

Run:

```bash
docker-compose up
```

### If `docker-compose.yml` Is in a Nested Folder

For example, if it's located at `./mysql/docker-compose.yml`, run:

```bash
docker-compose -f ./mysql/docker-compose.yml up
```

This command will start both the MySQL container (exposed on port 3306) and the Adminer container (accessible on port 8080).

## Accessing Adminer

1. Open your browser and navigate to [http://localhost:8080](http://localhost:8080).
2. On the Adminer login page:
   - **System:** MySQL
   - **Server:** `db` (or `localhost` if preferred)
   - **Username:** `root`
   - **Password:** `root`
   - **Database:** `rootDB` (optional; leave blank to see all databases)
3. Click **Login** to start managing your MySQL database through the Adminer GUI.

## Accessing the MySQL Monitor

To execute SQL queries directly via the terminal, run the MySQL client within the `db` container. Use the following command (adjusting the file path if your `docker-compose.yml` is not in the root):

```bash
docker-compose -f ./mysql/docker-compose.yml run db mysql -u root -p --host=db
```

### Explanation of the Command

- **`-f ./mysql/docker-compose.yml`**  
  Points to the Docker Compose file. Omit this flag if the file is in the root folder.
  
- **`run db`**  
  Runs a one-time command in the `db` service (MySQL container).
  
- **`mysql`**  
  Launches the MySQL client inside the container.
  
- **`-u root`**  
  Specifies the MySQL username (`root`).
  
- **`-p`**  
  Prompts for the MySQL password (enter `root` when prompted).
  
- **`--host=db`**  
  Specifies that the client should connect to the `db` container.

After entering the password, you should see output similar to:

```bash
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 14
Server version: 8.1.0 MySQL Community Server - GPL

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

## Listing All Databases

Once at the MySQL prompt, list your databases with:

```sql
SHOW DATABASES;
```

You should see output similar to:

```bash
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| rootDB             |
+--------------------+
4 rows in set (0.07 sec)
```
