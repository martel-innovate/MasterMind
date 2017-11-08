API
---

The backend of MasterMind is a Rails 5 API application, backed by a MySQL database.

The quickest way to run it is with Docker: building the image with the Dockerfile provided on the API's Github repository, and running it as a Docker container, exposing it on port 3000.

```
cd /dockerfile/location
docker build -t mastermind-api .
docker run -d --name mastermind-api -p 3000:3000 mastermind-api
```

To run it without using Docker, Ruby 2.4 or higher and Rails 5 need to be installed on the host. Afterwards, the admin can install the dependancies, initialize the database and start the Rails server as such for example:

```
bundle install
rails db:setup
rails s
```

The service's default configuration can be overriden through the use of a few environment variables:

  - MASTERMIND_VERSION: the current version of MasterMind
  - SERVICE_MANAGER_URI: the URI of MasterMind's Service Manager Microservice, port and protocol included (e.g. http://service-manager:8081)

Service Manager
---------------

The Service Manager of MasterMind is a Microservice, written in Python, which performs the actual interactions with the Docker Swarm Clusters registered in MasterMind. It performs similar actions to the command line Docker client, which include parsing Docker Compose files, deploying Services, and providing data on the Clusters.

It can easily be deployed with Docker, building the image with the provided Dockerfile, and exposing it on port 8000 for instance.

```
cd /dockerfile/location
docker build -t mastermind-service-manager .
docker run -d --name mastermind-service-manager -p 8000:8080 mastermind-service-manager
```

UI
---

The frontend of MasterMind is a Vue.js application, harnessing Bulma for styling.

The UI can be run easily with Docker, much like the UI and Service Manager, running it on port 8080 by default.

```
cd /dockerfile/location
docker build -t mastermind-ui .
docker run -d --name mastermind-ui -p 8080:8080 mastermind-ui
```

To run the UI without Docker, Node.js 6 needs to be installed. The admin can then install the Vue.js dependancies and serve the UI with node.

```
npm install
npm run dev
```

The UI's default configuration can be overriden through the use of a few environment variables:

  - MASTERMIND_VERSION: the current version of MasterMind
  - MASTERMIND_API_URI: the URI of MasterMind's API, port and protocol included (e.g. http://localhost:3000)
