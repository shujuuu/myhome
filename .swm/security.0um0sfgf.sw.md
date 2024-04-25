---
title: Security
---
&nbsp;

<SwmSnippet path="/service/src/main/java/com/myhome/security/AppUserDetailsService.java" line="35">

---

&nbsp;

```java
public class AppUserDetailsService implements UserDetailsService {
  private final UserRepository userRepository;
  private final UserMapper userMapper;

  @Override public UserDetails loadUserByUsername(String username)
      throws UsernameNotFoundException {

    com.myhome.domain.User user = userRepository.findByEmail(username);
    if (user == null) {
      throw new UsernameNotFoundException(username);
    }

    return new User(user.getEmail(),
        user.getEncryptedPassword(),
        true,
        true,
        true,
        true,
        Collections.emptyList());
  }

  public UserDto getUserDetailsByUsername(String username) {
    com.myhome.domain.User user = userRepository.findByEmail(username);
    if (user == null) {
      throw new UsernameNotFoundException(username);
    }
    return userMapper.userToUserDto(user);
  }
}

```

---

</SwmSnippet>

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
