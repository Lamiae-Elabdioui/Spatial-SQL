# TD-2: Creating Tables with Spatial Columns

## 1. Create Spatial Tables (Points)

- Use **pgAdmin** to create a table `points_of_interests` with a geometric column of type `Point`:
  ```sql
  CREATE TABLE points_of_interests (
      id SERIAL PRIMARY KEY,
      nom VARCHAR(255),
      geom GEOMETRY(Point, 4326)
  );
  ```

- Insert data into this table using **QGIS**:
  1. For the first connection from QGIS:
     - Right-click on **PostgreSQL** in the explorer panel.
     - Select **New Connection** and provide the following information:
       - Database name
       - Username and password
       - Host and port details
     - Test the connection.
  2. Once the connection is created, double-click on the `points_of_interests` table to add it as a layer in QGIS.
  3. Switch to **edit mode**.
  4. Add points, then **save**.

- Go back to **pgAdmin** and execute the following query to verify:
  ```sql
  SELECT * FROM points_of_interests;
  ```

---

## 2. Create Spatial Tables (Polygons)

- Create a table `zones_protegees` with a geometric column of type `Polygon`:
  ```sql
  CREATE TABLE zones_protegees (
      id SERIAL PRIMARY KEY,
      nom VARCHAR(255),
      geom GEOMETRY(Polygon, 4326)
  );
  ```

- Insert data into this table using **QGIS**, then save.

- In **pgAdmin**, execute the following query to verify:
  ```sql
  SELECT * FROM zones_protegees;
  ```

---

## 3. Create a Spatial Table with a LineString Column

- Follow the same process to create a spatial table with a column of type `LINESTRING`.

Example for the table:
```sql
CREATE TABLE roads (
    id SERIAL PRIMARY KEY,
    nom VARCHAR(255),
    geom GEOMETRY(LINESTRING, 4326)
);
```
