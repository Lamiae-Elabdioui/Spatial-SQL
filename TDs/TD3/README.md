# TD-3: Spatial SQL Functions

## Objective

Determine how many parcels in Florida are located within 1 km of fire points. Fire points are defined as the centroids of specific parcels.

For additional reference, consult the official [PostGIS documentation](https://postgis.net/docs/reference.html).

---

## Steps to Complete the Exercise

### 1. Import the Shapefile into PostGIS

- Download the shapefile for Florida parcels from the provided [link](https://maps.leegov.com/datasets/80708a2f5f56426f94c8be97c182176b/about).
- Open **PostGIS Shapefile Import/Export Manager** (search for "Shapefile" in the Windows menu to locate it).
- Select the Florida parcels shapefile.
- Import it into a PostgreSQL table.

---

### 2. Verify the Imported Data

- In **pgAdmin**, execute the following query to check the imported data:
  ```sql
  SELECT COUNT(*) FROM parcels;
  ```

---

### 3. Identify the Fire Point (Centroid of Parcel 462273)

- Execute the following query to find the fire point:
  ```sql
  SELECT ST_Centroid(geom) AS fire_point
  FROM parcels
  WHERE gid = 462273;
  ```

---

### 4. Create a 1 km Risk Zone Around the Fire Point

#### a. Visualize the Risk Zone in QGIS

1. In **QGIS**, duplicate the `parcels` layer and rename it to `fire-risk`.
2. Right-click on the new layer and select **Filter**.
3. Use the following filter expression:
   ```sql
   ST_DWithin(geom, (SELECT ST_Centroid(geom) FROM "public"."parcels" WHERE gid = 462273), 1000)
   ```

---

### 5. Analyze Spatial Data with SQL

#### a. How Many Parcels Are Located Within 1 km of Both Target Parcels (gid = 460957 and gid = 462273)?

- Execute the following query:
  ```sql
  SELECT COUNT(*)
  FROM parcels
  WHERE ST_DWithin(geom, (SELECT ST_Centroid(geom) FROM parcels WHERE gid = 462273), 1000)
     OR ST_DWithin(geom, (SELECT ST_Centroid(geom) FROM parcels WHERE gid = 460957), 1000);
  ```

#### b. What is the total area of parcels close to the fire?

Execute the following query:
```sql
SELECT SUM(ST_Area(geom))
FROM parcels
WHERE ST_DWithin(geom, (SELECT ST_Centroid(geom) FROM parcels WHERE gid = 462273), 1000)
   OR ST_DWithin(geom, (SELECT ST_Centroid(geom) FROM parcels WHERE gid = 460957), 1000);
```
```
