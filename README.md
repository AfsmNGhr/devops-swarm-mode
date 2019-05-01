## DevOps multi-repository

One repository to rule all.

### Deployment

The deployment will be produced with the bash script name of [deploy](./deploy).
This script is wrapper the ansible [playbook](./ansible/playbook/deploy.yml) with same name.

#### Requirements on localhost:

You must [install ansible](http://docs.ansible.com/ansible/intro_installation.html).

```sh
sudo pip install ansible==2.7.5
```

Also you need to create `.vault` file with password for [ansible-vault](https://docs.ansible.com/ansible/2.4/ansible-vault.html).

#### Deploy the application stack:

The `deploy` script takes two arguments. The first argument is the application stack.
Every service will be deployed separately with same the stack name. You can see all stacks in [the services folder](./services).
The second arguments is environment. You can see all environments in [the ansible environments folder](./ansible/environments).
You will must type in vault password if don't create `.vault` file.

```sh
./deploy example staging
```

#### How to add a new application stack:

You must create in service's folder your new stack folder. [See more what to do next](./services#structure).

#### Removing the application stack:

Change stack name and run the command below to remove an unnecessary stack. [More read](https://docs.docker.com/engine/reference/commandline/stack_rm/).

```sh
ansible -i ansible/environments/staging staging -m shell -a 'docker stack rm example' --vault-password-file=.vault
```

**INFO:** Deleting a stack does not remove volumes. [More read](https://docs.docker.com/engine/reference/commandline/volume_rm/).

```sh
ansible -i ansible/environments/staging staging -m shell -a 'docker volume rm example_*' --vault-password-file=.vault
```

**IMPORTANT:** You can't remove volume if `volume is in use - [5a665dc1dcfc52d6b87cd7cd2440832f23519b71c673d1a7106a134467034603]`
<br>
**DANGEROUS:** Add a flag `-f` for above the command if you are sure and exactly want to remove volumes.

#### Running manual command:

```sh
ansible -i ansible/environments/staging staging -m shell -a 'docker stack ls' --vault-password-file=.vault
```
