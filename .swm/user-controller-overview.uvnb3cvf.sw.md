---
title: User Controller Overview
---
This document will cover the User Controller in the MyHome project. We'll cover:

1. What is the User Controller
2. The main classes/functions/files that are related to User Controller

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/UserController.java" line="50">

---

# What is the User Controller

The User Controller is a class that facilitates user actions. It implements the UsersApi interface and contains methods for user operations such as sign up, listing all users, getting user details, managing user passwords, listing all housemates of a user, confirming email, and resending confirmation email.

```java
@RestController
@Slf4j
@RequiredArgsConstructor
public class UserController implements UsersApi {

  private final UserService userService;
  private final UserApiMapper userApiMapper;
  private final HouseService houseService;
  private final HouseMemberMapper houseMemberMapper;

  @Override
  public ResponseEntity<CreateUserResponse> signUp(@Valid CreateUserRequest request) {
    log.trace("Received SignUp request");
    UserDto requestUserDto = userApiMapper.createUserRequestToUserDto(request);
    Optional<UserDto> createdUserDto = userService.createUser(requestUserDto);
    return createdUserDto
        .map(userDto -> {
          CreateUserResponse response = userApiMapper.userDtoToCreateUserResponse(userDto);
          return ResponseEntity.status(HttpStatus.CREATED).body(response);
        })
        .orElseGet(() -> ResponseEntity.status(HttpStatus.CONFLICT).build());
```

---

</SwmSnippet>

<SwmSnippet path="/service/src/main/java/com/myhome/controllers/UserController.java" line="60">

---

# Main classes/functions/files related to User Controller

The `signUp` method is one of the main functions in the User Controller. It takes a CreateUserRequest object as input, maps it to a UserDto object, and calls the `createUser` method of the UserService. If the user is successfully created, it maps the UserDto object to a CreateUserResponse object and returns it with a CREATED status. If the user is not created, it returns a CONFLICT status.

```java
  @Override
  public ResponseEntity<CreateUserResponse> signUp(@Valid CreateUserRequest request) {
    log.trace("Received SignUp request");
    UserDto requestUserDto = userApiMapper.createUserRequestToUserDto(request);
    Optional<UserDto> createdUserDto = userService.createUser(requestUserDto);
    return createdUserDto
        .map(userDto -> {
          CreateUserResponse response = userApiMapper.userDtoToCreateUserResponse(userDto);
          return ResponseEntity.status(HttpStatus.CREATED).body(response);
        })
        .orElseGet(() -> ResponseEntity.status(HttpStatus.CONFLICT).build());
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXlob21lJTNBJTNBc3dpbW1pbw==" repo-name="myhome"><sup>Powered by [Swimm](/)</sup></SwmMeta>
