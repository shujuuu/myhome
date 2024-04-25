---
title: The Authentication Controller
---
This document will cover the Authentication Controller in the MyHome project. We'll cover:

1. What is the Authentication Controller
2. Main classes and methods related to the Authentication Controller

# What is the Authentication Controller

The `AuthenticationController` is a class in the `com.myhome.controllers` package. It implements the `AuthenticationApi` interface and is responsible for handling authentication requests. It uses the `AuthenticationService` to perform the actual authentication.

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/AuthenticationController.java" line="13">

---

# Main classes and methods related to the Authentication Controller

The `AuthenticationController` class contains the `login` method which is responsible for handling login requests. It takes a `LoginRequest` object as input and uses the `AuthenticationService` to perform the login. The result is an `AuthenticationData` object which contains the user's ID and JWT token. These are then added to the HTTP headers of the response.

```java
@RequiredArgsConstructor
@RestController
public class AuthenticationController implements AuthenticationApi {

  private final AuthenticationService authenticationService;

  @Override
  public ResponseEntity<Void> login(@Valid LoginRequest loginRequest) {
    final AuthenticationData authenticationData = authenticationService.login(loginRequest);
    return ResponseEntity.ok()
        .headers(createLoginHeaders(authenticationData))
        .build();
  }

  private HttpHeaders createLoginHeaders(AuthenticationData authenticationData) {
    final HttpHeaders httpHeaders = new HttpHeaders();
    httpHeaders.add("userId", authenticationData.getUserId());
    httpHeaders.add("token", authenticationData.getJwtToken());
    return httpHeaders;
  }
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
