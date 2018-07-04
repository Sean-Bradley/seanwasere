# Delete all docker containers and images

if you need sudo permissions?

```
sudo docker rm -f $(sudo docker ps -a -q)

sudo docker rmi -f $(sudo docker images -q)
```

if not (you are probably using mingw64) then

```
docker rm -f $(docker ps -a -q)

docker rmi -f $(docker images -q)
```
