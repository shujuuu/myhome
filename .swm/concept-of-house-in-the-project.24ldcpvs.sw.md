---
title: Concept of House in the Project
---
This document will cover the concept of 'House' in the MyHome project. We'll cover:

1. What 'House' represents in the project
2. The main classes related to 'House'

<SwmSnippet path="/service/src/main/java/com/myhome/domain/CommunityHouse.java" line="36">

---

# What 'House' Represents

`CommunityHouse` is the main class representing a 'House' in the project. It contains fields such as `houseId`, `name`, `houseMembers` and `amenities`. `houseMembers` is a set of `HouseMember` objects representing the members of the house. `amenities` is a set of `Amenity` objects representing the amenities of the house.

```java
@Entity
@AllArgsConstructor
@NoArgsConstructor
@Getter
@Setter
@EqualsAndHashCode(of = {"houseId", "name"}, callSuper = false)
@NamedEntityGraphs({
    @NamedEntityGraph(
        name = "CommunityHouse.community",
        attributeNodes = {
            @NamedAttributeNode("community"),
        }
    ),
    @NamedEntityGraph(
        name = "CommunityHouse.houseMembers",
        attributeNodes = {
            @NamedAttributeNode("houseMembers"),
        }
    )
})
public class CommunityHouse extends BaseEntity {
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/domain/HouseMember.java" line="30">

---

# Main Classes Related to 'House'

`HouseMember` is a class representing a member of a house. It contains fields such as `memberId`, `name`, and `communityHouse`. `communityHouse` is a `CommunityHouse` object representing the house that the member belongs to.

```java
@Entity
@AllArgsConstructor
@NoArgsConstructor
@Data
@EqualsAndHashCode(callSuper = false, exclude = "communityHouse")
public class HouseMember extends BaseEntity {

  @With
  @Column(nullable = false, unique = true)
  private String memberId;

  @OneToOne(orphanRemoval = true)
  @JoinColumn(name = "document_id")
  private HouseMemberDocument houseMemberDocument;

  @With
  @Column(nullable = false)
  private String name;

  @ManyToOne
  private CommunityHouse communityHouse;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
