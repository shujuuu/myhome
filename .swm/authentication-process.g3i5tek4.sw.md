---
title: Authentication Process
---
This document will cover the Authentication process in the MyHome project, which includes:

1. Understanding the AuthenticationService interface
2. Implementation of AuthenticationService in AuthenticationSDJpaService
3. Usage of AuthenticationService in AuthenticationController.

<SwmSnippet path="/service/src/main/java/com/myhome/services/AuthenticationService.java" line="6">

---

# Understanding the AuthenticationService interface

`AuthenticationService` is an interface that defines the `login` method. This method takes a `LoginRequest` object as a parameter and returns an `AuthenticationData` object.

```java
public interface AuthenticationService {
  AuthenticationData login(LoginRequest loginRequest);
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/AuthenticationSDJpaService.java" line="20">

---

# Implementation of AuthenticationService in AuthenticationSDJpaService

`AuthenticationSDJpaService` is a class that implements the `AuthenticationService` interface. It provides the implementation for the `login` method. This method retrieves the user details, validates the password, creates a JWT token, and returns an `AuthenticationData` object.

```java
public class AuthenticationSDJpaService implements AuthenticationService {

  private final Duration tokenExpirationTime;
  private final String tokenSecret;

  private final UserSDJpaService userSDJpaService;
  private final AppJwtEncoderDecoder appJwtEncoderDecoder;
  private final PasswordEncoder passwordEncoder;

  public AuthenticationSDJpaService(@Value("${token.expiration_time}") Duration tokenExpirationTime,
      @Value("${token.secret}") String tokenSecret,
      UserSDJpaService userSDJpaService,
      AppJwtEncoderDecoder appJwtEncoderDecoder,
      PasswordEncoder passwordEncoder) {
    this.tokenExpirationTime = tokenExpirationTime;
    this.tokenSecret = tokenSecret;
    this.userSDJpaService = userSDJpaService;
    this.appJwtEncoderDecoder = appJwtEncoderDecoder;
    this.passwordEncoder = passwordEncoder;
  }

```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/AuthenticationController.java" line="17">

---

# Usage of AuthenticationService in AuthenticationController

`AuthenticationService` is used in `AuthenticationController`. The `AuthenticationController` class has a dependency on `AuthenticationService`.

```java
  private final AuthenticationService authenticationService;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
