---
title: Mail Controller Overview
---
This document will cover the Mail Controller in the MyHome project. We'll cover:

1. What is the Mail Controller
2. The main classes/functions/files that are related to the Mail Controller

# What is the Mail Controller

The Mail Controller in the MyHome project is responsible for handling email-related functionalities. It is implemented in the UserController class, which is part of the `com.myhome.controllers` package. The UserController class contains methods such as `resendConfirmEmailMail` and `confirmEmail` which are related to email confirmation process.

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/UserController.java" line="126">

---

# Main classes/functions/files related to Mail Controller

The `confirmEmail` and `resendConfirmEmailMail` methods in the UserController class are part of the Mail Controller. The `confirmEmail` method is used to confirm the user's email, while the `resendConfirmEmailMail` method is used to resend the confirmation email to the user.

```java
  @Override
  public ResponseEntity<Void> confirmEmail(String userId, String emailConfirmToken) {
    boolean emailConfirmed = userService.confirmEmail(userId, emailConfirmToken);
    if(emailConfirmed) {
      return ResponseEntity.ok().build();
    } else {
      return ResponseEntity.badRequest().build();
    }
  }

  @Override
  public ResponseEntity<Void> resendConfirmEmailMail(String userId) {
    boolean emailConfirmResend = userService.resendEmailConfirm(userId);
    if(emailConfirmResend) {
      return ResponseEntity.ok().build();
    } else {
      return ResponseEntity.badRequest().build();
    }
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
