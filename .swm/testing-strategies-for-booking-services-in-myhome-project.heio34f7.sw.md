---
title: Testing Strategies for Booking Services in MyHome Project
---
This document will cover the testing of services associated with 'Booking' in the MyHome project. We'll cover:

1. The role of the BookingService interface
2. The implementation of BookingService in BookingSDJpaService
3. The usage of BookingService in BookingController
4. The testing of BookingService in BookingControllerTest and BookingSDJpaServiceTest.

<SwmSnippet path="/service/src/main/java/com/myhome/services/BookingService.java" line="3">

---

# The role of the BookingService interface

The BookingService interface defines the contract for any class that wants to provide booking services. It declares a method `deleteBooking` which takes an amenityId and a bookingId as parameters.

```java
public interface BookingService {

  boolean deleteBooking(String amenityId, String bookingId);

}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/BookingSDJpaService.java" line="11">

---

# The implementation of BookingService in BookingSDJpaService

The BookingSDJpaService class implements the BookingService interface. It provides a concrete implementation of the `deleteBooking` method. This method uses the `AmenityBookingItemRepository` to find the booking by its id and deletes it if it belongs to the provided amenity.

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

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/BookingController.java" line="12">

---

# The usage of BookingService in BookingController

The BookingController class uses the BookingService to handle HTTP requests related to bookings. In the `deleteBooking` method, it calls the `deleteBooking` method of the BookingService and returns an appropriate HTTP response based on the result.

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

<SwmSnippet path="/service/src/test/java/com/myhome/controllers/BookingControllerTest.java" line="1">

---

# The testing of BookingService

The BookingControllerTest class contains unit tests for the BookingController. It tests the `deleteBooking` method among others. Similarly, the BookingSDJpaServiceTest class contains unit tests for the BookingSDJpaService.

```java
package com.myhome.controllers;

import com.myhome.services.BookingService;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertNull;
import static org.mockito.BDDMockito.given;
import static org.mockito.Mockito.verify;

public class BookingControllerTest {

  private final String TEST_AMENITY_ID = "test-amenity-id";
  private static final String TEST_BOOKING_ID = "test-booking-id";

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
