# Overview

MasterMind uses relational data models to represent the various entities that it
tracks. This section provides a full reference to all of them.

## Actors

This model represents a MasterMind Actor, which could refer to a singular user
or an organization of many users. The Actor credentials are obtained from a
Fiware Lab user/organization.

An Actor is defined by:

- **Fullname**: The full name of the actor
- **Email**: The email associated to the actor

## Projects

This model represents a Project within MasterMind, where each Project contains
its own set of registered Actors, Services, Clusters and Subscriptions.

A Project is defined by:

- **Name**: The name of the project
- **Description**: The description of the project

## Clusters

This model represents a Docker Swarm Cluster registered to a project, where the
IoT Services are going to be deploted onto.

A Cluster is defined by:

- **Name**: The name MasterMind is going to refer the cluster by
- **Description**: A description for the registered cluster
- **Project**: The project this cluster is registered to
- **Endpoint**: The endpoint of the master node of the Docker Swarm cluster
- **Cert**: The Cert certificate for accessing the cluster using TLS
- **Ca**: The Ca certificate for accessing the cluster using TLS
- **Key**: The Key for accessing the cluster using TLS

## Roles

This model represents a Role a certain Actor has within a project. This can be
either an Admin role or a User role, where the latter doesn't have permission
to perform certain actions inside of a MasterMind project, such as deleting a
project entirely for example.

A Role is defined by:

- **Role Level**: The Role Level, which can be either 1 for Admin or 2 for User
- **Project**: The Project this Role refers to
- **Actor**: The Actor this Role is assigned to

## Services

This model represents an IoT Service registered within a MasterMind Project.
Services within MasterMind are generally mapped to what Docker Swarm refers to
as a Stack, as IoT Services can be made out of multiple separate components that
Docker refers to as individual services (e.g. a Context Broker and its
Database).

A Service is defined by:

- **Name**: The name MasterMind is going to refer to the service by
- **Service Type**: The Service Type this Service belongs to
- **Project**: The Project this service belongs to
- **Managed**: Whether the Service is managed or unmanaged by MasterMind
- **Cluster**: The Cluster this Service is or will be deployed to
- **Docker Service ID**: The ID of the deployed Service (stack) on Docker
- **Configuration**: The set of environment variables to provide to the Service
  when deploying it to a Cluster
- **Status**: The current status of the Service on the Cluster (e.g. Active,
  Inactive)
- **Endpoint**: The endpoint the Service can be reached at

## Service Types

This model represents a Service Type, which individual Services can belong to
(e.g Orion Context Broker).

A Service Type is defined by:

- **Name**: The name of the Service Type
- **Protocol Type**: The protocol used by the Service Type (e.g. HTTP)
- **NGSI Version**: The version of NGSI used by this Service, if any
- **Configuration Template**: The template describing how the Services belonging
  to this type are meant to be configured when the Services are
  deployed/registered
- **Deploy Template**: The template for deploying Services of this type to a
  cluster (usually this is the Docker Compose file that deploys them)

## NGSI Subscriptions

This model represents a NSGI V2 Subscription, to be registered to a Context
Broker (see the NGSI specs
[here](http://fiware.github.io/specifications/ngsiv2/stable/)).

A NGSI Subscription is defined by:

- **Name**: The name MasterMind is going to refer to this Subscription by
- **Description**: A description for the Subscription
- **Subscription ID**: The ID of the Subscription given by the Context Broker
- **Service**: The Service (Context Broker) this Subscription belongs to
- **Expires**: The expiration time of the Subscription (if any)
- **Throttling**: The Throttling period of the Subscription
- **Status**: The Status of the Subscription (e.g. Active, Inactive)
- **Subject**: The Subject of the Subscription, which is a JSON object
  containing mainly the entities and attributes to observe
- **Notfication**: The Notification object of the Subscription, which is a JSON
  object containing mainly the endpoint that Notifications are being sent to
