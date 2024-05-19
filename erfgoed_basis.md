# Maak Erfgoed basislaag

aan de hand van de basislagen uit de opbouw van de database maken we de basislaag erfgoed

```
drop table if exists erfgoed_basis_slecht;
create table erfgoed_basis_slecht as 
select public.bes_arch_site.geom
from public.bes_arch_site
union
select public.bes_landschap.geom
from public.bes_landschap
union 
select public.bes_sd_gezicht.geom
from public.bes_sd_gezicht
union
select public.erfgoedls.geom
from public.erfgoedls
union
select public.landschappelijk_elementen.geom
from public.landschappelijk_elementen
union
select public.landschappelijk_gehelen.geom
from public.landschappelijk_gehelen
union 
select public.unesco_buffer.geom
from public.unesco_buffer
union
select public.unesco_kern.geom
from public.unesco_kern
union 
select public.vast_la.geom
from public.vast_la;
drop table if exists aa_erfgoed_slecht;
create table aa_erfgoed_slecht as
select st_union(public.erfgoed_basis_slecht.geom) as geom
from public.erfgoed_basis_slecht;
drop table public.erfgoed_basis_slecht;
```