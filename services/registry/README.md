## Docker Registry

- Read [documentation](https://docs.docker.com/registry/)

### Setup basic authorization

```
docker run --entrypoint htpasswd registry:2 -Bbn example *********
```

You are need to add string from stdout to `traefik.frontend.auth.basic` line in `docker-compose.swarm.yml` file.

**IMPORTANT**: You should to escape a sign `$` from the string with `$$` in `docker-compose.swarm.yml` file.

### Deploy

```sh
docker stack deploy -c docker-compose.swarm.yml registry
```
