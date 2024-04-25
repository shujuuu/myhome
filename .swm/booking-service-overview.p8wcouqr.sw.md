---
title: Booking Service Overview
---
This document will cover the Booking Service in the MyHome project. We'll cover:

1. What is the Booking Service
2. Where the Booking Service is implemented
3. The main classes/functions/files related to the Booking Service

<SwmSnippet path="/service/src/main/java/com/myhome/services/BookingService.java" line="3">

---

# What is the Booking Service

The `BookingService` is an interface that defines the contract for booking related operations. Currently, it only has one method `deleteBooking` which takes an amenityId and a bookingId as parameters.

```java
public interface BookingService {

  boolean deleteBooking(String amenityId, String bookingId);

}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/BookingSDJpaService.java" line="13">

---

# Where the Booking Service is implemented

`BookingService` is implemented in `BookingSDJpaService`. This class uses `AmenityBookingItemRepository` to perform database operations. The `deleteBooking` method is implemented here. It first finds the booking by its id and then checks if the amenity id matches. If it does, it deletes the booking and returns true, otherwise it returns false.

```java
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
  }
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/BookingController.java" line="17">

---

# Main classes/functions/files related to the Booking Service

`BookingService` is used in `BookingController`. The controller uses the service to perform operations related to bookings.

```java
  private final BookingService bookingSDJpaService;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
