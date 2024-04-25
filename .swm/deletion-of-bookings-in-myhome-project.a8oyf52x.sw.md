---
title: Deletion of Bookings in MyHome Project
---
This document will cover the process of deleting bookings in the MyHome project. We'll cover:

1. The requirement for deleting bookings
2. The API endpoint for deleting bookings
3. The controller method for handling the delete request
4. The service method for deleting the booking from the database.

# Requirement for Deleting Bookings

The requirement for deleting bookings is defined in the MyHome Requirements Elicitation document. It states that house members should be able to delete a future booking.

<SwmSnippet path="/api/src/main/resources/public/swagger/api.yaml" line="135">

---

# API Endpoint for Deleting Bookings

The API endpoint for deleting bookings is defined in the Swagger API specification. The endpoint is `/amenities/{amenityId}/bookings/{bookingId}`, and it responds to the DELETE HTTP method.

```yaml
        '400':
          description: If amenity is not found
  /amenities/{amenityId}/bookings/{bookingId}:
    delete:
      security:
        - bearerAuth: [ ]
      tags:
        - Bookings
      description: Remove booking
      operationId: deleteBooking
      parameters:
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/BookingController.java" line="19">

---

# Controller Method for Handling the Delete Request

The `deleteBooking` method in the `BookingController` class handles the delete request. It calls the `deleteBooking` method of the `BookingService` to delete the booking. If the booking is successfully deleted, it returns a HTTP status of NO_CONTENT. If the booking is not found, it returns a HTTP status of NOT_FOUND.

```java
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
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/BookingSDJpaService.java" line="19">

---

# Service Method for Deleting the Booking from the Database

The `deleteBooking` method in the `BookingSDJpaService` class deletes the booking from the database. It first finds the booking by its ID using the `findByAmenityBookingItemId` method of the `AmenityBookingItemRepository`. If the booking is found and its amenity ID matches the provided amenity ID, it deletes the booking and returns true. If the booking is not found or the amenity ID does not match, it returns false.

```java
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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
