---
title: Community Service in the Project
---
This document will cover the topic of 'Community Service' in the MyHome project. We'll cover:

1. What is 'Community Service' and where it is implemented.
2. The main classes/functions/files that are related to 'Community Service'.

<SwmSnippet path="/service/src/main/java/com/myhome/services/CommunityService.java" line="28">

---

# What is 'Community Service' and where it is implemented

`CommunityService` is an interface that defines the operations related to managing communities in the MyHome project. It includes methods for creating communities, listing all communities, getting community details, finding community houses and admins, adding admins and houses to a community, removing a house or an admin from a community, and deleting a community.

```java
public interface CommunityService {
  Community createCommunity(CommunityDto communityDto);

  Set<Community> listAll();

  Set<Community> listAll(Pageable pageable);

  Optional<Community> getCommunityDetailsById(String communityId);

  Optional<List<CommunityHouse>> findCommunityHousesById(String communityId, Pageable pageable);

  Optional<List<User>> findCommunityAdminsById(String communityId, Pageable pageable);

  Optional<User> findCommunityAdminById(String adminId);

  Optional<Community> getCommunityDetailsByIdWithAdmins(String communityId);

  Optional<Community> addAdminsToCommunity(String communityId, Set<String> admins);

  Set<String> addHousesToCommunity(String communityId, Set<CommunityHouse> houses);

```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/CommunitySDJpaService.java" line="46">

---

# The main classes/functions/files that are related to 'Community Service'

`CommunitySDJpaService` is a class that implements the `CommunityService` interface. It provides the concrete implementation of the methods defined in `CommunityService`. For example, the `createCommunity` method generates a unique ID for the new community, retrieves the current authenticated user as the admin, and saves the new community to the repository.

```java
public class CommunitySDJpaService implements CommunityService {
  private final CommunityRepository communityRepository;
  private final UserRepository communityAdminRepository;
  private final CommunityMapper communityMapper;
  private final CommunityHouseRepository communityHouseRepository;
  private final HouseService houseService;

  @Override
  public Community createCommunity(CommunityDto communityDto) {
    communityDto.setCommunityId(generateUniqueId());
    String userId = (String) SecurityContextHolder.getContext().getAuthentication().getPrincipal();
    Community community = addAdminToCommunity(communityMapper.communityDtoToCommunity(communityDto),
        userId);
    Community savedCommunity = communityRepository.save(community);
    log.trace("saved community with id[{}] to repository", savedCommunity.getId());
    return savedCommunity;
  }

  private Community addAdminToCommunity(Community community, String userId) {
    communityAdminRepository.findByUserIdWithCommunities(userId).ifPresent(admin -> {
      admin.getCommunities().add(community);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
