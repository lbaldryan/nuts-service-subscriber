# Nuts Service Subscriber 

This project is a 3-layer Java application that connects to a RabbitMQ message bus ("nutsQueue"), processes messages, and stores them in a PostgreSQL database. It includes:
- RabbitMQ listener
- Business logic
- PostgreSQL persistence

This version is **not Dockerized**. All dependencies must be run manually.

## Project Structure

```
src/
  main/
    java/
      org.example.nutssubscriber/
        api/                <-- RabbitMQ message listener
        service/            <-- Business logic
        repository/         <-- Data layer (JPA, PostgreSQL)
        NutsSubscriberApplication.java
  test/
    java/
      org.example.nutssubscriber/  <-- Unit tests
```

## Prerequisites

- Java 17
- Maven
- RabbitMQ server (running locally)
- PostgreSQL server (running locally)

---

## Configuration

### `application.properties`
Located at: `src/main/resources/application.properties`

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/nutsdb
spring.datasource.username=postgres
spring.datasource.password=098148675

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

spring.rabbitmq.host=localhost
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

## Start PostgreSQL

1. Make sure PostgreSQL is running.
2. Create a database named `nutsdb`.
   ```sql
   CREATE DATABASE nutsdb;
   ```
3. Ensure your credentials match those in `application.properties`.

## Start RabbitMQ

1. Make sure RabbitMQ is installed and running on your machine.
2. Open the Management UI (optional):
   - Navigate to: http://localhost:15672
   - Login: `guest` / `guest`
3. Create a queue named `nutsQueue`:
   - Go to "Queues" → Add queue → Name: `nutsQueue`

---

## Run the Application

Running NutsSubscriberApplication 

Once your application is running, go to the Queues tab → click nutsQueue → go to Publish message, enter a payload (e.g. Hello from RabbitMQ UI!), and click Publish Message. Your app will receive the message and store it in the database.


## Summary Architecture
```

+------------------+       +---------------+       +-----------------------+
| MessageSender    | --->  | RabbitMQ      | --->  | MessageListener      |
| (producer)       |       | (nutsQueue)   |       | MessageService       |
|                  |       |               |       | PostgreSQL persistence|
+------------------+       +---------------+       +-----------------------+
```

## Author & Submission

Project: Nuts Service Subscriber

Prepared for: Software Engineering Course

Developed by: Laura Baldryan

## Questions?
If you have any issues running the project, feel free to open an issue or comment in the GitHub repo.



