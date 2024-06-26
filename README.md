# ARK: Survival Ascended Docker Server

Ark server in a docker container using GloriousEggroll's custom [proton build](https://github.com/GloriousEggroll/proton-ge-custom)

1) Install [docker](https://docs.docker.com/engine/install/)
2) Copy `.env.example` to `.env` and [configure](#environment-variables)
3) Run `docker compose up --build`

Server files are mounted in the `ark-data` docker volume `/var/lib/docker/volumes/ark-data/_data/ShooterGame/`

## Configuration

Custom [server settings](https://ark.fandom.com/wiki/Server_configuration#GameUserSettings.ini) `/ShooterGame/Saved/Config/WindowsServer/GameUserSettings.ini`

### Environment Variables

Settings in `.env`

| Variable         | Default | Description
| ---              | ---     | ---
| `MAP_NAME`       | TheIsland_WP | The name of the map to load (e.g. `TheIsland_WP` or `ScorchedEarth_WP`)
| `SESSION_NAME`   | | Name of the server
| `ADMIN_PASSWORD` | | Server [administrator](https://ark.fandom.com/wiki/Console_commands#EnableCheats) password
| `MAX_PLAYERS`    | `20`    | Player slots (Max `70`)
| `GAME_PORT`      | `7777`  | UDP port
| `MODS`     | | Comma-separated list of [CurseForge](https://www.curseforge.com/ark-survival-ascended) mod IDs to install (e.g. `928501,928728`)
| `CMD_ARGS` | | Additional [command line arguments](https://ark.fandom.com/wiki/Server_configuration#Command_line_arguments) (e.g. `"-ForceAllowCaveFlyers -NotifyAdminCommandsInChat"`)

## Docker

The docker image builds off the offical `steamcmd/steamcmd:latest` base image

Running `docker compose build` builds the image locally and tags it as `ark-server`

Alternatively you can use a [pre-built image](https://hub.docker.com/r/chandywerks/ark-server) on docker hub `chandywerks/ark-server:latest`

```yml
version: '3'
services:
  ark-server:
    restart: unless-stopped
    image: chandywerks/ark-server:latest
    container_name: ark-server
    environment:
       ...
```
