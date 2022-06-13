# Mariadb

### 1. install Mariadb

&#x20;a) install db by:

```
docker run -d -p 3306:3306 --name mariadb --env MARIADB_USER=admin --env MARIADB_PASSWORD=P@ssw0rd --env MARIADB_ROOT_PASSWORD=P@ssw0rd  mariadb:latest

```



b) gainting access to remote server

show id of container

```bash
docker container ls

f23acdfc9109   mariadb:latest                  "docker-entrypoint.s…"   15 minutes ago   Up 15 minutes   0.0.0.0:3306->3306/tcp                                     mariadb
```

access container:

```bash
docker exec -it f23acdfc9109 bash
```

access mysql:

```bash
mysql -u root -p
```

then, enter the password

```
CREATE USER  'admin'@'localhost' IDENTIFIED BY 'P@ssw0rd';
```



```
GRANT ALL ON *.* to 'admin'@'%' IDENTIFIED BY 'P@ssw0rd' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```





### 2. install phpmyadmin



```bash
docker run --name myadmin -d -e PMA_ARBITRARY=1 -p 33061:80 phpmyadmin

```





### 3. access DB



In Portainer we can see:

![](<../.gitbook/assets/image (4).png>)

So in phpmyadmin:

![](<../.gitbook/assets/image (6).png>)



The ip should be the container inside ip.
