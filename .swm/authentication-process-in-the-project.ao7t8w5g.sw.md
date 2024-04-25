---
title: Authentication Process in the Project
---
This document will cover the authentication process in the MyHome project, specifically focusing on:

1. The structure and purpose of the `AuthenticationData` class.
2. The role of the `SecurityToken` class in the authentication process.
3. The involvement of the `User` class in authentication.

<SwmSnippet path="/service/src/main/java/com/myhome/domain/AuthenticationData.java" line="6">

---

# The `AuthenticationData` Class

The `AuthenticationData` class is a simple data holder that contains a JWT token and a user ID. This class is used to pass around authentication data within the application.

```java
@Getter
@RequiredArgsConstructor
public class AuthenticationData {
  private final String jwtToken;
  private final String userId;
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/domain/SecurityToken.java" line="15">

---

# The `SecurityToken` Class

The `SecurityToken` class represents a security token that is used in the authentication process. It contains information about the token type, the token itself, its creation and expiry dates, and the user it belongs to.

```java
@Entity
@Data
@AllArgsConstructor
@NoArgsConstructor
@ToString(exclude = {"tokenOwner"})
public class SecurityToken extends BaseEntity {
  @Column(nullable = false)
  @Enumerated(EnumType.STRING)
  private SecurityTokenType tokenType;
  @Column(nullable = false, unique = true)
  private String token;
  @Column(nullable = false)
  private LocalDate creationDate;
  @Column(nullable = false)
  private LocalDate expiryDate;
  private boolean isUsed;
  @ManyToOne
  private User tokenOwner;
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/domain/User.java" line="40">

---

# The `User` Class

The `User` class represents a user in the system. It contains information about the user's ID, email, password, and associated communities. This class is crucial in the authentication process as it is used to verify the user's credentials and determine their access rights.

```java
/**
 * Entity identifying a valid user in the service.
 */
@AllArgsConstructor
@Getter
@NoArgsConstructor
@Data
@EqualsAndHashCode(callSuper = false, of = {"userId", "email"})
@Entity
@With
@NamedEntityGraphs({
    @NamedEntityGraph(
        name = "User.communities",
        attributeNodes = {
            @NamedAttributeNode("communities"),
        }
    ),
    @NamedEntityGraph(
        name = "User.userTokens",
        attributeNodes = {
            @NamedAttributeNode("userTokens"),
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
