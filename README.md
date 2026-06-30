# Midas Core — JP Morgan Chase Virtual Work Experience

A backend transaction processing system built as part of the
JP Morgan Chase Software Engineering Virtual Experience on Forage.

## What I implemented

- **Kafka Consumer** (`TransactionListener.java`): Listens to incoming
  financial transactions on a Kafka topic, deserializes them, and
  processes them through a validation and persistence pipeline.

- **Transaction Validation & Persistence**: Validates each transaction
  against three rules (valid sender, valid recipient, sufficient balance),
  updates user balances atomically using Spring Data JPA, and persists
  approved transactions to an H2 in-memory database.

- **Incentive API Integration** (`IncentiveClient.java`): Posts validated
  transactions to an external REST API using Spring's RestTemplate,
  receives incentive amounts, and applies them to recipient balances.

- **Balance REST Endpoint** (`BalanceController.java`): Exposes a
  GET /balance endpoint on port 33400 that accepts a userId parameter
  and returns the user's current balance as JSON.

## Tech Stack

- Java 17
- Spring Boot 3.2.5
- Apache Kafka (embedded via spring-kafka-test)
- Spring Data JPA
- H2 In-Memory Database
- Spring Web (RestTemplate + REST Controller)
- Maven

## How to run

1. Start the Incentive API:
   ```
   java -jar services/transaction-incentive-api.jar
   ```
2. Run the Spring Boot application:
   ```
   mvn spring-boot:run
   ```
3. Query a user balance:
   ```
   GET http://localhost:33400/balance?userId=1
   ```

## Note

This project was completed as part of the
[JP Morgan Chase Software Engineering Virtual Experience](https://www.theforage.com/simulations/jpmorgan/software-engineering-5wud)
on Forage. The project skeleton and test suite were provided;
the implementation of all business logic was completed independently.