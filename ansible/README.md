OpenMRS Infrastructure Ansible Master Playbook
======================
Master playbook that should be run on all servers.

## Roles currently configured
* server-common

## Requirements
* This repo.
* ansible  1.5+ installed on the same machine the repo is cloned to.

## How to use this
To run this on a set of machines , currently (production, staging, testing).

`ansible-playbook -i testing site.yml`

This will run all roles against the inventory you specified. This will also assume you want to log into the server using your current user. use the `-u` switch to specify another user. The use of `--sudo` will use sudo when needed as well.

If you want to run a specific task/role on a set of machines.

`ansible-playbook -i testing server-common.yml`

Look into each role in the roles directroy to find out what each role does.

## Running example ad-hoc commands
#### Updating all packages on staging servers

`ansible -i staging all -m apt -a "update_cache=yes upgrade=yes" --sudo` 

You may also want to add `--check` to do a dry run before to make sure you really want to upgrade the intended packages.

#### Update a ceratin package to latest version on production

`ansible -i production all -m apt -a "update_cache=yes name=openssl state=latest" --sudo`

This will only update the package to the latest version if it is already installed.  It will not install the openssl package on hosts that do not have it installed.
