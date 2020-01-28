# ansible-role-docker-nextcloud

This role runs nextcloud with [Let's Encrypt](https://letsencrypt.org/) behind a traefik reverse proxy. It is intended to work with [ansible-role-docker-traefik](https://github.com/mambord/ansible-role-docker-traefik).

If there is no nextcloud installation present, nextcloud will be downloaded by this role. Actually, the first installation steps have to be done manually. If there is already nextcloud installed, ansible won't touch anything.

## Defaults

These are the default values for this playbook.

```yaml
---

#
# traefik settings
#

docker_nextcloud_traefik_network: 'traefik'

#
# base settings
#

docker_nextcloud_url: cloud.home.local

#
# collabora (see: https://www.collaboraoffice.com/code/docker/)
#

docker_nextcloud_url_escaped: cloud\\.home\\.local
docker_nextcloud_collabora_url: office.home.local
docker_nextcloud_collabora_user: admin
docker_nextcloud_collabora_password: p4Ssw0rd!
# Can be 0-8, or none (turns off logging), fatal, critical, error, warning, notice, information, debug, trace
docker_nextcloud_collabora_loglevel: warning

#
# nextcloud
#

docker_nextcloud_version: '17.0.1'
docker_nextcloud_language: 'de'
docker_nextcloud_locale: 'de_CH'
docker_nextcloud_logtimezone: 'Europe/Zurich'
docker_nextcloud_maintenance_mode: no
docker_nextcloud__integrity_check_disabled: no

#
# database
#

docker_nextcloud_database_password_nextcloud: 'nextcloud-db-password'
docker_nextcloud_database_password_root: 'root-db-password'

#
# php
#

docker_nextcloud_php_version: '7.2'

#
# docker-compose
#

# always pull images
docker_nextcloud_pull: no

# stop all containers
docker_nextcloud_stopped: no

# place for configs and data
docker_nextcloud_base_dir: /opt/nextcloud

```

## File tree
```
/opt/nextcloud
    ├── apache
    │   ├── html                # nextcloud html files
    │   └── conf                # apache configuration files
    ├── php
    │   └── conf                # php configuration files
    │   └── Dockerfile          # Dockerfile for php-apache container
    ├── mariadb
    │   ├── data                # mariadb files
    │   └── conf                # mariadb configuration
    |   └── dumps               # nextcloud database dumps
    ├── scripts                 # helper scripts
    ├── data                    # nextclouds data directory
    └── docker-compose.yml

```
