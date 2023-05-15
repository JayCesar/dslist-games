## 📌 About

**DSList games** is a backend application developed during DevSuperior Week - an event organized by <b> <a href="https://github.com/devsuperior">DevSuperior.</a></b> 

It allows the user - once in the front-end - to be able to position the games in a list - by clicking and dragging - which is the main logic.

The system follows the Rest **API pattern** and handles **HTTP/REST requests** via **Get** and Post **methods**.

In practice, DsList games sends and handles game information through the use of Spring tools, SQL and databases - H2 (for testing) and Postgressql (for cloud application);

The data transaction takes place in three layers:

 **1) Rest + DTO controllers:** Data Transfer Objects - the "backend gateway" - it makes the **API available.**

 **2) Service Layer:** Where the business logic implementation takes place;

 **3) Data access layer:** mediated by entities and ORM (Object Relational Mapping).

![image](https://github.com/JayCesar/dslist-games/assets/44206400/f79ca93e-d020-439e-9f22-502c7cca39c4)

## DSList domain model

![image](https://github.com/JayCesar/dslist-games/assets/44206400/f0bae213-a16f-47e8-aaeb-03aa9f510480)

***

## 🎯 Goals of the project:

- Apply concepts (Web systems and resources; Client/server, HTTP, JSON; REST standard for web API);
- Spring Rest project structuring;
- Entities and ORM;
- Database seeding;
- Pattern layers;
- controller, service, repository;
- DTO Standard;
- N-N Relationships;
- Association class, embedded id;
- SQL Queries in Spring Data JPA;
- projections;
- project profiles;
- Local environment with Docker Compose;
- Local approval process;
- Deployment process with CI/CD;
- CORS configuration.

***

Tools used: 
- ``Java``
- ``Spring Boot``
- ``Docker``
- ``JPA / Hibernate``
- ``Maven``
- ``API Rest``
- ``H2 Database``
- ``PostgreSQL``
- ``Postman``

***

## Testes do projeto no H2
- TB_GAME_LIST
![image](https://github.com/JayCesar/dslist-games/assets/44206400/fbb526c2-4026-47e6-9cfb-e66369566e18)

- TB_GAME
![image](https://github.com/JayCesar/dslist-games/assets/44206400/0f3ab7df-88f9-4d83-95ed-5cb26edcbe3a)

- TB_BELONGING
![image](https://github.com/JayCesar/dslist-games/assets/44206400/70fa021c-cf26-4184-a42d-7ce829f46fc0)

## Testes do projeto no POSTGRESQL
- TB_GAME_LIST
