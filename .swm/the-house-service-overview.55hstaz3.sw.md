---
title: The House Service Overview
---
This document will cover the 'House Service' in the MyHome project. We'll cover:

1. What is the 'House Service'
2. Main classes and functions related to 'House Service'

<SwmSnippet path="/service/src/main/java/com/myhome/services/HouseService.java" line="26">

---

# What is the 'House Service'

The 'House Service' is an interface that defines several methods related to house operations. These methods include listing all houses, adding house members, deleting a member from a house, getting house details by ID, and listing house members for houses of a specific user.

```java
public interface HouseService {
  Set<CommunityHouse> listAllHouses();

  Set<CommunityHouse> listAllHouses(Pageable pageable);

  Set<HouseMember> addHouseMembers(String houseId, Set<HouseMember> houseMembers);

  boolean deleteMemberFromHouse(String houseId, String memberId);

  Optional<CommunityHouse> getHouseDetailsById(String houseId);

  Optional<List<HouseMember>> getHouseMembersById(String houseId, Pageable pageable);

  Optional<List<HouseMember>> listHouseMembersForHousesOfUserId(String userId, Pageable pageable);
}
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/HouseSDJpaService.java" line="37">

---

# Main classes and functions related to 'House Service'

The 'HouseSDJpaService' class implements the 'HouseService' interface. It provides the concrete implementation of the methods defined in the 'HouseService' interface. This class interacts with the 'HouseMemberRepository' and 'CommunityHouseRepository' to perform operations on the house members and community houses.

```java
public class HouseSDJpaService implements HouseService {
  private final HouseMemberRepository houseMemberRepository;
  private final HouseMemberDocumentRepository houseMemberDocumentRepository;
  private final CommunityHouseRepository communityHouseRepository;

  private String generateUniqueId() {
    return UUID.randomUUID().toString();
  }

  @Override
  public Set<CommunityHouse> listAllHouses() {
    Set<CommunityHouse> communityHouses = new HashSet<>();
    communityHouseRepository.findAll().forEach(communityHouses::add);
    return communityHouses;
  }

  @Override
  public Set<CommunityHouse> listAllHouses(Pageable pageable) {
    Set<CommunityHouse> communityHouses = new HashSet<>();
    communityHouseRepository.findAll(pageable).forEach(communityHouses::add);
    return communityHouses;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
