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

***

## 📝 DSList domain model

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

## 🛠️ Tools used: 
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

## Project tests in H2
- TB_GAME_LIST
![image](https://github.com/JayCesar/dslist-games/assets/44206400/fbb526c2-4026-47e6-9cfb-e66369566e18)

- TB_GAME
![image](https://github.com/JayCesar/dslist-games/assets/44206400/0f3ab7df-88f9-4d83-95ed-5cb26edcbe3a)

- TB_BELONGING
![image](https://github.com/JayCesar/dslist-games/assets/44206400/70fa021c-cf26-4184-a42d-7ce829f46fc0)

## Project tests in POSTGRESQL
- TB_GAME_LIST
![image](https://github.com/JayCesar/dslist-games/assets/44206400/4dcdba6a-fd97-4039-ba6b-568240394cdb)

- TB_GAME
![image](https://github.com/JayCesar/dslist-games/assets/44206400/96598174-791a-4f27-b4f4-8f15cb3cd950)

- TB_BELONGING
![image](https://github.com/JayCesar/dslist-games/assets/44206400/bb15e66d-8003-4530-bb6c-07f17275db0f)

## Testes do projeto no Postman
- GET GAMES
![image](https://github.com/JayCesar/dslist-games/assets/44206400/1d7c0cf1-3325-4e32-b8a6-ae5ab30226b6)

- GET GAMES LISTS
![image](https://github.com/JayCesar/dslist-games/assets/44206400/daea46f9-6e5e-47b9-821c-212caa61176a)

- GET GAMES BY LIST
![image](https://github.com/JayCesar/dslist-games/assets/44206400/3942a001-fc05-4e82-9d51-d25264ed295e)

- GET GAMES BY ID
![image](https://github.com/JayCesar/dslist-games/assets/44206400/76bf5a63-0998-4cba-a2ac-f85937cf5425)

- POST LIST REPLACEMED
![image](https://github.com/JayCesar/dslist-games/assets/44206400/29dec29c-9733-4935-8f40-fcc6fb2eb217)

***

## 🎥 Video demo

https://github.com/JayCesar/dslist-games/assets/44206400/f2fa9762-eafc-4d5e-b700-0b57e9bd6fbf

***

## Code snippets

### Plug-in Maven

```xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-resources-plugin</artifactId>
	<version>3.1.0</version> <!--$NO-MVN-MAN-VER$ -->
</plugin>
```

### application.properties

```
spring.profiles.active=${APP_PROFILE:test}
spring.jpa.open-in-view=false

cors.origins=${CORS_ORIGINS:http://localhost:5173,http://localhost:3000}
```

### application-test.properties

```
# H2 Connection
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.username=sa
spring.datasource.password=

# H2 Client
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

# Show SQL
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

### application-dev.properties

```
#spring.jpa.properties.jakarta.persistence.schema-generation.create-source=metadata
#spring.jpa.properties.jakarta.persistence.schema-generation.scripts.action=create
#spring.jpa.properties.jakarta.persistence.schema-generation.scripts.create-target=create.sql
#spring.jpa.properties.hibernate.hbm2ddl.delimiter=;

spring.datasource.url=jdbc:postgresql://localhost:5432/dscatalog
spring.datasource.username=postgres
spring.datasource.password=1234567

spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
spring.jpa.hibernate.ddl-auto=none
```

### application-prod.properties
```
spring.datasource.url=${DB_URL}
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}

spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
spring.jpa.hibernate.ddl-auto=none
```

### system.properties
```
java.runtime.version=17
```

### WebConfig

```java
@Configuration
public class WebConfig {

	@Value("${cors.origins}")
	private String corsOrigins;
	
	@Bean
	public WebMvcConfigurer corsConfigurer() {
		return new WebMvcConfigurer() {
			@Override
			public void addCorsMappings(CorsRegistry registry) {
				registry.addMapping("/**").allowedMethods("*").allowedOrigins(corsOrigins);
			}
		};
	}
	
}
```

### GameRepository

```java
@Query(nativeQuery = true, value = """
		SELECT tb_game.id, tb_game.title, tb_game.game_year AS `year`, tb_game.img_url AS imgUrl,
		tb_game.short_description AS shortDescription, tb_belonging.position
		FROM tb_game
		INNER JOIN tb_belonging ON tb_game.id = tb_belonging.game_id
		WHERE tb_belonging.list_id = :listId
		ORDER BY tb_belonging.position
			""")
List<GameMinProjection> searchByList(Long listId);
```

### GameListRepository

```java
@Modifying
@Query(nativeQuery = true, value = "UPDATE tb_belonging SET position = :newPosition WHERE list_id = :listId AND game_id = :gameId")
void updateBelongingPosition(Long listId, Long gameId, Integer newPosition);
```

### import.sql

```sql
INSERT INTO tb_game_list (name) VALUES ('Aventura e RPG');
INSERT INTO tb_game_list (name) VALUES ('Jogos de plataforma');

INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('Mass Effect Trilogy', 4.8, 2012, 'Role-playing (RPG), Shooter', 'XBox, Playstation, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/1.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');
INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('Red Dead Redemption 2', 4.7, 2018, 'Role-playing (RPG), Adventure', 'XBox, Playstation, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/2.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');
INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('The Witcher 3: Wild Hunt', 4.7, 2014, 'Role-playing (RPG), Adventure', 'XBox, Playstation, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/3.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');
INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('Sekiro: Shadows Die Twice', 3.8, 2019, 'Role-playing (RPG), Adventure', 'XBox, Playstation, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/4.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');
INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('Ghost of Tsushima', 4.6, 2012, 'Role-playing (RPG), Adventure', 'XBox, Playstation, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/5.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');
INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('Super Mario World', 4.7, 1990, 'Platform', 'Super Ness, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/6.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');
INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('Hollow Knight', 4.6, 2017, 'Platform', 'XBox, Playstation, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/7.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');
INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('Ori and the Blind Forest', 4, 2015, 'Platform', 'XBox, Playstation, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/8.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');
INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('Cuphead', 4.6, 2017, 'Platform', 'XBox, Playstation, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/9.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');
INSERT INTO tb_game (title, score, game_year, genre, platforms, img_url, short_description, long_description) VALUES ('Sonic CD', 4, 1993, 'Platform', 'Sega CD, PC', 'https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/10.png', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Odit esse officiis corrupti unde repellat non quibusdam! Id nihil itaque ipsum!', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus dolorum illum placeat eligendi, quis maiores veniam. Incidunt dolorum, nisi deleniti dicta odit voluptatem nam provident temporibus reprehenderit blanditiis consectetur tenetur. Dignissimos blanditiis quod corporis iste, aliquid perspiciatis architecto quasi tempore ipsam voluptates ea ad distinctio, sapiente qui, amet quidem culpa.');

INSERT INTO tb_belonging (list_id, game_id, position) VALUES (1, 1, 0);
INSERT INTO tb_belonging (list_id, game_id, position) VALUES (1, 2, 1);
INSERT INTO tb_belonging (list_id, game_id, position) VALUES (1, 3, 2);
INSERT INTO tb_belonging (list_id, game_id, position) VALUES (1, 4, 3);
INSERT INTO tb_belonging (list_id, game_id, position) VALUES (1, 5, 4);

INSERT INTO tb_belonging (list_id, game_id, position) VALUES (2, 6, 0);
INSERT INTO tb_belonging (list_id, game_id, position) VALUES (2, 7, 1);
INSERT INTO tb_belonging (list_id, game_id, position) VALUES (2, 8, 2);
INSERT INTO tb_belonging (list_id, game_id, position) VALUES (2, 9, 3);
INSERT INTO tb_belonging (list_id, game_id, position) VALUES (2, 10, 4);
```

### Script Docker Compose

https://gist.github.com/acenelio/5e40b27cfc40151e36beec1e27c4ff71


