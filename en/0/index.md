# USNTP

**Universal Social Network Transfer Protocol** allows social networks to sync posts between each other while being safe.

Protocol is represented by actors, objects and servers.

## .well-known

Any webserver implementing USNTP must have `./well-known/usntp` route.
That json like this:

```json
{
  "@USNTP": ".well-known",
  "contact": <EMAIL TO CONTACT OPERATORS OF THIS SOCIAL NETWORK>,
  "supported": [<NETWORK TYPES SUPPORTED BY SERVER>]
}
```

All fields here and mandatory.

Also check <a onclick="$to('netTypes')">Network types</a>.

## JSON Object format

All USNTP JSON objects **MUST** contain `@USNTP` key.

## Actors

Actors are users, bots, service accounts etc.

For more info <a onclick="$to('actors')">see full actors page</a>.
