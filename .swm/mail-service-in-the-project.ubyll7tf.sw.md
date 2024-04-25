---
title: Mail Service in the Project
---
This document will cover the Mail Service in the MyHome project. We'll cover:

1. What is the Mail Service
2. Where the Mail Service is implemented
3. Main classes and functions related to the Mail Service

<SwmSnippet path="/service/src/main/java/com/myhome/services/MailService.java" line="6">

---

# What is the Mail Service

The `MailService` is an interface that defines methods for sending different types of emails, such as password recovery, account creation, password change, and account confirmation.

```java
public interface MailService {

  boolean sendPasswordRecoverCode(User user, String randomCode);

  boolean sendAccountCreated(User user, SecurityToken emailConfirmToken);

  boolean sendPasswordSuccessfullyChanged(User user);

  boolean sendAccountConfirmed(User user);
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/MailSDJpaService.java" line="30">

---

# Where the Mail Service is implemented

`MailService` is implemented in `MailSDJpaService` class. This class provides the actual implementation of the methods defined in the `MailService` interface. It uses the `JavaMailSender` to send emails and `ITemplateEngine` to process the email templates.

```java
public class MailSDJpaService implements MailService {

  private final ITemplateEngine emailTemplateEngine;
  private final JavaMailSender mailSender;
  private final ResourceBundleMessageSource messageSource;
  private final MailProperties mailProperties;

  @Override
  public boolean sendPasswordRecoverCode(User user, String randomCode) {
    Map<String, Object> templateModel = new HashMap<>();
    templateModel.put("username", user.getName());
    templateModel.put("recoverCode", randomCode);
    String passwordRecoverSubject = getLocalizedMessage("locale.EmailSubject.passwordRecover");
    boolean mailSent = send(user.getEmail(), passwordRecoverSubject,
        MailTemplatesNames.PASSWORD_RESET.filename, templateModel);
    return mailSent;
  }

  @Override
  public boolean sendPasswordSuccessfullyChanged(User user) {
    Map<String, Object> templateModel = new HashMap<>();
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/DevMailSDJpaService.java" line="14">

---

# Main classes and functions related to the Mail Service

`DevMailSDJpaService` is another implementation of `MailService` used for development purposes. It logs the email sending actions instead of actually sending emails.

```java
public class DevMailSDJpaService implements MailService {

  @Override
  public boolean sendPasswordRecoverCode(User user, String randomCode) throws MailSendException {
    log.info(String.format("Password recover code sent to user with id= %s, code=%s", user.getUserId()), randomCode);
    return true;
  }

  @Override
  public boolean sendAccountConfirmed(User user) {
    log.info(String.format("Account confirmed message sent to user with id=%s", user.getUserId()));
    return true;
  }

  @Override
  public boolean sendPasswordSuccessfullyChanged(User user) {
    log.info(String.format("Password successfully changed message sent to user with id=%s", user.getUserId()));
    return true;
  }


```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
