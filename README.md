# Microservices boilerplate built with NestJS & RabbitMQ

This boilerplate implementing:

- Clean Architecture by Uncle Bob[(source)](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html).
- Event Driven Architecture(Microservice).

# Technology Used:

- NestJS Framework
- RabbitMQ Message Broker
- Docker
- Kong Api Gateway
- TypeORM
- Mysql
- Caching in every HTTP GET Method (NestJS built in package)
- Rate Limiting Security (NestJS built in package)

# Quick Review:

1. Clean architecture means that the business logic app needs to be separated with its delivery mechanism. To follow that rule in this case I made 3 main folder for each service(domain, use_case & infrastructure) where there are 3 service in this boilerplate(user, product & transaction) and I'll give a quick explain for each folder to the following:

- domain: contains the business code and its logic and has no outward dependency: nor on frameworks (NestJS in our case), nor on use_cases or infrastructure packages.
- usecases: use_case depends only on domain package to execute business logic. use_cases should not have any dependencies on infrastructure (including framework or npm module).
- infrastructure: contains all the technical details, configuration, implementations (database, web services, npm module, etc.), and must not contain any business logic. infrastructure has dependencies on domain, use_cases and frameworks.

2. Event driven architecture means that each service not depends on another service. But in this case I still haven't done the best practice of it since microservice built in package in NestJS only provide one consumer on each service(cmiiw) means that if there's any data changed in a service, it needs to broadcast the data to all its consumer. I'm still working on this, to improve the implementation of event driven architecture best practice.

# Getting Started

```bash
git clone --recursive https://github.com/Ammarfar/microservices.git
cd microservices
docker-compose up -d
```

open the browser and go to http://localhost:8000/{service}/v1/{services} (still on progress to fix this routing)
see the detail in postman collection https://documenter.getpostman.com/view/12263458/2s9XxySDhm

# Pending Improvement

- fix routing
- implement unit testing
- each service hasn't isolated yet, still can access it when hit its url
- need to build custom event listener since each service only can consume to one queue in one transport method in NestJS

# Challenge

- build trx service using another language(Go/Java)
