## Services Folder

This folder have to contains all services.
A service folder can be contains subfolders if they are depends on service.

### Structure

Every a service folder should contains `docker-compose.swarm.yml` file.
Also you can be add `docker-compose.$env.yml`, `Dockerfile` and `.env`, if it's necessary.
You must create `.dockerignore` file with `.env`, `*.md` and `*.yml` that they mustn't in the context of the build if you are need to built custom the docker image.

#### Required sections for swarm configuration

##### Networking

For domain notation use only service name.

##### Statefull

For statefull service you must create volume.

```yml
version: '3.4'
services:
  pg:
    image: postgres:10.6-alpine
    volumes:
      - pg_data:/var/lib/postgresql/data/pg_data
volumes:
  pg_data:
```

##### Web Application

For web application, configure a check that a service is "healthy". [More learn](https://docs.docker.com/compose/compose-file/#healthcheck).

```yml
version: '3.4'
services:
  example:
    healthcheck:
      test: 'nc -z localhost 8000 > /dev/null 2>&1 || exit 1'
```

##### Enable Traefik

Need to add external network with name of `traefik_proxy` and below labels for routing.

```yml
version: '3.4'
services:
  example:
    ports:
      - 8000
    networks:
      - traefik_proxy
    deploy:
      labels:
        traefik.enable: 'true'
        traefik.backend: example
        traefik.frontend.rule: 'Host: example.com'
        traefik.port: '8000'
networks:
  traefik_proxy:
    external: true
```

For advanced routing [see matchers](https://docs.traefik.io/basics/#matchers).

##### Load-balancing with Traefik

Dynamic Round Robin: increases weights on servers that perform better than others. It also rolls back to original weights if the servers have changed. [More about load-balancing](https://docs.traefik.io/basics/#load-balancing).

```yml
version: '3.4'
services:
  example:
    deploy:
      labels:
        traefik.backend.loadbalancer.method: drr
```

##### Force ssl redirect

```yml
version: '3.4'
services:
  example:
    deploy:
      labels:
        traefik.frontend.headers.SSLRedirect: 'true'
```

Also, see [custom headers](https://docs.traefik.io/basics/#custom-headers).

##### Migration's containers

For containers of `*__migrator`, which run migrations. You must use utility of `wait-for` to wait connection with database.
Container mustn't start after fail. [More about startup order](https://docs.docker.com/compose/startup-order/).

```yml
example__migrator:
  command: sh -c './wait-for pg:5432 -- python manage.py migrate'
  deploy:
    mode: replicated
    restart_policy:
      condition: none
```

### Deployment

Every a service have to deploy separately by docker stack via [Ansible](../README.md#deploy-the-application-stack).

### Learn more

Learn more about specific service in service folder.
