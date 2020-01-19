## DevOps & Swarm-mode

[![Build Status](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Factions-badge.atrox.dev%2FAfsmNGhr%2Fdevops-swarm-mode%2Fbadge&style=flat)](https://actions-badge.atrox.dev/AfsmNGhr/devops-swarm-mode/goto)

The repository concept for managing all services as code (IaC).
Git submodules **use for updates only** (pull-mode like as [Repo](https://gerrit.googlesource.com/git-repo/)).

### Deployment

![Deploy on swarm](https://i.imgur.com/GpiyprY.gif)

Every service will be deployed separately with same the stack name. You can see all stacks in [services folder](./services).
You can see all environments in [ansible environments folder](./ansible/environments).

```sh
./deploy "$STACK" "$ENV" # optionally "$GROUP"
```
