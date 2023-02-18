# Jellyfin/Starr Apps Media Server for Docker

![Jellyfin](https://i.imgur.com/BCfda0J.png)
## Description

This repository provides a beginner-friendly ready-to-use template following the guidelines defined by [TRaSH Guides](trash-guides.info). All credit goes to the people maintaining the [project](https://github.com/TRaSH-/Guides). If you enjoy their work, [go buy them a cup of coffee](https://github.com/sponsors/TRaSH-)!

I've created this repository to help anyone looking for a quick start in configuring their own media server solution and to version control my personal setup.

I'm making use of **Jellyfin** for media streaming as it is open-source and pretty much ubiquitous in app stores. For downloading torrents, I'm using **qBittorrent**'s official Docker image. And for managing and choosing what I want to watch in an user-friendly UI, I'm using the **Starr apps**. Here is a quick breakdown of what each service in this stack does:

* [Jellyfin](https://jellyfin.org/): Make your media into a nice library and stream it to your devices where you want to watch them. The client can be found in most app stores and works on browsers.
* [Radarr](https://radarr.video/): Monitor and grab movies you want to add to your collection, which it then sends to your torrent client
* [Sonarr](https://sonarr.tv/): Monitor and grab TV shows you want to add to your collection, which it then sends to your torrent client
* [Bazarr](https://www.bazarr.media/): Monitor and grab subtitles for the TV Shows and Movies in your Sonarr/Radarr
* [Prowlarr](https://github.com/Prowlarr/Prowlarr): Group all the torrent trackers you want to use in one place, which it is then able to pass on to Radarr and Sonarr
* [Recyclarr](https://github.com/recyclarr/recyclarr): Gets updates for the release profiles defined in TRaSH Guides so that Sonarr/Radarr can choose the best torrent releases and avoid the bad ones
* [qBittorrent](https://www.qbittorrent.org/): Downloading torrents obtained from Sonarr/Radarr
* [Gluetun](https://github.com/qdm12/gluetun): Routing the traffic from your Docker containers through a VPN (OPTIONAL)

## Getting Started

### Dependencies

* A Linux server with [Docker Compose](https://docs.docker.com/compose/install/) installed.

### Installing

* Begin by creating the directories (preferrably with the same names) and granting them the correct permissions using the chown/chmod commands found [here](https://trash-guides.info/Hardlinks/How-to-setup-for/Docker/).
* Clone this repository on your server.
* In case you don't need to have your traffic routed through a VPN, read [this section](###without-a-vpn) on how you can omit it from the configuration.
* Navigate to the repository's folder on a terminal and run `docker compose up -d` to have Docker create all the containers in this stack.
* You should now be able to navigate to each of your containers on your browser after they are up on `http://server-ip:port` to continue setting them up. Follow the instructions [here](https://trash-guides.info/Hardlinks/Examples/) for Radarr, Sonarr and qBittorrent.

That's essentially it for the installation. You will now have to set up each service and make them communicate with one another on their settings. I highly encourage you to read up the sections on Sonarr and Radarr on Trash Guides for their recommended configurations, which will save you time on debugging in the future. You can also copy my [recyclarr.yml](./recyclarr.yml) to /docker/appdata/recyclarr (if using the same directories as me), which contains the updated profiles I get from Trash Guides to consistently get good quality 1080p files for movies, TV shows and animes that will direct play on most clients and reduce the transcoding load on your server. Doing that will import these profiles into your Sonarr/Radarr, and from there you can assign them to the 1080p quality (more details on the Sonarr and Radarr sections on Trash Guides).

### Without a VPN

If forgoing the use of a VPN, simply edit the [docker-compose.yml](./docker-compose.yml) to remove or comment out the Gluetun service from it. You will also have to transfer all the ports which were assigned for Gluetun and place them into their respective services. E.g.: Radarr will need to have a section for ports mapping ports 7878:7878. You can find an example of a docker-compose done this way [here](https://trash-guides.info/Hardlinks/How-to-setup-for/Docker/)

## Help

The apps being used in this repository are very known and you should not have a hard time finding tutorials on youtube or finding answers on Reddit for most issues you may come across. There are also active Discord servers for each of the services listed [as well for TRaSH Guides itself](https://trash-guides.info/discord). 