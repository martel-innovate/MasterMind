# Installation

## API

The backend of MasterMind is a Rails 5 API application, backed by a MySQL
database.

The quickest way to run it is with Docker. The image can be pulled directly from
Dockerhub, and the API can be run as a Docker container, exposed on port 3000.:

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

The service's default configuration can be overriden through the use of a few
environment variables:

- MASTERMIND_VERSION: the current version of MasterMind
- SERVICE_MANAGER_HOST: the host of MasterMind's Service Manager Microservice,
  (e.g. service-manager)
- SERVICE_MANAGER_PORT: the port of MasterMind's Service Manager Microservice,
  (e.g. 8080)

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

- MASTERMIND_VERSION: the current version of MasterMind
- MASTERMIND_API_HOST: the host of MasterMind's API
  (e.g. localhost)
- MASTERMIND_API_PORT: the port of MasterMind's API
  (e.g. 3000)
