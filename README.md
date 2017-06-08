oc-project-migrator
=========

This role facilitates the migration of an OpenShift Container Platform project from one cluster to another.  In a test scenario, it can migrate the project to the same cluster.

Requirements
------------

At least one operational OpenShift Container Platform cluster.

Role Variables
--------------

The following variables can be found in defaults/main.yml.

```
---
---
# defaults file for kevensen.oc-project-migrator
# The Kubernetes Services to Migrate
services_to_migrate: []
# The Container Routes to Migrate
routes_to_migrate: []
# The Image Streams to Migrate
image_streams_to_migrate: []
# The Kubernetes Secrets to Migrate
secrets_to_migrate: []
# The Kubernetes Service Accounts to Migrate
service_accounts_to_migrate: []
# The Deployment Configurations to Migrate
deployments_to_migrate: []
# Add a string to the end of the project
# name. This is essential if you are migrating
# to the same cluster.
project_name_postpend: ''
# The default project role for the user
#migrating the project
project_role: 'view'
```

Dependencies
------------

This role requires the kevensen.oc role to be applied to a host as well.

Example Playbook
----------------

The following example shows how one can use this role to create a project.
```
---
# file: migrate.yml
- hosts: oc
  roles:
  - kevensen.oc
  - kevensen.oc-project-migrator
  vars:
    ansible_become: true
    project_name: cake
    project_name_postpend: '-test'
    services_to_migrate:
    - cakephp-mysql-example
    - mysql
    routes_to_migrate:
    - cakephp-mysql-example
    image_streams_to_migrate:
    - cakephp-mysql-example
    secrets_to_migrate:
    - cakephp-mysql-example
    deployments_to_migrate:
    - cakephp-mysql-example
    - mysql
```

License
-------

GPLv3

Author Information
------------------

Ken Evensen is a Solutions Architect with Red Hat
