docker_nagios
=============

The main repo for this role is on [Le Filament GitLab](https://sources.le-filament.com/lefilament/ansible-roles/docker_nagios.git)
This role deploys Nagios in Docker for monitoring all hosts defined in Ansible inventory for services depending on groups they belong to.
The authentifcation mechanism for Nagios is disabled in this role, replaced by Traefik one.
Also, specific css files are provisionned in this role to update Nagios UI look & feel.

Requirements
------------

None

Role Variables
--------------

Variables from default directory :
* nagios_url: URL on which Nagios will be listening
* webhooks_to_be_called_daily: list of WebHooks to be called daily
* services_to_be_monitored: list of extra services to be monitored

Variables used on other hosts for monitoring :
* raid_config: for monitoring RAID configuration
* urls for every service listed below

Hosts from the following groups added to monitoring :
* docker
* docker_direct_internet_access
* docker_restrict_internet_access
* full_maintenance
* backup_server
* docker_auth
* docker_drawio
* docker_etherpad
* docker_framadate
* docker_jitsi
* docker_mattermost
* docker_nagios
* docker_nextcloud
* docker_odoo
* docker_owncloud
* docker_privatebin
* docker_tuleap
* gitlab
* odoo_server
* owncloud_server

Dependencies
------------

This role requires the following Ansible collection :
* community.docker

This Docker role supposes that Traefik is deployed as an inverseproxy in front of the deployed Dockers.
The following role is used by Le Filament for deploying Traefik : docker_server (https://sources.le-filament.com/lefilament/ansible-roles/docker_server)
As explained above, this role is based on inventory and configures monitoring for all hosts depending on the groups they belong to. Roles for deploying other hosts and supported services are available in Le Filament GitLab (https://sources.le-filament.com/le-filament/ansible-roles/)

Example Playbook
----------------

    - hosts: docker_nagios
      roles:
      - { role: docker_nagios, tags: docker_nagios }
      vars:
      - { nagios_url: "nagios.example.org" }

License
-------

AGPL-3

Author Information
------------------

Le Filament (https://le-filament.com)
