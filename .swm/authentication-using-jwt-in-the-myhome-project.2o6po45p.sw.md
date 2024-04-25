---
title: Authentication Using JWT in the MyHome Project
---
This document will cover the following aspects of how the authentication process in the MyHome project aligns with the JSON Web Token (JWT) standard:

1. The structure of the JWT in the application.
2. The encoding and decoding of the JWT.
3. The usage of JWT in the authentication process.

<SwmSnippet path="/service/src/main/java/com/myhome/security/jwt/AppJwt.java" line="30">

---

# The structure of the JWT in the application

The `AppJwt` class represents a JWT in the application. It contains two fields: `userId` and `expiration`. The `userId` is used to identify the user, and `expiration` is used to set the validity period of the JWT.

```java
public class AppJwt {
  private final String userId;
  private final LocalDateTime expiration;
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/security/jwt/AppJwtEncoderDecoder.java" line="23">

---

# The encoding and decoding of the JWT

The `AppJwtEncoderDecoder` interface provides the logic to encode and decode the application's JWT. The `decode` method is used to decode the encoded JWT and the `encode` method is used to encode the JWT.

```java
  AppJwt decode(String encodedJwt, String secret);

  String encode(AppJwt jwt, String secret);
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/AuthenticationSDJpaService.java" line="49">

---

# The usage of JWT in the authentication process

In the authentication process, after the user is validated, a JWT is created and encoded. The `createJwt` method is used to create a JWT for the user, and the `encode` method of `AppJwtEncoderDecoder` is used to encode the JWT.

```java
    final AppJwt jwtToken = createJwt(userDto);
    final String encodedToken = appJwtEncoderDecoder.encode(jwtToken, tokenSecret);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
