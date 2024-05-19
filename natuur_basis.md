# Maak basislaag Natuur

```
drop table if exists aa_natuur_basis_slecht;
create table aa_natuur_basis_slecht as 
select public.habitatrichtlijngebieden.geom
from public.habitatrichtlijngebieden
union
select public.ps_ven2.geom
from public.ps_ven2
union 
select public.hb_vegbesl.geom
from public.hb_vegbesl 
where statuut = 'verbod';
drop table if exists aa_natuur_slecht;
create table aa_natuur_slecht as
select st_union(public.aa_natuur_basis_slecht.geom) as geom
from public.aa_natuur_basis_slecht;
drop table public.aa_natuur_basis_slecht;
drop table if exists aa_natuur_matig01;
create table aa_natuur_matig01 as 
select public.habitatrichtlijngebieden.geom
from public.habitatrichtlijngebieden
union 
select public.ps_ven2.geom
from public.ps_ven2;
drop table if exists aa_natuur_matig02;
create table aa_natuur_matig02 as 
select st_union(aa_natuur_matig01.geom) as geom
from aa_natuur_matig01;
drop table if exists aa_natuur_matig03;
create table aa_natuur_matig03 as 
select ST_Buffer(aa_natuur_matig02.geom, 200) as geom
from aa_natuur_matig02;

```
