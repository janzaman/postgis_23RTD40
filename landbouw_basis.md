# Maak landbouw basislaag

Vertrekkend van de vectordata ingevoegd in de database.
```
drop table if exists aa_landbouw_basis;
create table aa_landbouw_basis as 
select public.lis_uirarc_10m_aaneengesloten_10haofmeer.geom
from public.lis_uirarc_10m_aaneengesloten_10haofmeer
union
select public.listot_uitarcgis.geom
from public.listot_uitarcgis;
```
Blijkbaar zit er een topologiefout in het resulterende bestand.
We lossen dit op door een buffer van 0 meter te tekenen die wel geometrisch correct is.
```
drop table if exists aa_landbouw_01;
create table aa_landbouw_01 as 
select ST_Buffer(public.aa_landbouw_basis.geom, 0) as geom
from public.aa_landbouw_basis;
drop table if exists aa_landbouw_slecht;
create table aa_landbouw_slecht as
select st_union(public.aa_landbouw_01.geom) as geom
from public.aa_landbouw_01;
drop table public.aa_landbouw_basis;
drop table public.aa_landbouw_01;
```
