## 📌 About

**DSList games** is a backend application developed during DevSuperior Week - an event organized by <b> <a href="https://github.com/devsuperior">DevSuperior.</a></b> It allows the user - once in the front-end - to be able to position the games in a list - by clicking and dragging - which is the main logic.

The system follows the Rest **API pattern** and handles **HTTP/REST requests** via **Get** and Post **methods**.

In practice, DsList games sends and handles game information through the use of Spring tools, SQL and databases - H2 (for testing) and Postgressql (for cloud application);

The data transaction takes place in three layers:

**1) Rest + DTO controllers:** Data Transfer Objects - the "backend gateway" - it makes the **API available.**

**2) Service Layer:** Where the business logic implementation takes place;

**3) Data access layer:** mediated by entities and ORM (Object Relational Mapping).

![image](https://github.com/JayCesar/dslist-games/assets/44206400/f79ca93e-d020-439e-9f22-502c7cca39c4)










![image](https://github.com/JayCesar/dslist-games/assets/44206400/f0bae213-a16f-47e8-aaeb-03aa9f510480)
