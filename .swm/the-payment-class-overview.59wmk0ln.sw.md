---
title: The Payment Class Overview
---
This document will cover the 'Payment' class in the MyHome project. We'll cover:

1. What is the 'Payment' class
2. The main fields and their purpose in the 'Payment' class
3. Where the 'Payment' class is implemented

<SwmSnippet path="/service/src/main/java/com/myhome/domain/Payment.java" line="31">

---

# What is the 'Payment' class

The 'Payment' class is an entity representing a payment in the service. This could be an electricity bill, house rent, water charge etc. It extends the 'BaseEntity' class and includes several fields such as 'paymentId', 'charge', 'type', 'description', 'recurring', 'dueDate', 'admin', and 'member'.

```java
/**
 * Entity identifying a payment in the service. This could be an electricity bill, house rent, water
 * charge etc
 */
@AllArgsConstructor
@NoArgsConstructor
@Data
@EqualsAndHashCode(callSuper = false)
@Entity
public class Payment extends BaseEntity {
  @Column(unique = true, nullable = false)
  private String paymentId;
  @Column(nullable = false)
  private BigDecimal charge;
  @Column(nullable = false)
  private String type;
  @Column(nullable = false)
  private String description;
  @Column(nullable = false)
  private boolean recurring;
  @JsonFormat(pattern = "yyyy-MM-dd")
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/domain/Payment.java" line="41">

---

# The main fields and their purpose in the 'Payment' class

The 'Payment' class includes several fields. 'paymentId' is a unique identifier for each payment. 'charge' represents the amount of the payment. 'type' and 'description' provide information about the payment. 'recurring' is a boolean indicating whether the payment is recurring or not. 'dueDate' is the date when the payment is due. 'admin' and 'member' are references to the user who is the admin and the house member associated with the payment respectively.

```java
  @Column(unique = true, nullable = false)
  private String paymentId;
  @Column(nullable = false)
  private BigDecimal charge;
  @Column(nullable = false)
  private String type;
  @Column(nullable = false)
  private String description;
  @Column(nullable = false)
  private boolean recurring;
  @JsonFormat(pattern = "yyyy-MM-dd")
  private LocalDate dueDate;
  @ManyToOne(fetch = FetchType.LAZY)
  private User admin;
  @ManyToOne(fetch = FetchType.LAZY)
  private HouseMember member;
```

---

</SwmSnippet>

# Where the 'Payment' class is implemented

The 'Payment' class is implemented in several places in the codebase. It is used in the 'PaymentController', 'PaymentService', 'PaymentRepository', 'PaymentMapper', 'PaymentSDJpaService', and 'SchedulePaymentApiMapper' classes.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
