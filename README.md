# MasterMind

## Introduction

MasterMind is a management platform for FIWARE Data and IoT services, such as
Context Brokers, IoT Agents, IoT Managers and so forth. It allows users to
create individual projects with defined permissions per user, register Docker
Swarm clusters to them in order to deploy or register IoT services, as well as
registering and managing NSGI subscriptions.

## Quick Start

The simplest way to get MasterMind up and running is via Docker, using the
`docker-compose.yml` file provided. To deploy MasterMind, navigate to the folder
containing the compose file and type:

```shell
docker-compose up
```

MasterMind's UI can be found on port 8080 by default. The environment variables
that are passed to the MasterMind components can be altered in the compose file
if needed, but the defaults will work out of the box for some simple testing.

## Documentation

For the complete Documentation see [here](http://mastermind-main.readthedocs.io/en/latest/)

## Related Repositories

- [MasterMind API](https://github.com/martel-innovate/MasterMind-API)
- [MasterMind Service Catalog](https://github.com/martel-innovate/MasterMind-Service-Catalog)
- [MasterMind Service Manager](https://github.com/icclab/MasterMind-ServiceManager)
- [MasterMind UI](https://github.com/martel-innovate/MasterMind-UI)

## How to contribute

Contributions are welcomed in the form of Github Pull Requests. It is
recommended to squash commits before pulling, and writing a detailed description
of what the Pull Request aims to do. If any Github Issue is being addressed,
make sure to reference it in the description.

Feel free to open an issue for reporting bugs, or suggesting new features and
enhancements.

## License

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at
[HERE](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
