---
title: The House Controller
---
This document will cover the House Controller in the MyHome project. We'll cover:

1. What is the House Controller
2. The main classes/functions/files that are related to House Controller

# What is the House Controller

The House Controller is a class in the MyHome project that handles the API endpoints related to houses. It is responsible for managing the house-related operations such as listing all houses, getting house details, listing all members of a house, adding house members, and deleting a house member.

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/HouseController.java" line="43">

---

# Main classes/functions/files related to House Controller

This is the HouseController class. It implements the HousesApi interface and contains methods for handling house-related operations. It uses instances of HouseMemberMapper, HouseService, and HouseApiMapper to perform its tasks.

```java
@RestController
@RequiredArgsConstructor
@Slf4j
public class HouseController implements HousesApi {
  private final HouseMemberMapper houseMemberMapper;
  private final HouseService houseService;
  private final HouseApiMapper houseApiMapper;

  @Override
  public ResponseEntity<GetHouseDetailsResponse> listAllHouses(
      @PageableDefault(size = 200) Pageable pageable) {
    log.trace("Received request to list all houses");

    Set<CommunityHouse> houseDetails =
        houseService.listAllHouses(pageable);
    Set<GetHouseDetailsResponseCommunityHouse> getHouseDetailsResponseSet =
        houseApiMapper.communityHouseSetToRestApiResponseCommunityHouseSet(houseDetails);

    GetHouseDetailsResponse response = new GetHouseDetailsResponse();

    response.setHouses(getHouseDetailsResponseSet);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
