## DevOps multi-repository

This is a repository concept for managing all services.
Git submodules are **only used for updates** (pull-mode like as [Repo](https://gerrit.googlesource.com/git-repo/)).

### Requirements

#### For localhost

```sh
sudo pip install -r requirements.txt
```

#### For remote server(s)

```sh
sudo pip install -r requirements.swarm.txt
```

### Deployment

The deployment will be produced with the bash script name of [deploy](./deploy).
This script is a wrapper for [ansible playbook](./ansible/playbook/deploy.yml) with same name.

![Deploy on swarm](https://i.imgur.com/GpiyprY.gif)

#### Deploy an application stack

Every service will be deployed separately with same the stack name. You can see all stacks in [services folder](./services).
You can see all environments in [ansible environments folder](./ansible/environments).

```sh
./deploy $STACK $ENV
```
