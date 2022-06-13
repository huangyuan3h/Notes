# Dockers



### Clean up

#### Delete all docker containers

```bash
docker rm -f $(docker ps -a -q)
```

#### Delete all volumes

```bash
docker volume rm $(docker volume ls -q)
```







