## Traefik reverse proxy

- Read [documentation](https://docs.traefik.io/)

### Build local image

```
export $(cat .env)
docker build -t ${TRAEFIK_SERVICE}:${TRAEFIK_SERVICE__VERSION} .
```

# Deploy stack

```sh
docker stack deploy -c docker-compose.swarm.yml traefik
```
