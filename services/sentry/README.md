## Sentry

> Open-source error tracking that helps developers monitor and fix crashes in real time.

- docker-compose.swarm.yml based off this [repo](https://github.com/getsentry/onpremise)

- Official [website](https://sentry.io)

- Read [documentation](https://docs.sentry.io/server/)

### Creating admin user

To create initial admin user use this command on running `web` container

```
docker exec -it 02edfb170093 ./entrypoint.sh createuser
```

### Upgrading database

To perform migrations use this command on running `web` container

```
docker exec -it 02edfb170093 ./entrypoint.sh upgrade
```
