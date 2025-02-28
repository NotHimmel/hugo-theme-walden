+++
title = 'Linux应用软件-Docker'
date = 2025-02-28T17:00:00+08:00
draft = false
weight = 2
+++

<!--more-->
syncthing
```
docker run -d \
  --name=syncthing \
  --hostname=syncthing `#optional` \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -p 8384:8384 \
  -p 22000:22000/tcp \
  -p 22000:22000/udp \
  -p 21027:21027/udp \
  -v /home/taozheng/docker/syncthing/config:/config \
  -v /home/taozheng/docker/syncthing/data1:/data1 \
  -v /home/taozheng/docker/syncthing/data2:/data2 \
  --restart unless-stopped \
  lscr.io/linuxserver/syncthing:latest

/root/docker/syncthing
```

readeck
```
docker run --rm -ti -p 8000:8000 \
    -v readeck-data:/readeck \
    -v $(pwd)/readeck-backup:/backup \  # Mount the backup directory
    codeberg.org/readeck/readeck:latest
```