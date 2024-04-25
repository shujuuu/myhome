---
title: Authentication Service Overview
---
This document will cover the Authentication Service in the MyHome project. We'll cover:

1. What is the Authentication Service
2. Main classes and functions related to the Authentication Service

<SwmSnippet path="/service/src/main/java/com/myhome/services/AuthenticationService.java" line="6">

---

# What is the Authentication Service

The `AuthenticationService` is an interface that defines the `login` method. This method takes a `LoginRequest` as an argument and returns an `AuthenticationData` object.

```java
public interface AuthenticationService {
  AuthenticationData login(LoginRequest loginRequest);
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/AuthenticationSDJpaService.java" line="20">

---

# Main classes and functions related to the Authentication Service

`AuthenticationSDJpaService` is a class that implements the `AuthenticationService` interface. It contains the `login` method which is responsible for authenticating the user. The `login` method first finds the user by email, checks if the password matches, creates a JWT token, encodes it, and finally returns an `AuthenticationData` object.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
