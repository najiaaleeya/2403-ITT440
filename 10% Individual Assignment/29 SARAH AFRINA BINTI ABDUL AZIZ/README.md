`SARAH AFRINA BINTI ABDUL AZIZ | 2022495434 | CDCS2554A | ITT440 | PREPARED FOR SIR SHAHADAN SAAD`

# TITLE: HOW TO DOCKER COMPOSE

## What is Docker Compose?
- Docker Compose is a tool for defining and running multi-container applications.
- It is key to unlocking a streamlined and efficient development and deployment experience.

## What is Compose?
- Compose simplifies control of your entire application stack, making it easy to manage services, networks
  and volumes in a single, comprehensible YAM configuration file.
- With a single command, you can create and start all the services from your configuration file.
- Compose works in all environments such as production, staging, development, testing, as well as CI workflows.
It also has commands for managing the whole lifecycle of your application:
```
- start, stop and rebuild services
- view the status of running services
- stream the log output of running services
- run a one-off command on a service

```
## Why use Compose?
### Key benefits of Docker Compose
- Simplified control: define and manage multi-container applications in a single YAML file.
- Efficient collaboration: configuration files are easy to share, facilitating collaboration among developers, 
  operations teams and other stakeholders.
- Rapid application development: Compose caches the configuration used to create a container.
- Portability across environments: supports variables in the Compose file.
- Extensive community and support: Docker Compose benefits from a vibrant and active community, which means
  abundant resources, tutorials and support.

### Common use cases of Docker Compose
1. Development environments
   - Compose file provides a way to document and configure all of the application's service dependencies(database,
     queues, caches, web service APIs, etc)
   - Using the Compose command line tool you can create and start one or more containers for each dependency with
     a single command (`docker compose up`)
2. Automated testing environments
   - Automated end-to-end testing requires an environment in which to run tests
   - Compose provides a convenient way to create and destroy isolated testing environments for your test suites
   - By defining, the full environment in a Compose file, you can create and destroy these envrionments in just 
     few commands:
     ```
     $ docker compose up -d
     $ ./run_tests
     $ docker compose down
     ```
3. Single host deployments
   - Compose has traditionally been focused on development and testing workflows, but with each release we're making 
     progress on more production-oriented features

## How Compose works


 
