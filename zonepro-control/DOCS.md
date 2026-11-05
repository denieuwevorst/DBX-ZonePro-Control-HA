# ZonePRO Control

Bediening van een dbx ZonePRO (volume, mute, bron per zone).

## Gebruik

1. Start de add-on. Open **ZonePRO** in de zijbalk (ingress), of ga naar `http://<ha-ip>:3001` voor de losse website.
2. Vul het ZonePRO-IP en de object-ID's van je zones in, via `/config` in de webpagina of door `config.json` te bewerken (zie hieronder).
3. Op `/ha-dashboard` genereer je de Lovelace-YAML voor een dashboard.

## Configuratiebestand (`config.json`)

Staat in de add-on config-map en is dus bewerkbaar met de **File editor**, **Studio Code Server**, Samba of SSH:

`/addon_configs/<xxxxxxxx>_zonepro_control/config.json`

(de exacte mapnaam zie je in de File editor onder `addon_configs`). Wijzigingen worden binnen ~2 seconden automatisch ingelezen, ook MQTT en het ZonePRO-IP; een herstart is niet nodig. Is het bestand ongeldig (JSON-fout, verplicht veld weg), dan staat de fout in het add-on logboek en blijft de laatste goede configuratie actief. Opslaan via `/config` in de webpagina werkt ook, met automatische backups (laatste 30, in `/data/backups`).

## MQTT

De zones verschijnen via MQTT discovery als apparaten in Home Assistant. De broker wordt in deze volgorde bepaald:

1. `mqtt.host` in `config.json`, indien ingevuld.
2. De add-on opties **mqtt_host / mqtt_port / mqtt_username / mqtt_password** (tabblad Configuratie), bijvoorbeeld voor een externe broker. Herstart de add-on na wijzigen.
3. Automatisch de broker van de **Mosquitto broker** add-on (met MQTT-integratie), als je niets invult.

Bij de allereerste start wordt `mqtt.enabled` automatisch op `true` gezet als er een broker bekend is. Staat `enabled` in een bestaande `config.json` op `false`, dan blijft MQTT uit.

## Opslag

`config.json` staat in de add-on config-map, `state.json` en `backups/` in `/data`. Beide blijven bewaard bij updates en zitten in je Home Assistant-backups.
