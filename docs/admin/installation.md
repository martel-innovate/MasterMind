# Installation

## API

The backend of MasterMind is a Rails 5 API application, backed by a MySQL
database.

The quickest way to run it is with Docker. The image can be pulled directly from
Dockerhub, and the API can be run as a Docker container, exposed on port 3000:

```shell
docker run -d --name mastermind-api -p 3000:3000 martel/mastermind-api
```

Alternatively, the image can be built with the Dockerfile provided on the API's
Github repository.

```shell
cd /dockerfile/location
docker build -t mastermind-api .
docker run -d --name mastermind-api -p 3000:3000 mastermind-api
```

To run it without using Docker, Ruby 2.4 or higher and Rails 5 need to be
installed on the host (see the
[Rails Starting Guide](http://guides.rubyonrails.org/getting_started.html)).
Afterwards, the admin can install the dependancies, initialize the database and
start the Rails server as such for example:

```shell
bundle install
rails db:setup
rails s
```

The service's default configuration can be overridden through the use of a few
environment variables:

- MASTERMIND_VERSION: The current version of MasterMind
- SERVICE_MANAGER_HOST: The host of MasterMind's Service Manager Microservice,
  (e.g. service-manager)
- SERVICE_MANAGER_PORT: The port of MasterMind's Service Manager Microservice,
  (e.g. 8080)
- MASTERMIND_API_HOST: The Host of the MasterMind API. This should be localhost
  for a local deployment for instance.
- MASTERMIND_API_PORT: The Port of the MasterMind API. By default it's 3000
- MASTERMIND_UI_HOST: The UI of the MasterMind UI. This should be localhost
  for a local deployment for instance.
- MASTERMIND_UI_PORT: The Port of the MasterMind UI. By default it's 8080
- MASTERMIND_OAUTH_URI: The URI of the OAUTH IDM to use for MasterMind. By
  default it uses the official Fiware Lab installation at
  <https://account.lab.fiware.org>
- MASTERMIND_OAUTH_CLIENT_ID: The Client ID for OAUTH2 authentication
- MASTERMIND_OAUTH_SECRET_ID: The Secret ID for OAUTH2 authentication
- MASTERMIND_CATALOG_REPOSITORY: The URI of the Github repository where the
  global "official" Catalog for the MasterMind Service Types is found
  (e.g [https://github.com/martel-innovate/MasterMind-Service-Catalog])
- MASTERMIND_CATALOG_REPOSITORY_BRANCH: The Branch to use for the Catalog repo
  (e.g master)
- MASTERMIND_DB_PASSWORD: The password used in the MySQL database for the
  MasterMind data.
- MASTERMIND_DB_HOST: The host of the MySQL database for the MasterMind data.
  This should be localhost for a local deployment for instance.
- OAUTH_ENABLED: This is set to true or false depending on whether you want
  the Oauth authentication to be enabled or not. Setting this to false is good
  for testing the API without needing to go through authenticating and getting
  tokens, but it's not recommended in any other situation.
- SECRET_KEY_BASE: The base string for Rails to handle tokens and cookies. It
  would be best to generate a new random string to use here when deploying to
  production environments.
  
## Service Manager

The Service Manager is a Microservice, written in Python, which performs the
actual interactions with the Docker Swarm Clusters registered in MasterMind. It
performs similar actions to the command line Docker client, which include
parsing Docker Compose files, deploying Services, and providing data on the
Clusters.

It can easily be deployed with Docker, pulling the image straight from Dockerhub
and exposing it on port 8000 for instance.

```shell
docker run -d --name mastermind-service-manager -p 8000:8080 icclab/mastermind-service-manager
```

Alternatively, the image can be built manually using the Dockerfile on the
Github repository.

```shell
cd /dockerfile/location
docker build -t mastermind-service-manager .
docker run -d --name mastermind-service-manager -p 8000:8080 mastermind-service-manager
```

## UI

The frontend of MasterMind is a [Vue.js](https://vuejs.org/) application,
harnessing [Bulma](https://bulma.io/) for styling.

The UI can be run easily with Docker, much like the UI and Service Manager,
running it on port 8080 by default.

```shell
docker run -d --name mastermind-ui -p 8080:8080 martel/mastermind-ui
```

Building the image manually:

```shell
cd /dockerfile/location
docker build -t mastermind-ui .
docker run -d --name mastermind-ui -p 8080:8080 mastermind-ui
```

To run the UI without Docker, Node.js 6 needs to be installed. The admin can
then install the Vue.js dependancies and serve the UI with npm as such:

```shell
npm install
npm run dev
```

The UI's default configuration can be overriden through the use of a few
environment variables:

- MASTERMIND_API_HOST: The host of MasterMind's API
  (e.g. localhost)
- MASTERMIND_API_PORT: The port of MasterMind's API
  (e.g. 3000)
- MASTERMIND_OAUTH_URI: The URI of the Oauth Identity Provider (a Fiware Lab
  instance in MasterMind's case, e.g account.lab.fiware.org)
- MASTERMIND_OAUTH_CLIENT_ID: The Client ID for OAUTH2 authentication
