## Deployment Scripts

This is a repo to store deployment scripts I use. Traefik acts as a reverse proxy for all services and other containers are connected through docker network `traefik`


### To spin up traefik:
```
docker compose -f traefik.yaml up -d
```

### For everything else:
```
docker compose -f <compose-file>.yaml up  -d
```

### Note

If you've changed stuff after deploying a container, add arguments to docker as needed when re-deploying

```
--force-recreate --build
```
