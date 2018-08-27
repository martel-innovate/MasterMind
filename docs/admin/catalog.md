# Catalog

## Introduction

The Service Catalog is a repository containing all the Service Types descriptors
supported by MasterMind. Such descriptors include both configuration templates
(for managed and unmanaged services) and the deployment templates (only for
managed services).

This section describes the structure of the Catalog: how to import a default
Catalog available to all MasterMind Projects, as well as importing custom
Catalogs that are specific to each Project.

## Catalog Entries

A Catalog for MasterMind can be imported from any Github repository. A Catalog
entry corresponds to a subfolder within the repository that contains:

- A `mastermind.yml` file (required), which describes the Service and its
  configuration options. This is what MasterMind uses to generate the UI forms
  to create and deploy new Services.
- A `docker-compose.yml` file (optional - it is required only for services that
  supports the managed configuration, e.g. any Service that a user can deploy
  from MasterMind itself), which describes the deployment of the service as a
  Docker Stack on a Swarm cluster.
- Config files (optional), to be used to create Docker configs.
- Secret files (optional), to be used to create Docker secrets.

## Configuration Template

The configuration template for a Catalog entry comes in the form of a YAML file,
named `mastermind.yml`. This file follows a specific structure, and defines
metadata regarding the Services this entry can deploy, as well as how the
Services are configurable at deployment time.

An example of a (mock) `mastermind.yml` file:

```yaml
name: comet
version: 1.0.0
description: Short Time Historic Data Management Service
protocol_type: HTTP
ngsi_version: 1
environment_variables:
  - variable: COMET_VERSION
    name: Comet Version
    description: The version of STH Comet to use
    required: true
    managed: true
    default: latest
  - variable: REPLICASET_NAME
    name: Replicaset Name
    description: The name of the Replica Set to use
    required: true
    managed: true
    default: rs
services:
  - service_type: mongo
    name: Mongo
    description: Mongo database to connect to
    required: true
    managed: true
    retrieve: endpoint
    as: MONGO_SERVICE_URI
```

The following options should be defined in the mastermind.yml file:

- name: the name of the Service Type (e.g. `orion`)
- version: the version of this Service Type (e.g. `1.0.3`)
- description: a description for the Service Type
- protocol_type: the protocol type being used by the Service Type (e.g. `HTTP`)
- ngsi_version: the version of NGSI being used by the Service Type (e.g. `v1`)
- environment_variables: the environment variables the user can provide at
  deployment time. This option comes in the form of a list, where each entry
  defines:
  - variable: the environment variable itself (e.g. `CONFIG_VARIABLE`)
  - name: a name for the environment variable (e.g. `Config Variable`)
  - description: a description for the variable
  - required: whether this variable is required or not (`true` or `false`)
  - managed: whether this variable is needed for a managed Service (`true` or
    `false`)
  - default: the default value for this variable
- services: other services that this Service can be "linked" to at deployment
  time. What this does is create a new environment variable whose value is taken
  from the endpoint of another Service for example. This option comes in the
  form of a list, where each entry defines:
  - service_type: the Type of the Service to link to (e.g. `mongo`)
  - name: the name for this link (e.g. `Mongo Database`)
  - description: a description for this Link
  - required: whether this link is required or not (`true` or `false`)
  - managed: whether this link is needed for a managed Service (`true` or
    `false`)
  - retrieve: the value to retrieve from the other Service. This can be any of
    the fields defined by the Service model (e.g. `endpoint`, `name`,
    `latitude`/`longitude`, ...)
  - as: the environment variable to store the retrieved value as (e.g.
    `MONGO_SERVICE_URI`)

## Deployment Template

The deployment template for a Catalog entry comes in the form of a
`docker-compose.yml` file, which describes how to deploy the Service on a Docker
Swarm cluster. These files should be compliant with Docker Compose Version 3.3
and up in order to be used by MasterMind, however not all options available in
Compose are currently supported.

To provide MasterMind users with some degree of configuration at deployment
time, the `docker-compose.yml` file can define environment variable substitution
as such:

```yaml
environment:
  - CONFIG_VARIABLE=${CONFIG_VARIABLE}
```

If default values are included, for example:

```yaml
environment:
  - CONFIG_VARIABLE=${CONFIG_VARIABLE:-foobar}
```

The value will be ignored when deploying the Service. For setting default values
always use the mastermind.yml configuration template.

These can then be defined in the configuration template, to be provided by the
user through MasterMind's UI when creating a new Service.

## Importing the global Catalog

When MasterMind is deployed, the default "official" Catalog will be imported
(as defined by the MASTERMIND_CATALOG_REPOSITORY env variable for the API).
This Catalog is available to all Projects in MasterMind, and it's intended to
contain a series of default recipes that all users can benefit from. The Catalog
can be manually updated even when MasterMind is running from the UI by a
MasterMind Superadmin.

## Importing a custom Catalog/Recipe

In addition to the "official" global Catalog, MasterMind users can choose to
import their own Catalogs and Recipes within the Projects they own in
MasterMind.
Unlike the global Catalog, the entries of custom Catalogs are only available
within the Projects they were imported in.
Custom Catalogs can be imported directly from the UI, specifying the Github
repository that contains the Catalog and the branch to checkout. Single recipes
can also be imported by simply uploading the corresponding mastermind.yml and
docker-compose.yml files.
