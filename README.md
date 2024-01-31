# op-be-docs
The Documentations for the Backend Layer of OctopOSPrime

## Development Environment

#### go.work
```
use github.com/octoposprime/op-be-shared
use github.com/octoposprime/op-be-logging
use github.com/octoposprime/op-be-user
use github.com/octoposprime/op-be-graphql
```

#### .env
```
POSTGRES_USERNAME=op
POSTGRES_PASSWORD=op
JWT_SECRET_KEY=op
REDIS_PASSWORD=op
```

#### Docker
```
// Create Network
docker network create op 

// Run Postgres
docker run -d --expose 5432 -p 5432:5432 --network op --name postgres -e POSTGRES_USER={POSTGRES_USERNAME} -e POSTGRES_PASSWORD={POSTGRES_PASSWORD} -e POSTGRES_DB=op postgres

// Run Redis
docker run -d --expose 6379 -p 6379:6379 --network op --name redis -e REDIS_PASSWORD={REDIS_PASSWORD} redis --requirepass "{REDIS_PASSWORD}"

// Run Pgadmin
docker run -d --expose 5050 -p 5050:80 --network op --name pgadmin -e "PGADMIN_DEFAULT_EMAIL={PGADMIN_EMAIL}" -e "PGADMIN_DEFAULT_PASSWORD={PGADMIN_PASSWORD}" dpage/pgadmin4

// Portainer
docker run -d --expose 9000 -p 9000:9000 --network op --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data portainer/portainer

// RedisInsight
docker run -d --expose 8001 -p 8001:8001 --network op --name rinsight -e RIAUTHPROMPT=true -e RIAUTHTIMER=30 -v redisinsight:/db redislabs/redisinsight:latest
```

## Test Environment
```
	docker stop op-be-logging
	docker stop op-be-user
	docker stop op-be-graphql

	docker rm op-be-logging
	docker rm op-be-user
	docker rm op-be-graphql

	docker run --pull=always -d --expose 18081 -p 18081:18080 --network op -e TEST=true --name op-be-logging ghcr.io/octoposprime/op-be-logging:latest
	docker run --pull=always -d --expose 18082 -p 18082:18080 --network op -e TEST=true --name op-be-user ghcr.io/octoposprime/op-be-user:latest
	docker run --pull=always -d --expose 18080 -p 18080:18080 --network op -e TEST=true --name op-be-graphql ghcr.io/octoposprime/op-be-graphql:latest
```

## Pre-Prod Environment

## Prod Environment