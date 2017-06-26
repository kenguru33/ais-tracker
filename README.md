# Ais-Tracker

## Prosjektbekrivelse

### Oppsummert
Laster ais data fra json "feeds" og lagrer dem. Spørringer kan kjøres via webapi.

systemskisse her

---

### Utviklingsoppsett

Prosjektet er satt sammen med et hovedprosjekt hvor de forskjellige microservice'ene tas inn som git submodules

Git submodulene er satt til å følge master branch:

git submodule add -b master \<repo\>



#### Hoved git repo: ais-tracker
Docker-Compose oppsett:
- docker-compose.yml - base
- docker-compose.override.yml - dev
- docker-compose.prod.yml - prod

Submodules:
- ais-data-fetcher (fetches ais json data)
- ais-Data-collector (stores ais data)
- ais-data-webapi (query api)
- ais-data-domain (common core domain)

#### Start av utviklingsmiljø:

Bygg images:

docker-compose build


deploy utviklingsmiljø:

docker-compose

Detter starter opp følgende service'er:
- fetcher
- collector
- mongodb
- message queue (rabbitmq)
- webapi
- nginx (load balancer)

Kildekoden er monter på volume: ./src:/app/src


restart av miljøet:

docker-compose restart


#### Sett i produksjon

docker-compose -f docker-compose.yml -f docker-compose.prod.yml

Dette deployer koden i en docker swarm




