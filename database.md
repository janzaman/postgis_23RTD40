# Setting up database
## Create database
```
-- Database: 23RTD40

-- DROP DATABASE IF EXISTS "23RTD40";

CREATE DATABASE "23RTD40"
    WITH
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'Dutch_Belgium.1252'
    LC_CTYPE = 'Dutch_Belgium.1252'
    LOCALE_PROVIDER = 'libc'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1
    IS_TEMPLATE = False;
```
## Create extensions
```
-- Extension: plpgsql

-- DROP EXTENSION plpgsql;

CREATE EXTENSION IF NOT EXISTS plpgsql
    SCHEMA pg_catalog
    VERSION "1.0";
-- Extension: fuzzystrmatch

-- DROP EXTENSION fuzzystrmatch;

CREATE EXTENSION IF NOT EXISTS fuzzystrmatch
    SCHEMA public
    VERSION "1.2";
-- Extension: postgis

-- DROP EXTENSION postgis;

CREATE EXTENSION IF NOT EXISTS postgis
    SCHEMA public
    VERSION "3.4.1";
-- Extension: h3

-- DROP EXTENSION h3;

CREATE EXTENSION IF NOT EXISTS h3
    SCHEMA public
    VERSION "4.1.3";
-- Extension: h3_postgis

-- DROP EXTENSION h3_postgis;

CREATE EXTENSION IF NOT EXISTS h3_postgis
    SCHEMA public
    VERSION "4.1.3";
-- Extension: pg_trgm

-- DROP EXTENSION pg_trgm;

CREATE EXTENSION IF NOT EXISTS pg_trgm
    SCHEMA public
    VERSION "1.6";
-- Extension: pointcloud

-- DROP EXTENSION pointcloud;

CREATE EXTENSION IF NOT EXISTS pointcloud
    SCHEMA public
    VERSION "1.2.4";
-- Extension: pointcloud_postgis

-- DROP EXTENSION pointcloud_postgis;

CREATE EXTENSION IF NOT EXISTS pointcloud_postgis
    SCHEMA public
    VERSION "1.2.4";
-- Extension: postgis_raster

-- DROP EXTENSION postgis_raster;

CREATE EXTENSION IF NOT EXISTS postgis_raster
    SCHEMA public
    VERSION "3.4.1";
-- Extension: postgis_sfcgal

-- DROP EXTENSION postgis_sfcgal;

CREATE EXTENSION IF NOT EXISTS postgis_sfcgal
    SCHEMA public
    VERSION "3.4.1";
-- Extension: postgis_tiger_geocoder

-- DROP EXTENSION postgis_tiger_geocoder;

CREATE EXTENSION IF NOT EXISTS postgis_tiger_geocoder
    SCHEMA tiger
    VERSION "3.4.1";
-- Extension: postgis_topology

-- DROP EXTENSION postgis_topology;

CREATE EXTENSION IF NOT EXISTS postgis_topology
    SCHEMA topology
    VERSION "3.4.1";
```
## Add data

### Raster data
voorzieningenniveau: eerst selectie van de slecht gelegen categorieën, gebaseerd op een indeling van de waarden in vier klassen volgens Jencks Natural Breaks, dan omzetten in een 1 bit raster
```
C:\> raster2pgsql -s 31370 -I -C -M C:\Users\janza\Documents\02_gis\23RTD40\Rasters\Ontwikkelingskansen2022\voorzieningsniveau_2022_natural_breaks_25_Slecht.tif -F -t 25x25 public.voorzieningenslecht | psql -U postgres -d 23RTD40
```
knooppuntwaarde: eerst selectie van de slecht gelegen categorieën, gebaseerd op een indeling van de waarden in vier klassen volgens Jencks Natural Breaks, dan omzetten in een 1 bit raster
```
C:\> raster2pgsql -s 31370 -I -C -M C:\Users\janza\Documents\02_gis\23RTD40\Rasters\Ontwikkelingskansen2022\knooppuntwaarde_OV_2022_natural_breaks_25_Slecht.tif -F -t 25x25 public.knooppuntwaardeslecht | psql -U postgres -d 23RTD40
```
pluviaal overstromingsgevoelig
```
C:\> raster2pgsql -s 31370 -I -C -M C:\Users\janza\Documents\02_gis\23RTD40\Rasters\Water_Overstroombaargebied\waterdiepte_PLU_hCC_T10_Groterdan0.tif -F -t 2x2 public.plu_hcc_t10 | psql -U postgres -d 23RTD40
```
