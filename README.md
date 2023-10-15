# integration-test-wiremock
This repository contains an example integration test project for a microservice API built with Spring Boot, utilizing WireMock to facilitate integration testing. This README will explain what WireMock is, how it works with Spring Boot, and the advantages it offers for integration testing in detail.

## Table of Contents
- [Introduction](#introduction)
- [What is WireMock?](#what-is-wiremock)
- [How WireMock Works with Spring Boot](#how-wiremock-works-with-spring-boot)
- [Advantages of Using WireMock for Integration Testing](#advantages-of-using-wiremock-for-integration-testing)
- [Getting Started](#getting-started)
- [Writing Integration Tests with WireMock](#writing-integration-tests-with-wiremock)
- [Running Integration Tests](#running-integration-tests)
- [License](#license)

## Introduction

Integration testing is an essential part of the software development process, especially when working with microservice architectures. It ensures that all components of a system interact correctly. WireMock is a powerful tool for simulating HTTP responses from external services, making it a valuable asset for integration testing in microservice environments.

## What is WireMock?

**WireMock** is a flexible and easy-to-use library for mocking HTTP-based services. It allows you to define and configure mock HTTP endpoints and their responses. It's commonly used for simulating API endpoints during testing. WireMock provides the ability to define expected HTTP request-response interactions, effectively mocking external services.
Key features of WireMock include:

- **Standalone Mock Server**: WireMock can be run as a standalone HTTP server that listens to specific ports.

- **Request Matching**: You can define precise request matching criteria, including URL patterns, HTTP methods, headers, query parameters, and request bodies.

- **Response Simulation**: You can simulate responses with custom status codes, headers, and response bodies. This enables you to mimic the behavior of external services in a controlled manner.

- **Record and Playback**: WireMock can record actual HTTP traffic and generate stub mappings from the recorded requests and responses, simplifying the creation of mocks.

## How WireMock Works with Spring Boot

WireMock can be seamlessly integrated into a Spring Boot application to facilitate integration testing. Here's how it works:

1. **Setting Up WireMock Server**: In your integration test class, you create a WireMock server instance, which can run on a specified port. This server acts as a mock external service.

   ```java
   @RunWith(SpringRunner.class)
   @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
   public class MyIntegrationTest {
       // ... other annotations and setup
       
       @ClassRule
       public static WireMockClassRule wireMockRule = new WireMockClassRule(WireMockSpring.options().port(8080));
   }
   ```

2. **Defining Expected Behavior**: You define the expected behavior of the mock service by configuring it to respond to specific HTTP requests.

   ```java
   @Test
   public void testMyMicroserviceWithWireMock() {
       wireMockRule.stubFor(WireMock.get(WireMock.urlPathEqualTo("/api/resource"))
           .willReturn(WireMock.aResponse()
               .withStatus(200)
               .withBody("Mocked Response")));
   
       // Perform the actual test using your microservice client.
   }
   ```

3. **Running Integration Tests**: When you run your integration tests, your Spring Boot application interacts with the WireMock server as if it were a real external service.

## Advantages of Using WireMock for Integration Testing

WireMock offers several advantages for integration testing in microservice environments:

1. **Isolation**: Tests are isolated from external services, ensuring that test results are consistent and not influenced by external factors like service outages or changes.

2. **Predictable Behavior**: You can define the expected behavior of the mock service, ensuring predictable and reproducible test outcomes.

3. **Speed**: WireMock is lightweight and runs locally, making it fast and suitable for running tests frequently during development.

4. **Edge Case Testing**: You can simulate edge cases and error scenarios, providing comprehensive test coverage that might be challenging to achieve with a real external service.

5. **Offline Testing**: You can develop and run tests even when the external service is unavailable or not accessible, allowing you to work offline.

6. **Test-Driven Development (TDD)**: WireMock supports a TDD approach, where you write tests based on expected external service behavior before the service is fully implemented.

By incorporating WireMock into your integration testing strategy, you can ensure that your microservice APIs interact correctly with external services, leading to more robust, reliable, and bug-free software.

## Getting Started

Before you get started, ensure you have the following prerequisites:

- Java Development Kit (JDK) 11 or later
- Maven
- Your Spring Boot microservice API to be tested

## Writing Integration Tests with WireMock

To write integration tests with WireMock, follow these steps:

1. Clone this repository to your local machine.

2. Navigate to the project directory and set up your test class as shown in the example.

3. Define the expected behavior for your mock service in your test methods.

4. Run your integration tests using `mvn test`.

## Running Integration Tests

To run your integration tests, navigate to the project's root directory and execute the following command:

```bash
mvn test
```
## License

...

Happy testing!
