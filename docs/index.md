# Docker Bungee Server

Prelaunch settings are held in the `docker-compose.yml` file, and will be automatically executed when the container is launched. Other settings can be adjusted by manually going into i.e. a `server.properties` file and changing a value, or by adding it to the environment variable. All adjustments should stay upon a server restart unless it is overridden by `docker-compose.yml`.

If you wish to add more worlds/servers to your [BungeeCord](https://www.spigotmc.org/wiki/bungeecord/) server, simply copy/paste the following code into `docker-compose.yml` and `data/bungeecord/config.yml`, and adjust it according to your needs.

```yaml
# DOCKER-COMPOSE.YML
<docker service name>: # set this to i.e. "mc-<gamemode/theme>_<version>" to easily locate it for maintenance
    image: itzg/minecraft-server
    container_name: <container name> # set this to be the same as the service name
    ports:
      - "25566:25565" # first port is adjustable, second port must be the same as the internal server port
    environment:
      EULA: "TRUE" # must be set to true
      ONLINE_MODE: "FALSE"
      MOTD: "<motd>"
      LEVEL: <level name> # name of the world folder
      TYPE: <server_type> # i.e. PAPER, SPIGOT, etc
      VERSION: <version> # i.e. 1.17.1, 1.16.5, etc
      MEMORY: <amount>G # i.e. 1G, 2G, 4G, etc
      MODRINTH_PROJECTS: | # or CURSEFORGE_FILES # see the PROJECTS.md file for more information about this
        <project>
      RCON_CMDS_STARTUP:  |-
        op <your_username>
    volumes:
      - ./data/<container name>:/data # makes sure the data is saved locally
    restart: unless-stopped # restart the container if it crashes
```

```yaml
# DATA/BUNGEECORD/CONFIG.YML
<server name>: # This is the name that the "/server <server name>" command is going to use - can differ from service name
    motd: '<motd>'
    address: host.docker.internal:<port> # set the port to the same one you used in the docker-compose file
    restricted: false
```


You can find information about installing mods/plugins for your worlds/servers in the [[docs/plugins-and-mods/index|Plugins and Mods]] document.