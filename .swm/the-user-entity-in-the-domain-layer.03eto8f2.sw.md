---
title: The User Entity in the Domain Layer
---
This document will cover the 'User' entity in the MyHome project. We'll cover:

1. What is a 'User' in the context of the MyHome project
2. The main classes and fields related to 'User'

<SwmSnippet path="/service/src/main/java/com/myhome/domain/User.java" line="64">

---

# What is a 'User'

The 'User' class is a core entity in the MyHome project. It extends the 'BaseEntity' class and includes fields such as 'name', 'userId', 'email', 'encryptedPassword', and relationships with 'Community' and 'SecurityToken'.

```java
public class User extends BaseEntity {
  @Column(nullable = false)
  private String name;
  @Column(unique = true, nullable = false)
  private String userId;
  @Column(unique = true, nullable = false)
  private String email;
  @Column(nullable = false)
  private boolean emailConfirmed = false;
  @Column(nullable = false)
  private String encryptedPassword;
  @ManyToMany(mappedBy = "admins", fetch = FetchType.LAZY)
  private Set<Community> communities = new HashSet<>();
  @OneToMany(fetch = FetchType.LAZY, cascade = CascadeType.ALL, mappedBy = "tokenOwner")
  private Set<SecurityToken> userTokens = new HashSet<>();
}
```

---

</SwmSnippet>

# Main classes and fields related to 'User'

The 'User' entity is referenced in several other classes in the project. For instance, it's referenced as 'bookingUser' in the 'AmenityBookingItem' class, as 'admin' in the 'Payment' class, and as 'tokenOwner' in the 'SecurityToken' class. It's also part of a many-to-many relationship with the 'Community' class, where it's referenced as 'admins'.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
