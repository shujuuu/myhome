---
title: Transactional Integrity of Booking Process in MyHome Project
---
This document will cover the transactionality of the 'Booking' process in the MyHome project. We'll cover:

1. The role of the `BookingSDJpaService` class
2. The use of the `@Transactional` annotation
3. The interaction between the `BookingController` and `BookingSDJpaService`.

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/BookingSDJpaService.java" line="11">

---

# The role of the `BookingSDJpaService` class

The `BookingSDJpaService` class implements the `BookingService` interface. It contains the `deleteBooking` method, which is responsible for deleting a booking. This method is annotated with `@Transactional`, indicating that it should be executed within a transaction context.

```java
@Service
@RequiredArgsConstructor
public class BookingSDJpaService implements BookingService {

  private final AmenityBookingItemRepository bookingRepository;

  @Transactional
  @Override
  public boolean deleteBooking(String amenityId, String bookingId) {
    Optional<AmenityBookingItem> booking =
        bookingRepository.findByAmenityBookingItemId(bookingId);
    return booking.map(bookingItem -> {
      boolean amenityFound =
          bookingItem.getAmenity().getAmenityId().equals(amenityId);
      if (amenityFound) {
        bookingRepository.delete(bookingItem);
        return true;
      } else {
        return false;
      }
    }).orElse(false);
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/BookingSDJpaService.java" line="17">

---

# The use of the `@Transactional` annotation

The `@Transactional` annotation is used to ensure that the `deleteBooking` operation is executed within a transaction. This means that if any part of the operation fails, all changes made within the transaction will be rolled back, ensuring data consistency.

```java
  @Transactional
  @Override
  public boolean deleteBooking(String amenityId, String bookingId) {
    Optional<AmenityBookingItem> booking =
        bookingRepository.findByAmenityBookingItemId(bookingId);
    return booking.map(bookingItem -> {
      boolean amenityFound =
          bookingItem.getAmenity().getAmenityId().equals(amenityId);
      if (amenityFound) {
        bookingRepository.delete(bookingItem);
        return true;
      } else {
        return false;
      }
    }).orElse(false);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/BookingController.java" line="12">

---

# The interaction between the `BookingController` and `BookingSDJpaService`

The `BookingController` class uses the `BookingService` to delete a booking. If the deletion is successful, it returns a `NO_CONTENT` status; otherwise, it returns a `NOT_FOUND` status. This operation is part of the transaction started in the `BookingSDJpaService`.

```java
@RestController
@Slf4j
@RequiredArgsConstructor
public class BookingController implements BookingsApi {

  private final BookingService bookingSDJpaService;

  @Override
  public ResponseEntity<Void> deleteBooking(@PathVariable String amenityId,
      @PathVariable String bookingId) {
    boolean isBookingDeleted = bookingSDJpaService.deleteBooking(amenityId, bookingId);
    if (isBookingDeleted) {
      return ResponseEntity.status(HttpStatus.NO_CONTENT).build();
    } else {
      return ResponseEntity.status(HttpStatus.NOT_FOUND).build();
    }
  }
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
