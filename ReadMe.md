# Library Versioning with Nexus Artifactory

This repository demonstrates various library versioning patterns using Nexus Artifactory. It explores strategies for releasing test, staging, and production versions of Java libraries within a multi-module Maven project.

## Folder Structure
```
service-boot/
├── alpha-service/        # Example service module
│   ├── pom.xml
│   └── src/
├── auth-common/         # Authentication common library
│   ├── pom.xml
│   └── src/
├── container/           # Docker Compose and Nexus settings
│   ├── docker-compose.yaml
│   └── settings.xml
├── logging-common/      # Logging common library
│   ├── pom.xml
│   └── src/
└── tracking-common/     # Tracking common library
├── pom.xml
└── src/
```

## Project Overview

This project is structured as a multi-module Maven project, consisting of several common libraries and a service module.

-   **`alpha-service`**: A sample Spring Boot service that depends on the common libraries.
-   **`auth-common`**: A common library for authentication functionalities.
-   **`logging-common`**: A common library for logging functionalities.
-   **`tracking-common`**: A common library for tracking functionalities.
-   **`container`**: Contains Docker Compose configuration for setting up a local Nexus repository and Maven settings.

## Versioning Patterns Demonstrated

This repository explores the following versioning patterns:

-   **Snapshot Versions (`-SNAPSHOT`)**: For development and early testing.
-   **Release Versions**: For stable and production-ready libraries.
-   **Staging Versions**: For pre-release testing and validation.
-   **Semantic Versioning**: Adhering to `major.minor.patch` versioning.

## Usage

### Prerequisites

-   Docker and Docker Compose
-   Maven
-   Java Development Kit (JDK)

### Setup

1.  **Start Nexus Repository:**

    ```bash
    cd container
    docker-compose up -d
    ```

    This will start a local Nexus repository. Access the Nexus UI at `http://localhost:8081/`.
2.  **Configure Maven Settings:**

    Copy the `container/settings.xml` file to your Maven settings directory (`~/.m2/settings.xml`). This configures Maven to use the local Nexus repository.
    If you already have a settings.xml, merge the server section from the provided settings.xml to your own.
3.  **Build and Deploy Libraries:**

    Navigate to the root directory of the project (`service-boot`) and run the following Maven command to build and deploy the libraries:

    ```bash
    mvn clean deploy -DskipTests
    ```

    This will build the libraries and deploy them to the local Nexus repository.
4.  **Build and Run the Service:**

    Navigate to the `alpha-service` directory and build the service:

    ```bash
    cd alpha-service
    mvn clean package
    ```

    Run the service:

    ```bash
    java -jar target/alpha-service-*.jar
    ```

### Exploring Versions

-   **Snapshot Versions**: Observe the deployment of `-SNAPSHOT` versions in the Nexus repository.
-   **Release Versions**: Check the release versions (e.g., `1.0`, `1.5`, `2.0`, `3.0`) in the Nexus repository.
-   **Staging Versions**: You can modify the `pom.xml` files to experiment with staging versions (e.g., `1.0-rc.1`, `1.0-beta.1`).

## Notes

-   The `container/docker-compose.yaml` file sets up a basic Nexus repository. You may need to customize it for more advanced configurations.
-   The `container/settings.xml` file configures Maven to use the local Nexus repository. Ensure that the server credentials are correct.
-   The `pom.xml` files in the library modules demonstrate different versioning strategies. You can modify them to experiment with different patterns.
-   The `target` folders contain the generated jar files, and the structure of the maven build.

## Contributing

Feel free to contribute to this repository by submitting pull requests.

## License

This project is licensed under the [MIT License](LICENSE).
