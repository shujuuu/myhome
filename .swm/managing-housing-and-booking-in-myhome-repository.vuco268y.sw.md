---
title: Managing Housing and Booking in the 'myhome' Repository
---
# Managing Housing and Booking in the 'myhome' Repository

## Intro

This document provides an overview of how housing and booking are managed in the 'myhome' repository. The details provided here are based on the repository's code and the file [FEATURES.md](https://github.com/swimmio/myhome/blob/0927c2518bef40a70ec546a6195056ee4eda28d2/assets/FEATURES.md#L1-L71).

## Features

The 'myhome' repository facilitates the following functionalities:

1. **House Management**: Houses can be added to a community and community admins can add members to a house. This is marked as completed.

2. **Amenity Management**: Community admins can add amenities to a community. This is marked as completed.

3. **Amenity Booking Management**: House members should be able to book amenities for a time slot and delete a future booking. The status of this feature is not clearly indicated in the features list.

## Implementation

The Java files in the repository provide more specific details on how these functionalities are implemented:

- <SwmPath repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome" path="service/src/test/java/com/myhome/services/unit/BookingSDJpaServiceTest.java">`(myhome) service/src/test/java/com/myhome/services/unit/BookingSDJpaServiceTest.java`</SwmPath>, <SwmPath repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome" path="service/src/main/java/com/myhome/controllers/BookingController.java">`(myhome) service/src/main/java/com/myhome/controllers/BookingController.java`</SwmPath>, and <SwmPath repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome" path="service/src/test/java/com/myhome/controllers/BookingControllerTest.java">`(myhome) service/src/test/java/com/myhome/controllers/BookingControllerTest.java`</SwmPath> files demonstrate how bookings are managed. The `deleteBooking()` function in <SwmPath repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome" path="service/src/main/java/com/myhome/services/springdatajpa/BookingSDJpaService.java">`(myhome) service/src/main/java/com/myhome/services/springdatajpa/BookingSDJpaService.java`</SwmPath> deletes a booking by its amenity and booking IDs.

- <SwmPath repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome" path="service/src/main/java/com/myhome/domain/Amenity.java">`(myhome) service/src/main/java/com/myhome/domain/Amenity.java`</SwmPath> is an entity class that represents an amenity, including its ID, name, description, price, community, community house, and booking items.

## Summary

This document has provided an overview of the management of housing and booking in the 'myhome' repository. For more detailed information, refer to the respective Java files in the repository.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
