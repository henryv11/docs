# docker

## building

### provide build time arguments

```shell
--build-arg ARG_NAME=ARG_VALUE
```

## containers

### stop all containers

```shell
  docker stop $(docker ps -a -q)
```

### remove all containers

```shell
  docker rm $(docker ps -a -q)
```

## docker compose

### run docker-compose.yaml file

```shell
    docker-compose up
```

### nodejs typescript for development

#### sample docker-compose entry for running a nodejs typescript app in

```yaml
sample:
  container_name: sample_container
  image: node:12-alpine
  volumes:
    - <path-to-project-directory>:/sample
  working_dir: /sample
  command: npm run dev
  ports:
    - "8080:8080"
  restart: unless-stopped
```

#### package.json

```json
{
  ...
  "scripts": {
    "dev": "ts-node-dev ./src/index.ts"
  }
  ...
}
```

### postgres container

#### sample docker-compose service entry for postgres

```yaml
postgres:
container_name: postgres_container
image: postgres
environment:
  POSTGRES_USER: postgres
  POSTGRES_PASSWORD: postgres
  PGDATA: /data/postgres
volumes:
  - postgres:/data/postgres
ports:
  - "5431:5432"
command: -p 5431
restart: unless-stopped
```

when using other port than 5432 you'll need to change the port in container also, for example

```yaml
ports:
  - "5431:5432"
command: -p 5431
```

### pgadmin container

#### sample docker-compose service entry for pgadmin

```yaml
pgadmin:
container_name: pgadmin_container
image: dpage/pgadmin4
environment:
  PGADMIN_DEFAULT_EMAIL: pgadmin4@pgadmin.org
  PGADMIN_DEFAULT_PASSWORD: admin
volumes:
  - pgadmin:/root/.pgadmin
ports:
  - "5050:80"
restart: unless-stopped
```
