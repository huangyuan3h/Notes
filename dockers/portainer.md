# Portainer

#### Create the volume that Portainer Server will use to store its database:

```bash
docker volume create portainer_data
```

#### Download and install the Portainer Server container:

```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
```



#### Login to the portainer:

```
https://localhost:9443
```

