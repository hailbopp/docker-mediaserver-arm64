# Dockerized ARM-based Home Media Server

## Setup
In `docker-compose.yml`, change the `PUID` and `PGID` lines to your user ID.
Then, `docker-compose up -d`.

## Services
* Plex : localhost:32400/web
* Sonarr : localhost:8989
* SABnzbd : localhost:8080
