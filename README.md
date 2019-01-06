# SteamCMD for Docker
A Ubuntu based image for SteamCMD.

## Usage:
```bash
docker run --rm -it -v "/data/steam/csgo_ds:/steam/csgo_ds" -e "STEAM_ARGS=+login anonymous +force_install_dir ../csgo_ds +app_update 740 validate +quit" dekart811/steamcmd:latest
```
This will download a dedicated server for CS:GO.
