---
title: Amenity Controller Overview
---
This document will cover the following aspects of the Amenity Controller in the MyHome project:

1. What is the Amenity Controller?
2. The main classes and methods related to the Amenity Controller.

# What is the Amenity Controller?

The `AmenityController` is a class in the `com.myhome.controllers` package. It is responsible for handling HTTP requests related to amenities in the application. It uses the `AmenityService` and `AmenityApiMapper` to perform operations and map the data to the required format.

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/AmenityController.java" line="38">

---

# Main classes and methods related to the Amenity Controller

The `AmenityController` class implements the `AmenitiesApi` interface. It has several methods to handle different types of requests such as `getAmenityDetails`, `listAllAmenities`, `addAmenityToCommunity`, `deleteAmenity`, and `updateAmenity`. Each of these methods interacts with the `AmenityService` to perform the necessary operations.

```java
@RestController
@Slf4j
@RequiredArgsConstructor
public class AmenityController implements AmenitiesApi {

  private final AmenityService amenitySDJpaService;
  private final AmenityApiMapper amenityApiMapper;

  @Override
  public ResponseEntity<GetAmenityDetailsResponse> getAmenityDetails(
      @PathVariable String amenityId) {
    return amenitySDJpaService.getAmenityDetails(amenityId)
        .map(amenityApiMapper::amenityToAmenityDetailsResponse)
        .map(ResponseEntity::ok)
        .orElse(ResponseEntity.status(HttpStatus.NOT_FOUND).build());
  }

  @Override
  public ResponseEntity<Set<GetAmenityDetailsResponse>> listAllAmenities(
      @PathVariable String communityId) {
    Set<Amenity> amenities = amenitySDJpaService.listAllAmenities(communityId);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
