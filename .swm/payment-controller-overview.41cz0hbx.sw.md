---
title: Payment Controller Overview
---
This document will cover the Payment Controller in the MyHome project. We'll cover:

1. What is the Payment Controller
2. The main classes/functions/files that are related to the Payment Controller

# What is the Payment Controller

The `PaymentController` is a REST Controller which provides endpoints for managing payments. It is located in the `com.myhome.controllers` package. The controller is responsible for handling payment-related requests such as scheduling payments, listing payment details, listing all member payments, and listing all admin scheduled payments.

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/PaymentController.java" line="51">

---

# Main classes/functions/files related to Payment Controller

This is the `PaymentController` class. It contains several methods such as `schedulePayment`, `listPaymentDetails`, `listAllMemberPayments`, and `listAllAdminScheduledPayments`. These methods handle different types of payment-related requests. The `PaymentController` class uses `PaymentService`, `CommunityService`, and `SchedulePaymentApiMapper` to perform its operations.

```java
@RestController
@RequiredArgsConstructor
@Slf4j
public class PaymentController implements PaymentsApi {
  private final PaymentService paymentService;
  private final CommunityService communityService;
  private final SchedulePaymentApiMapper schedulePaymentApiMapper;

  @Override
  public ResponseEntity<SchedulePaymentResponse> schedulePayment(@Valid
      SchedulePaymentRequest request) {
    log.trace("Received schedule payment request");

    HouseMember houseMember = paymentService.getHouseMember(request.getMemberId())
        .orElseThrow(() -> new RuntimeException(
            "House member with given id not exists: " + request.getMemberId()));
    User admin = communityService.findCommunityAdminById(request.getAdminId())
        .orElseThrow(
            () -> new RuntimeException("Admin with given id not exists: " + request.getAdminId()));

    if (isUserAdminOfCommunityHouse(houseMember.getCommunityHouse(), admin)) {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
