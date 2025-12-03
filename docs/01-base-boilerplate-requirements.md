# Book publishing service

Create a backend service for a book publishing house.

The service should be able to manage authors and books via a protected API, as well as expose authors and books via a public API.

The source code of the service should be hosted on GitHub.

The build tool should be Gradle.

CI should be set up to build and test the project on every commit. The CI tool should be GitHub Actions.

The application should be containerized using Docker.

## CI/CD 

### Build

The pipeline should be triggered:
- On every commit to the `main` branch
- On every push to a branch which has a pull request opened against the `main` branch

The pipeline should:
- Build the project
- Run linters
- Run tests
- Generate JaCoCo coverage report
- Run OWASP dependency check
- Run SonarQube analysis
- Build snapshot Docker image
- Push Docker image to Docker Hub

### Release

The release should be triggered only on git tag creation on the `main` branch.

The pipeline should be triggered only if:
- A git tag was created on the `main` branch
- The tag has a semver format `v<MAJOR>.<MINOR>.<VERSION>`, e.g. `v1.5.3`

The pipeline should:
- Build the project
- Run linters
- Run tests
- Generate JaCoCo coverage report
- Run OWASP dependency check
- Run SonarQube analysis
- Build release Docker image
- Push Docker image to Docker Hub

## Features

### API

The API should be a REST API using HATEOAS. The protected API should be secured using OAuth 2.0.

#### Protected API

Define and document the following REST APIs.

Endpoints:
- Create author: limited to administrators
- Update author: limited to administrators
- Delete author: limited to administrators
- Create book: limited to administrators
- Publish book: limited to authors and administrators
- Delete book: limited to administrators

#### Public API

Define and document the following REST APIs.

Endpoints:
- Get author by ID
- Get all authors
- Get book by ISBN
- Get all books

#### Author API resource

Fields:
- Name
- Number of published books

By default, the API returns authors sorted by creation time (newest first).

The API supports returning authors sorted by number of published books.

One author can publish several books.

#### Book API resource

Fields:
- Title
- ISBN
- Genre

One book can be published by several authors.

By default, the API returns books sorted by publishing time (newest first).

Supports searching books by any of its attributes (title, ISBN, genre) or the author.

### Database schema

The database should be PostgreSQL. The database schema should be designed using the Entity-Relationship model.

Flyway should be used to manage database migrations.

The database should contain some generated seed data.

### Security

The service should be secured using OAuth 2.0.

The following scopes should be used:
- `author` - Author access, can publish books
- `admin` - Administrator access, can do all operations

### Tests

The service should have both unit and integration tests.

Integration tests should use the Spring Testcontainers library to run a PostgreSQL database in a Docker container.

## Technologies

Use the following technologies:

- Spring Boot
- Spring Web
- Spring Security
- Spring Data JPA
- PostgreSQL
- Flyway
- Docker
- GitHub Actions

## Documentation

Generate a README file with the following sections:
- Description of the project
- How to build and run the project
- Technologies used
- Database schema
- API documentation
