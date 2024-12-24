# TD-1: Installing PostGIS and Creating a Spatial Database

## 1. Download and Install PostgreSQL

- Visit the [PostgreSQL download page](https://www.postgresql.org/download/) to download the latest version suitable for your operating system. PostgreSQL is compatible with Linux, macOS, Windows, BSD, and Solaris.
- Follow the installation guide to set up the software on Windows, Linux, or macOS.
- During installation, set a password for the `postgres` user. Choose a password that is easy to remember as it will be needed to connect to PostGIS.

## 2. Download and Install PostGIS

- During the PostgreSQL installation, check all components. Stack Builder will be used to download PostGIS.
- When prompted, ensure the option to launch Stack Builder is checked, and follow the instructions.
- Once Stack Builder starts, select the PostgreSQL version corresponding to your installation to add PostGIS. **Note:** An internet connection is required.
- Select PostGIS from the available options. You can also check “Create a spatial database,” though we will manually create a database using **pgAdmin 4**.
- Once the installation is complete, click “Finish.” PostGIS is now installed.

## 3. Create a Database Using PgAdmin 4

1. Launch **pgAdmin 4**, the PostgreSQL database management tool.
2. Log in using the password you set during the PostgreSQL installation.
3. Expand **Servers**, then right-click on **PostgreSQL** > **Create** > **Database**.
4. Name your new database (e.g., `spatial-db-1`), then click **Save**.

### Add the PostGIS Extension

1. Expand the **Databases** section and navigate to your newly created database (`spatial-db-1`).
2. Right-click on your database and select **Query Tool**.
3. In the query editor, enter the following command:  
   ```sql
   CREATE EXTENSION postgis;
