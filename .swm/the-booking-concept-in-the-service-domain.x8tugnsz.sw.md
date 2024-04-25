---
title: The Booking Concept in the Service Domain
---
This document will cover the concept of 'Booking' within the MyHome project. We'll cover:

1. What is 'Booking' in the context of MyHome
2. The main classes and functions related to 'Booking'

# What is 'Booking' in the context of MyHome

In the MyHome project, 'Booking' refers to the reservation of an amenity by a user. This is represented by the `AmenityBookingItem` class, which contains information about the booking, such as the start and end dates, the user who made the booking, and the amenity that was booked.

<SwmSnippet path="/service/src/main/java/com/myhome/domain/AmenityBookingItem.java" line="24">

---

# Main classes and functions related to 'Booking'

The `AmenityBookingItem` class is the main class related to 'Booking'. It contains fields such as `amenityBookingItemId`, `amenity`, `bookingStartDate`, `bookingEndDate`, and `bookingUser` which represent the unique ID of the booking, the amenity that was booked, the start and end dates of the booking, and the user who made the booking, respectively.

```java
@Entity
@AllArgsConstructor
@NoArgsConstructor
@EqualsAndHashCode(callSuper = false, of = {"amenityBookingItemId"})
@Getter
@Setter
@With
@NamedEntityGraphs({
    @NamedEntityGraph(
        name = "AmenityBookingItem.amenity",
        attributeNodes = {
            @NamedAttributeNode("amenity"),
        }),
    @NamedEntityGraph(
        name = "AmenityBookingItem.bookingUser",
        attributeNodes = {
            @NamedAttributeNode("bookingUser"),
        })
})

public class AmenityBookingItem extends BaseEntity {
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/BookingSDJpaService.java" line="19">

---

The `deleteBooking` function in the `BookingSDJpaService` class is an example of a function related to 'Booking'. It deletes a booking based on the amenity ID and booking ID.

```java
  public boolean deleteBooking(String amenityId, String bookingId) {
    Optional<AmenityBookingItem> booking =
        bookingRepository.findByAmenityBookingItemId(bookingId);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
