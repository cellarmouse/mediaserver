# mediaserver
## Media Server Setup

## Operating System
Install whatever Linux operating system of your choice. I like Ubuntu or Debian, whatever floats your boat.

If you install ubuntu, I would recommend not using the snap package that comes with it, instead install using docker instructions: https://docs.docker.com/engine/install/ubuntu/

### Storage
This is dependent data paths existing in /data/docker/VOLUMES
The following are "needed":
* appdata - stores application configuration
* media - where media is stored
* media/TV - where Sonarr downloads go to
* media/Movies - where Radarr downloads go to
* media/downloads - where incoming stuff goes

### Scripts
I have a script that runs that unrars .rar downloads, not really common anymore. This is based on the script from here: https://github.com/arfoll/unrarall

I save it as /usr/local/bin/unrarall

Cront runs every 5 minutes:
*/5 * * * * echo `date` >> /root/unrar.log && /usr/local/bin/unrarall --disable-cksfv  --skip-if-exists /data/docker/VOLUMES/media/downloads/completed >> /root/unrar.log

## Docker
the docker-compose.yml file describes the whole stack.

Before setting this up, I usually set up portainer to make life a bit simpler, but it's not a requirement.

## Application Configuration
Some apps need to talk to each other. For example, Sonarr can talk to Jellyfin to tell it to rescan a library once a download is complete. You *should* be able to point it to the container name identified in the docker-compose file.  (e.g. "jellyfin:8096")

Other than that, it's a matter of following the configuration examples from each application at their respective sites.
