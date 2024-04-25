---
title: Community Controller Overview
---
This document will cover the Community Controller in the MyHome project. We'll cover:

1. What is the Community Controller
2. The main classes/functions/files that are related to the Community Controller

# What is the Community Controller

The `CommunityController` is a class in the `com.myhome.controllers` package. It implements the `CommunitiesApi` interface and is responsible for handling HTTP requests related to communities. It uses `CommunityService` for business logic and `CommunityApiMapper` for converting between DTOs and domain objects.

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/CommunityController.java" line="56">

---

# Main classes/functions/files related to Community Controller

The `CommunityController` class contains several methods for handling community-related requests. These include `createCommunity`, `listAllCommunity`, `listCommunityDetails`, `listCommunityAdmins`, `listCommunityHouses`, `addCommunityAdmins`, `addCommunityHouses`, and `removeCommunityHouse`. Each of these methods corresponds to a specific HTTP request and uses the `CommunityService` and `CommunityApiMapper` to process the request and generate a response.

```java
@RequiredArgsConstructor
@RestController
@Slf4j
public class CommunityController implements CommunitiesApi {
  private final CommunityService communityService;
  private final CommunityApiMapper communityApiMapper;

  @Override
  public ResponseEntity<CreateCommunityResponse> createCommunity(@Valid @RequestBody
      CreateCommunityRequest request) {
    log.trace("Received create community request");
    CommunityDto requestCommunityDto =
        communityApiMapper.createCommunityRequestToCommunityDto(request);
    Community createdCommunity = communityService.createCommunity(requestCommunityDto);
    CreateCommunityResponse createdCommunityResponse =
        communityApiMapper.communityToCreateCommunityResponse(createdCommunity);
    return ResponseEntity.status(HttpStatus.CREATED).body(createdCommunityResponse);
  }

  @Override
  public ResponseEntity<GetCommunityDetailsResponse> listAllCommunity(
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
