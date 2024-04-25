---
title: Project structure
---
# Project structure

Welcome to the MyHome repository. This project is designed to assist with apartment management. It's built using Gradle, Java 8, Docker, and React. The repository is structured into several packages, each with a specific purpose. From handling HTTP requests to managing data access and security, each package plays a crucial role in the functionality of the project. Additionally, the project supports multiple languages, with localized data stored in the resources files. This document will guide you through each package and its role in the project.

### Configuration `(service/src/main/java/com/myhome/configuration)`

This package contains the configuration files and settings.

### Controllers `(service/src/main/java/com/myhome/controllers)`

These classes handle HTTP requests and define the endpoints for managing different entities.

### Domain `(service/src/main/java/com/myhome/domain)`

This package contains the domain models and logic for apartment management.

### Repositories `(service/src/main/java/com/myhome/repositories)`

These packages contain the data access logic for apartment management.

### Security `(service/src/main/java/com/myhome/security)`

This package handles security-related functionality.

### Services `(service/src/main/java/com/myhome/services)`

This package contains the service layer for apartment management.

### Resources `(service/src/main/resources/locales)`

These files contain localized data for different languages used in the project.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
