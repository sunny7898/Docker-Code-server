# Docker-Code-server

This project can be run in two ways :
1. Using directly the docker command :
docker create \
  --name=code-server \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Asia/Kolkata \
  -e PASSWORD=password `#optional` \
  -p 8443:8443 \
  -v /path/to/appdata/config:/config \
  --restart always \
  linuxserver/code-server
  
2. Using docker-compose  :
version: "2.1"
services:
  code-server:
    image: linuxserver/code-server
    container_name: code-server
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Kolkata
      - PASSWORD=password #optional
    
    volumes:
      - /path/to/appdata/config:/config
    ports:
      - 8443:8443
    restart: always
    
    
Parameters : 
-p 8443	web gui
-e PUID=1000	for UserID 
-e PGID=1000	for GroupID 
-e TZ=Asia/Kolkata	Specify a timezone to use Asia/Kolkata
-e PASSWORD=password	Optional web gui password, if not provided, there will be no auth.
-v /config	Contains all relevant configuration files.

When using volumes (-v flags) permissions issues can arise between the host OS and the container, we avoid this issue by specifying the user PUID and group PGID.
Ensure any volume directories on the host are owned by the same user you specify.

In this Projetc PUID=1000 and PGID=1000, 
to find yours Command : id username
