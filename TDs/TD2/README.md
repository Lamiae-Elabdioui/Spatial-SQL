# TD-2: Creating Tables with Spatial Columns

## 1. Create Spatial Tables (Points)

- Use **pgAdmin** to create a table `points_of_interests` with a geometric column of type `Point`:
  ```sql
  CREATE TABLE points_of_interests (
      id SERIAL PRIMARY KEY,
      nom VARCHAR(255),
      geom GEOMETRY(Point, 4326)
  );
