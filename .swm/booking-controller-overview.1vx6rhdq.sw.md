---
title: Booking Controller Overview
---
This document will cover the Booking Controller in the MyHome project. We'll cover:

1. What is the Booking Controller
2. The main classes/functions/files that are related to Booking Controller

# What is the Booking Controller

The `BookingController` is a class in the `com.myhome.controllers` package. It implements the `BookingsApi` interface and is responsible for handling booking-related requests. The controller uses the `BookingService` to perform operations related to bookings.

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/BookingController.java" line="12">

---

# Main classes/functions/files related to Booking Controller

The `BookingController` class is defined here. It has a `deleteBooking` method which deletes a booking based on the amenityId and bookingId. The deletion operation is performed by the `BookingService`.

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
