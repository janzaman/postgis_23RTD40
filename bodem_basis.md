# Maak basislagen Bodem

Vertrekkend van de opgeladen vectorgegevens voor Bodem.

```
drop table if exists aa_bodem_slecht;
create table aa_bodem_slecht as
select public.gevoeligheid_voor_grondverschuivingen.geom
from public.gevoeligheid_voor_grondverschuivingen
where gevoelighd = 'hoge gevoeligheid' or gevoelighd = 'zeer hoge gevoeligheid';

drop table if exists aa_bodem_matig;
create table aa_bodem_matig as
select public.bodemkundig_erfgoed.geom
from public.bodemkundig_erfgoed;
```
