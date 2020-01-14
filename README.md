## Dockerized Development Environment - Windows VirtualBox + Boot2Docker

```
$ docker build -t signage/server -f Dockerfile.server .
$ docker build -t signage/websocket -f Dockerfile.websocket_server .
$ docker build -t signage/viewer -f Dockerfile.viewer .
	
$ docker run --rm -ti --name=digital-signage-server -e 'LISTEN=0.0.0.0' -p 8080:8080  signage/server
$ docker run --rm -ti --name=digital-signage-websocket -e 'LISTEN=0.0.0.0' -p 9999:9999  signage/websocket
$ docker run --rm -ti --name=digital-signage-viewer -e DISPLAY=192.168.1.9:0.0 -e 'LISTEN=192.168.1.9' signage/viewer

$ docker run --name=digital-signage-server -e 'LISTEN=0.0.0.0' -p 8080:8080 signage/server
$ docker logs --tail 100 digital-signage-server


$ docker run --name=digital-signage-websocket -e 'LISTEN=0.0.0.0' -p 9999:9999 signage/websocket
$ docker logs --tail 100 digital-signage-websocket


$ docker run --name=digital-signage-viewer -e DISPLAY=192.168.1.9:0.0 -e 'LISTEN=192.168.1.9'  signage/viewer
$ docker logs --tail 100 digital-signage-viewer


$ docker exec -it <container name> /bin/bash
$ docker rm -f $(docker ps -aq)
$ docker rmi <image>


```
#### Notes

* In VirtualBox - do port-mapping for below ports 8080 and 9999 with host as 0.0.0.0 (all network interfaces)

* Separate docker for viewer having issue with DB, since viewer is trying to use the same db which was created by server.     OperationalError: no such table: assets

    - Solution : Single Dockerfile with all 3 components would work :)

