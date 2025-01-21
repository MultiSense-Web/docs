# Tutorials

This article explains how-to build social network with USNTP in mind.

## Building microblogging(X/Twitter-like) network

First you need to implement account system.
Every user must have username (to comply with actor's ID field), profile page, inbox and outbox.

I will write example implementation of USNTP on Java with [SparkJava](https://github.com/perwendel/spark).

```java

// User, YourDatabase etc. are just example classes for example code only. You can implement anything how you want if it compling with USNTP specifications

// package, imports omitted
import static spark.Spark.*;

public class Main {
    public static void main(String[] args) {
        port(80);
        get("/.well-known/usntp", wellKnown);
        get("/:username", profile);
        get("/$/:username", actor);
        get("/$/:username/inbox", actorInbox);
        get("/$/:username/outbox", actorOutbox);
    }


    public static final Route wellKnown = (request, response) -> {
        response.type("application/json");
        return "{\"@USNTP\": \".well-known\",\"contact\": \"contact@example.social\"}";
    };
    public static final Route profile = (request, response) -> {
        // return profile page html for user with request.params(":username") username
    };
    public static final Route profile = (request, response) -> {
        // return actor json for user with request.params(":username") username
        User user = YourDatabase.getUserByUsername(request.params(":username"));
        return "{\"@USNTP\": \"actor\",\"id\": \"" + user.getUsername() + "@example.com\",\"type\": \"" + user.getType() + "\",\"localRole\": \"" + user.getRoleID() + "\",\"preferredUsername\": \"" + user.getDisplayName() + "\",\"summary\": \"" + user.getBio() + "\"}"
    };
}
```
