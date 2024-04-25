---
title: Payment Service Overview
---
This document will cover the Payment Service in the MyHome project. We'll cover:

1. What is the Payment Service
2. Main classes and methods related to the Payment Service

<SwmSnippet path="/service/src/main/java/com/myhome/services/PaymentService.java" line="30">

---

# What is the Payment Service

The `PaymentService` is an interface that defines the contract for payment-related operations. It declares methods for scheduling payments, retrieving payment details, getting payments by member or admin, and getting house member details.

```java
public interface PaymentService {
  PaymentDto schedulePayment(PaymentDto request);

  Optional<PaymentDto> getPaymentDetails(String paymentId);

  Set<Payment> getPaymentsByMember(String memberId);

  Page<Payment> getPaymentsByAdmin(String adminId, Pageable pageable);

  Optional<HouseMember> getHouseMember(String memberId);
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/PaymentSDJpaService.java" line="47">

---

# Main classes and methods related to the Payment Service

`PaymentSDJpaService` is a class that implements the `PaymentService` interface. It uses the `PaymentRepository` to perform CRUD operations on the `Payment` entity. It also uses the `UserRepository` for operations related to the `User` entity and `HouseMemberRepository` for operations related to the `HouseMember` entity. The class contains methods for scheduling payments, retrieving payment details, getting payments by member or admin, and getting house member details.

```java
public class PaymentSDJpaService implements PaymentService {
  private final PaymentRepository paymentRepository;
  private final UserRepository adminRepository;
  private final PaymentMapper paymentMapper;
  private final HouseMemberRepository houseMemberRepository;

  @Override
  public PaymentDto schedulePayment(PaymentDto request) {
    generatePaymentId(request);
    return createPaymentInRepository(request);
  }

  @Override
  public Optional<PaymentDto> getPaymentDetails(String paymentId) {
    return paymentRepository.findByPaymentId(paymentId)
        .map(paymentMapper::paymentToPaymentDto);
  }

  @Override
  public Optional<HouseMember> getHouseMember(String memberId) {
    return houseMemberRepository.findByMemberId(memberId);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
