# Актёры (Actors)

Актёры это пользователи, боты, сервисные аккаунты и др. подобные вещи

У актёров есть свой inbox и outbox для получения и отправления объектов.

Они представленны JSON объекты.

См. примеры актёров ниже:

```json
{
  "@USNTP": "actor",
  "id": "https://example.com/alyss",
  "type": "USER",
  "localRole": "NRM",
  "preferredUsername": "Alyss",
  "summary": "Really cool person",
  "inbox": "https://example.com/alyss/inbox",
  "outbox": "https://example.com/alyss/outbox"
}
```

```json
{
  "@USNTP": "actor",
  "id": "https://example.com/remindMeBot",
  "type": "BOT",
  "localRole": "NRM",
  "author": "https://example.com/alyss",
  "preferredUsername": "RemindMe Bot",
  "summary": "Bot for creating reminds",
  "inbox": "https://example.com/remindMeBot/inbox",
  "outbox": "https://example.com/remindMeBot/outbox"
}
```

## ID [Mandatory]

ID это ссылка на профиль актёра

## Type [Mandatory]

Содержит тип актёра. Типы актёра:

- USER: Аккаунт обычного пользователя
- BOT: Бот созданный обычным пользователем
- SERVICE: Бот созданный сотрудниками сервера

## localRole [Non-Mandatory]

Роль контролируемая сервером этого актёра.
Должно быть один из следущих:

- NRM: Обычный актёр(бот/пользователь), никаких доп. прав
- MOD: Модератор
- ADM: Администртор (роль выше модератора)
- STF: Сотрудник (сотрудник сервера)

Например все модераторы ващего сервера должны быть отмечены как `MOD`, но это не обязательно.

`localRole` актёров других серверов не должна влиять на ваш сервер в целях безопасности, но это можно использовать для отображения

Если проще, это роль актёра на **его** сервере.

## author [Non-Mandatory] [Запрещено type != BOT]

**Только для ботов.** Актёр который создал бота. (не обязательно)

## preferredUsername [Non-Mandatory]

Отображаемое имя актёра.

## summary [Non-Mandatory]

Короткое описание актёра.

## inbox, outbox [Non-Mandatory]

Ссылка на Inbox и Outbox актёра.

Например:

```json
{
  "@USNTP": "actor",
  "id": "https://example.com/john",
  "type": "USER",
  "localRole": "NRM",
  "preferredUsername": "John",
  "summary": "Just chill guy :)",
  "inbox": "https://example.com/api/user/inbox/john"
}
```

Так inbox будет - `https://example.com/api/user/inbox/john` и outbox будет - `https://example.com/john/outbox`
