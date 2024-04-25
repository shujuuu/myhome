---
title: Understanding the AmenityController in MyHome Repository
---
# Understanding the AmenityController in MyHome Repository

## Introduction

This document provides a detailed overview of the `AmenityController` class in the `myhome` service repository. It discusses its definition, usage, and code implementation.

## Definition and Usage

The `AmenityController` is defined in the file [AmenityController.java](https://github.com/swimmio/myhome/blob/a0e3d861e5f3e2d4918e0973b66ff0b7fa45ee73/service/src/main/java/com/myhome/controllers/AmenityController.java). It implements the `AmenitiesApi` interface and provides methods for getting amenity details, listing all amenities, adding amenities to a community, deleting an amenity, and updating an amenity.

The `AmenityController` is used in various parts of the system such as:

- [AmenityApiMapper.java](https://github.com/swimmio/myhome/blob/a0e3d861e5f3e2d4918e0973b66ff0b7fa45ee73/service/src/main/java/com/myhome/controllers/mapper/AmenityApiMapper.java)
- [AmenityDto.java](https://github.com/swimmio/myhome/blob/a0e3d861e5f3e2d4918e0973b66ff0b7fa45ee73/service/src/main/java/com/myhome/controllers/dto/AmenityDto.java)
- [BookingController.java](https://github.com/swimmio/myhome/blob/a0e3d861e5f3e2d4918e0973b66ff0b7fa45ee73/service/src/main/java/com/myhome/controllers/BookingController.java)
- [AmenitySDJpaService.java](https://github.com/swimmio/myhome/blob/a0e3d861e5f3e2d4918e0973b66ff0b7fa45ee73/service/src/main/java/com/myhome/services/springdatajpa/AmenitySDJpaService.java)

## Code Implementation

Below is part of the code where `AmenityController` is defined:

<SwmSnippet path="service/src/main/java/com/myhome/controllers/BookingController.java" line="12" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome">

---

&nbsp;

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

The `AmenityService` and `AmenityApiMapper` are injected as dependencies in the `AmenityController`. There is also a test class for `AmenityController` defined in [AmenityControllerTest.java](https://github.com/swimmio/myhome/blob/a0e3d861e5f3e2d4918e0973b66ff0b7fa45ee73/service/src/test/java/com/myhome/controllers/AmenityControllerTest.java).

## Summary

The `AmenityController` plays a crucial role in managing amenity data in the `myhome` service repository. It is defined in the <SwmPath repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome" path="service/src/main/java/com/myhome/controllers/AmenityController.java">`(myhome) service/src/main/java/com/myhome/controllers/AmenityController.java`</SwmPath> file and is used in numerous parts of the system. The understanding of this class is essential for managing amenity related operations.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
