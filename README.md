# DevOps Lab – CI/CD Pipeline Lab Assessment

**Question Set G: Prerequisite Equivalence**

## 1. Project Overview

This project enhances the supplied Course Registration application using Git, Maven, JUnit 5, and Jenkins Declarative Pipeline. It also demonstrates Nginx deployment, scaling, and self-healing using Kubernetes and Minikube.

## 2. Project Structure

```text
course-registration/
├── pom.xml
├── Jenkinsfile
├── README.md
├── deployment.yaml
├── service.yaml
└── course-registration-app/
    ├── pom.xml
    └── src/
        ├── main/java/
        └── test/java/
```

## 3. Git Workflow

A feature branch is used to implement the changes with meaningful commits.

```bash
git branch
git log --oneline --graph --decorate
git status
```

The completed changes are integrated into the `main` branch. The working tree is verified to ensure that no unintended changes remain.

## 4. Maven Build and Testing

The project is organized as a multi-module Maven project. The root POM defines shared properties, dependency management, and the application module. The child POM inherits the parent configuration and declares JUnit 5 dependencies.

The Maven Compiler Plugin and Surefire Plugin are configured for Java compilation and automated JUnit 5 testing.

Build and test commands:

```bash
mvn clean test
mvn package
```

The packaged JAR and test reports are generated under `course-registration-app/target/` and `course-registration-app/target/surefire-reports/`, respectively.

**Test results:** Tests run: `<actual count>`, Failures: `<actual count>`, Errors: `<actual count>`, Skipped: `<actual count>`.

## 5. Capacity Boundary Defect

The registration-capacity validation is corrected to reject registrations when a course is full while allowing registration when exactly one seat remains.

JUnit 5 tests verify both scenarios and ensure rejected registrations do not modify student registration or credit state, or the course enrollment count. Existing tests are preserved and executed alongside the new tests.

## 6. Prerequisite Equivalence

For courses requiring `CS301`, completion of either `CS301` or `CS3A1` satisfies the prerequisite.

JUnit 5 tests cover:

- Registration acceptance when `CS301` is completed.
- Registration acceptance when `CS3A1` is completed.
- Registration rejection when neither prerequisite is completed.

Rejected registrations must not modify student registration or course enrollment state. The equivalence rule applies only to prerequisite validation and does not globally change course-code identity or duplicate-registration rules.

## 7. Jenkins Declarative Pipeline

The `Jenkinsfile` automates the following stages:

1. Source checkout.
2. Maven build and test.
3. Application packaging.
4. JUnit test report publication.
5. Artifact archiving.

Maven commands execute from the repository root. The pipeline uses the following paths:

- **Artifacts:** `course-registration-app/target/*.jar`
- **JUnit reports:** `course-registration-app/target/surefire-reports/TEST-*.xml`

Packaging and artifact archiving are prevented when the test stage fails. The pipeline targets the configured Windows or Linux Jenkins agent using the appropriate command steps.

## 8. Kubernetes Deployment Using Minikube

The Nginx application is deployed using `nginx:1.27` with two initial replicas. The Deployment uses appropriate labels and selectors, and a NodePort Service exposes the application.

The following operations are performed:

- Deploy Nginx using `deployment.yaml`.
- Expose the application using `service.yaml`.
- Verify Pod status, Service configuration, and application accessibility.
- Scale the Deployment from two to three replicas.
- Delete a running Pod and verify that Kubernetes creates a replacement.

The Deployment controller maintains the desired replica count by creating replacement Pods when managed Pods are deleted.

## 9. Conclusion

The project demonstrates Git-based development, Maven multi-module configuration, JUnit 5 testing, defect correction, prerequisite validation, CI pipeline automation, and Kubernetes deployment management. Existing application functionality and registration rules are preserved while the required changes are implemented.

