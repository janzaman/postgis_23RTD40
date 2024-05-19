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
### Vector data Natuur

using postgis Shapefile Import/Export manager tool

Connecting:  host=localhost port=5432 user=postgres password='********' dbname=23RTD40 client_encoding=UTF8
Connection succeeded.

```
Importing with configuration: bwk_habitat, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Natuur\Bwk_Habitat.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: habitatrichtlijngebieden, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Natuur\Habitatrichtlijngebieden.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: hb_vegbesl, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Natuur\hb_vegbesl.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.
```
probleem met de laag ps_ven 'illegal byte sequence', eerst in QGIS exporteren naar 31370 en UTF-8 encoding => ps_ven2.shp

```
Importing with configuration: ps_ven2, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Natuur\ps_ven2.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.
```

### Vector data Erfgoed

```
Importing with configuration: bes_arch_site, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Erfgoed\bes_arch_site.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: bes_landschap, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Erfgoed\bes_landschap.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: bes_sd_gezicht, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Erfgoed\bes_sd_gezicht.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: erfgoedls, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Erfgoed\erfgoedls.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: landschappelijk_elementen, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Erfgoed\landschappelijk_elementen.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: landschappelijk_gehelen, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Erfgoed\landschappelijk_gehelen.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: unesco_buffer, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Erfgoed\unesco_buffer.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: unesco_kern, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Erfgoed\unesco_kern.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: vast_la, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Erfgoed\vast_la.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.
```

### Vector data bodem

```
Importing with configuration: bodemkundig_erfgoed, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Bodem\Bodemkundig_erfgoed.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: gevoeligheid_voor_grondverschuivingen, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Bodem\gevoeligheid_voor_grondverschuivingen.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.
```

### Vector data Landbouw

```
==============================
Importing with configuration: lis_uirarc_10m_aaneengesloten_10haofmeer, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Landbouw\lis_uirarc_10m_aaneengesloten_10haofmeer.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.

==============================
Importing with configuration: listot_uitarcgis, public, geom, C:\Users\janza\Documents\02_gis\23RTD40\Shapefiles\Bronnen\Landbouw\Listot_uitArcGis.shp, mode=c, dump=1, simple=0, geography=0, index=1, shape=1, srid=31370
Shapefile type: Polygon
PostGIS type: MULTIPOLYGON[2]
Shapefile import completed.
```

### Raster data
voorzieningenniveau: eerst selectie van de slecht gelegen categorieën, gebaseerd op een indeling van de waarden in vier klassen volgens Jencks Natural Breaks, dan omzetten in een 1 bit raster
```
C:\> raster2pgsql -s 31370 -I -C -M C:\Users\janza\Documents\02_gis\23RTD40\Rasters\Ontwikkelingskansen2022\voorzieningsniveau_2022_natural_breaks_25_Slecht.tif -F -t 25x25 public.voorzieningenslecht | psql -U postgres -d 23RTD40
```
knooppuntwaarde: eerst selectie van de slecht gelegen categorieën, gebaseerd op een indeling van de waarden in vier klassen volgens Jencks Natural Breaks, dan omzetten in een 1 bit raster
```
C:\> raster2pgsql -s 31370 -I -C -M C:\Users\janza\Documents\02_gis\23RTD40\Rasters\Ontwikkelingskansen2022\knooppuntwaarde_OV_2022_natural_breaks_25_Slecht.tif -F -t 25x25 public.knooppuntwaardeslecht | psql -U postgres -d 23RTD40
```
pluviaal overstromingsgevoelig toekomstig klimaat klein risico (t1000) 
```
C:\> raster2pgsql -s 31370 -I -C -M C:\Users\janza\Documents\02_gis\23RTD40\Rasters\Water_Overstroombaargebied\waterdiepte_PLU_hCC_T10_Groterdan0.tif -F -t 2x2 public.plu_hcc_t10 | psql -U postgres -d 23RTD40
```


