# Wobbly GraphQL Engine on Docker with pgAdmin

This Docker Compose setup runs [Hasura GraphQL Engine](https://github.com/hasura/graphql-engine) along with Postgres and [pgAdmin4](https://www.pgadmin.org/) using `docker-compose`.

## Pre-requisites

- [Docker](https://docs.docker.com/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Usage

- Clone this repo on a machine where you'd like to deploy graphql engine
- Copy `docker-compose.override.yml.dist` to `docker-compose.override.yml`
- Edit `docker-compose.override.yml` and change `POSTGRES_PASSWORD`, `PGADMIN_DEFAULT_EMAIL` and `PGADMIN_DEFAULT_PASSWORD` to something secure
- Edit `docker-compose.override.yml` and change 'changeme' substring in `HASURA_GRAPHQL_DATABASE_URL` with `POSTGRES_PASSWORD` value
- Edit `docker-compose.override.yml` and change `HASURA_GRAPHQL_ADMIN_SECRET` to something secure
- `docker-compose up -d --build`
- Go to the http://127.0.0.1:5050 and login to the pgAdmin via `PGADMIN_DEFAULT_EMAIL` and `PGADMIN_DEFAULT_PASSWORD`
- Use pgAdmin UI to add new connection to the postgres server
- Connect to the postgres server
- Drop Cascade all the Schemas
- Create new schema with name `public` using `postgres` owner
- Enter to the postgres docker container `docker exec -ti <postgres-container> bash`
- Restore database using `pg_restore -U <POSTGRES_USER> -d postgres -1 /data/fixtures/fixtures.dump`
- Type `exit` to go out from the container
- `docker-compose down`
- `docker-compose up -d --build`

## Important endpoints

- GraphQL endpoint will be `http://127.0.0.1:8080/v1/graphql`
- Hasura Console will be available on `http://127.0.0.1:8080/console`
- pgAdmin will be available on `http://127.0.0.1:5050`
