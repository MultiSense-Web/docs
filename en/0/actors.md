# Actors

Actors are users, bots, service accounts etc.

They are represented by JSON objects.

Actor json must be avalible at `<your website domain>/$/<actor's username>`. For example actor json for user with username alyss on example.com social network must be avalible at `example.com/$/alyss`

See examples of actor below.

```json
{
  "@USNTP": "actor",
  "id": "alyss@example.com",
  "type": "USER",
  "localRole": "NRM",
  "preferredUsername": "Alyss",
  "summary": "Really cool person",
  "inbox": "https://example.com/$/alyss/inbox",
  "outbox": "https://example.com/$/alyss/outbox",
  "PKEY": "-----BEGIN CER..."
}
```

```json
{
  "@USNTP": "actor",
  "id": "remindMeBot@example.com",
  "type": "BOT",
  "localRole": "NRM",
  "author": "https://example.com/alyss",
  "preferredUsername": "RemindMe Bot",
  "summary": "Bot for creating reminds",
  "inbox": "https://example.com/remindMeBot/inbox",
  "outbox": "https://example.com/remindMeBot/outbox",
  "profile": "https://example.com/remindMeBot",
  "PKEY": "-----BEGIN CER..."
}
```

## ID field [Mandatory]

ID Field contains actor's username which must comply with following regex: `([a-zA-Z_\.][0-9a-zA-Z_\.]*)@([0-9a-zA-Z\.]*)` (PCRE2 regex flavor). [View on regex101](https://regex101.com/r/LiXLJY/1), where group 2 must be valid domain name social network hosted on.

## Type [Mandatory]

Contains actors type which must be one of following values:

- USER: Regular user's account
- BOT: Bot account created by some user
- SERVICE: Bot created and controlled by server

## localRole [Non-Mandatory]

Role controlled by server actor owned by.
Must be on of following:

- NRM: Just default user(bot/service/actor) with normal perms
- MOD: Moderator
- ADM: Admin
- STF: Staff

For example all your server's mods should be marked with `MOD` localRole.

`localRole` shouldn't affect any servers but actor's server for security reasons but it can be used for ui elements.

To be more simple **this is role of user at his server**

## profile [Non-Mandatory]

Link to actor's profile page

## author [Non-Mandatory] [Forbidden if type != BOT]

**Only for bots**. This is id of actor that created this bot.

## preferredUsername [Non-Mandatory]

Actor's display name. This should be used as actor's name in ui elements.

## summary [Non-Mandatory]

Actor's short description/bio.

## inbox, outbox [Non-Mandatory]

Actor's inbox and outbox urls. If not specified, `/$/ + id + /inbox` or `/$/ + id + /outbox` will be used.

For example:

```json
{
  "@USNTP": "actor",
  "id": "john@example.com",
  "type": "USER",
  "localRole": "NRM",
  "preferredUsername": "John",
  "summary": "Just chill guy :)",
  "inbox": "https://example.com/api/user/inbox/john"
}
```

Will cause inbox url to be `https://example.com/api/user/inbox/john` and outbox url be `https://example.com/$/john/outbox`

## PKEY [Mandatory]

PKEY field must be SSL Certificate
