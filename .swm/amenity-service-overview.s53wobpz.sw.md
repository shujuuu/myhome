---
title: Amenity Service Overview
---
This document will cover the Amenity Service in the MyHome project. We'll cover:

1. What is the Amenity Service
2. Where the Amenity Service is implemented
3. The main classes/functions/files related to the Amenity Service

<SwmSnippet path="/service/src/main/java/com/myhome/services/AmenityService.java" line="25">

---

# What is the Amenity Service

The `AmenityService` is an interface that defines the operations related to amenities. These operations include creating amenities, getting amenity details, deleting an amenity, listing all amenities, and updating an amenity.

```java
public interface AmenityService {

  Optional<List<AmenityDto>> createAmenities(Set<AmenityDto> amenities, String communityId);

  Optional<Amenity> getAmenityDetails(String amenityId);

  boolean deleteAmenity(String amenityId);

  Set<Amenity> listAllAmenities(String communityId);

  boolean updateAmenity(AmenityDto updatedAmenityDto);
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/AmenitySDJpaService.java" line="37">

---

# Where the Amenity Service is implemented

`AmenityService` is implemented in `AmenitySDJpaService` class. This class provides the concrete implementation of the operations defined in the `AmenityService` interface.

```java
public class AmenitySDJpaService implements AmenityService {

  private final AmenityRepository amenityRepository;
  private final CommunityRepository communityRepository;
  private final CommunityService communityService;
  private final AmenityApiMapper amenityApiMapper;

  @Override
  public Optional<List<AmenityDto>> createAmenities(Set<AmenityDto> amenities, String communityId) {
    final Optional<Community> community = communityService.getCommunityDetailsById(communityId);
    if (!community.isPresent()) {
      return Optional.empty();
    }
    final List<Amenity> amenitiesWithCommunity = amenities.stream()
        .map(amenityApiMapper::amenityDtoToAmenity)
        .map(amenity -> {
          amenity.setCommunity(community.get());
          return amenity;
        })
        .collect(Collectors.toList());
    final List<AmenityDto> createdAmenities =
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/AmenityController.java" line="43">

---

# The main classes/functions/files related to the Amenity Service

`AmenityService` is used in `AmenityController` class. This class uses the `AmenityService` to perform operations on amenities.

```java
  private final AmenityService amenitySDJpaService;
  private final AmenityApiMapper amenityApiMapper;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
