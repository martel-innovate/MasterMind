# Actor Management

## Registering new Actors

In MasterMind, Actors represent either Fiware Lab Users or Organizations.
MasterMind automatically creates a new Actor whenever a new User or Organization
successfully authenticate on Fiware Lab when logging in for the first time,
obtaining full name and email address from the lab as well. By default, the new
Actor doesn't have any Role within MasterMind, and thus has no access to any
existing Project. In order to be granted permission to view or alter a Project
the Actor needs to be assigned a Role within the Project by an Actor with an
Admin Role. When a Project is first created, the Actor who created the Project
is automatically given the Role of Admin. By default, Admins can perform any
action within a Project, including deleting it, while user Roles can only view
it. Permissions can be changed per Actor, such as granting an Actor the
permission to register new Services, but without allowing it to alter Clusters
for example. 

## MasterMind Superadmins

Actors within MasterMind can also be labelled as a Superadmin. When an Actor is
made a Superadmin it receives Admin level privileges to all Projects in
MasterMind regardless of its Role within individual Projects. In addition,
Superadmins can view and alter all registered Actors in MasterMind, and make
more Superadmins if needed. The purpose of Superadmins is the management of
the MasterMind platform as a whole, and thus the Superadmin status should only
be granted to whoever is Administrator for MasterMind.
