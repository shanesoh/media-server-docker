# Docker-based Home Media Server with Emby, Sonarr, Radarr, Jackett, Transmission and Caddy

Runs a suite of services for a full-fledged home media server using Compose. Can optionally be used with Caddy for HTTPS.

Uses a bunch of a community-built Docker images that I've personally tried and tested and found to work great together.

## Getting Started

### Create a `.env` file
Define a `.env` file with the following environment variables:
- `TZ`: Time zone (eg "Asia/Singapore") as per [this list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
- `PUID` and `PGID`: Linux user and group IDs. Find yours using `id`.
- `USERDIR`: Directory path to contain all media and config files used by these services

An example of a `.env` file is as follows:
```
TZ="Asia/Singapore"
PUID=1000
PGID=1000
USERDIR=/home/user/media-server-docker
```

### Start Compose services
Simply start all the services with 
```
docker-compose up
```
which uses the `docker-compose.yml` by default.

### Enable SSL with Duck DNS and Caddy
Get a dynamic DNS domain at [Duck DNS](https://www.duckdns.org). Then configure the `caddy/Caddyfile` file by changing the domain name to whatever you picked.

Finally, start the services by including the `caddy.yml` file
```
docker-compose -f caddy.yml -f docker-compose.yml up
```
