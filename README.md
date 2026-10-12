# Student Course Registration System

## Project Overview

This project implements a Java-based course registration system using Maven. It validates course capacity, student credit limits, course activity, duplicate registrations, and prerequisites.

## Project Structure

The project uses a Maven multi-module structure.

- `pom.xml` — Parent POM that manages the child module, Java compiler configuration, and shared JUnit version.
- `course-registration-app/pom.xml` — Child POM that defines the application artifact and test dependency.
- `course-registration-app/src/main/java/` — Application source code.
- `course-registration-app/src/test/java/` — JUnit test cases.
- `course-registration-app/target/` — Generated build output, test reports, and JAR artifact.

## Technology Stack

- Java 17
- Apache Maven
- JUnit 5

## Dependency Management

The parent POM declares the JUnit Jupiter version in its `dependencyManagement` section. The child module declares the JUnit Jupiter dependency without specifying the version again.

The parent POM manages the Maven Compiler and Surefire plugin versions. The compiler is configured for Java 17, and Surefire executes the JUnit 5 tests.

## Build and Test Instructions

Run the following commands from the repository root.

### Run tests

```bash
mvn clean test
```

### Package the application

```bash
mvn package
```

Maven builds the parent project and the `course-registration-app` child module through its reactor.

## Test Results

Verified on October 13, 2026:

- CourseTest: 3 tests
- RegistrationServiceTest: 11 tests
- Total: 14 tests
- Failures: 0
- Errors: 0
- Skipped: 0
- Build result: BUILD SUCCESS

## Build Artifact

The generated JAR is located at:

`course-registration-app/target/course-registration-app-1.0-SNAPSHOT.jar`

## Continuous Integration

The Jenkins Declarative Pipeline should run the Maven build from the repository root. JUnit reports and the packaged JAR must be collected from the child module's `target` directory.

- Test reports: `course-registration-app/target/surefire-reports/TEST-*.xml`
- JAR artifacts: `course-registration-app/target/*.jar`
