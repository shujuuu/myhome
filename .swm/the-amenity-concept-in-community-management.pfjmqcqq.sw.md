---
title: The Amenity Concept in Community Management
---
This document will cover the concept of 'Amenity' in the MyHome project. We'll cover:

1. What is an 'Amenity'
2. Main classes and functions related to 'Amenity'

<SwmSnippet path="/service/src/main/java/com/myhome/domain/Amenity.java" line="37">

---

# What is an 'Amenity'

The 'Amenity' class represents an amenity in a community. It has properties such as 'amenityId', 'name', 'description', 'price', and relationships with 'Community', 'CommunityHouse', and 'AmenityBookingItem'.

```java
@Entity
@AllArgsConstructor
@NoArgsConstructor
@Getter
@Setter
@With
@NamedEntityGraphs({
    @NamedEntityGraph(
        name = "Amenity.community",
        attributeNodes = {
            @NamedAttributeNode("community"),
        }
    ),
    @NamedEntityGraph(
        name = "Amenity.bookingItems",
        attributeNodes = {
            @NamedAttributeNode("bookingItems"),
        }
    )
})

```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/services/springdatajpa/AmenitySDJpaService.java" line="19">

---

# Main classes and functions related to 'Amenity'

The 'AmenitySDJpaService' class uses the 'Amenity' class to perform operations such as getting amenity details, listing all amenities, and updating amenities.

```java
import com.myhome.controllers.mapper.AmenityApiMapper;
import com.myhome.domain.Amenity;
import com.myhome.domain.Community;
import com.myhome.model.AmenityDto;
import com.myhome.repositories.AmenityRepository;
import com.myhome.repositories.CommunityRepository;
import com.myhome.services.AmenityService;
import com.myhome.services.CommunityService;
import java.util.HashSet;
import java.util.List;
import java.util.Optional;
import java.util.Set;
import java.util.stream.Collectors;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Service;

@Service
@RequiredArgsConstructor
public class AmenitySDJpaService implements AmenityService {

  private final AmenityRepository amenityRepository;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
