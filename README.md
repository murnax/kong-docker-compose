# Kong with Docker-Compose

An example how to start using Kong in Docker compose.

In this compose file, there are 4 services:
- kong: API Gateway
- kong-migration: self-terminated container, is used to only migrate database for Kong.
- kong-database: Postgres database *(Kong supports Postgres and Cassandra)*
- dashboard: Kong GUI

And here is a dependency direction between each of these services:

<a href="./dependency-direction.png" target="_blank">  
  <img src="./dependency-direction.png" width="550">
</a>


- "kong-database" is the only service that has on dependencies on other services
- "kong" and "kong-migration" will depend on "kong-database"
- "dashboard" depends on "kong"

We set restarting policy on "kong" service to "always" because this service depends on migration status on "kong-database" that is handled by "kong-migration" that is a self-terminated service that will be removed after finish execution, so "kong" can not depend on "kong-migration".

### Todo:
- Integrate [Kongfig](https://github.com/mybuilder/kongfig) to setup upstream services.