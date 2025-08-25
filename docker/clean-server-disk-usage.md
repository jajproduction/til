# Clean Server Disk Usage

```sh
ssh root@your-server-ip
df -h
```

```sh
docker system prune -af
docker volume prune -f
docker image prune -af
docker builder prune -af
docker system df
df -h
```
