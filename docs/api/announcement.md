### Announcements

**Endpoint: /announcements/**

*Allowed methods*: **GET**

**GET**

Shows you PYBOSSA wide announcements

-   **announcements**: Announcements
-   **template**: the rendered Announcements tamplate (currently empty)

**Example output**

```json
{
    "announcements": [
        {
            "body": "test123",
            "created": "2017-05-31T15:23:44.858735",
            "id": 5,
            "media_url": null,
            "published": true,
            "title": "title123",
            "updated": "2017-05-31T15:23:44.858735",
            "user_id": 4953
        },
        {
            "body": "new body",
            "created": "2017-05-31T15:23:28.477516",
            "id": 4,
            "media_url": null,
            "published": true,
            "title": "blogpost title",
            "updated": "2017-05-31T15:23:28.477516",
            "user_id": 4953
        },
        {
            "body": "new body",
            "created": "2017-06-01T23:42:45.042010",
            "id": 7,
            "media_url": null,
            "published": true,
            "title": "blogpost title",
            "updated": "2017-06-01T23:42:45.042010",
            "user_id": 4953
        },
        {
            "body": "new body",
            "created": "2017-06-01T23:45:11.612801",
            "id": 8,
            "media_url": null,
            "published": true,
            "title": "blogpost title",
            "updated": "2017-06-01T23:45:11.612801",
            "user_id": 4953
        }
    ],
    "csrf": "1504710446.52##6a7fakjsdhsdflkj",
    "template": "admin/announcement.html",
    "title": "Manage global Announcements"
}
```

### Admin announcement

**Endpoint: /admin/announcement**

**GET**

Shows you PYBOSSA wide announcements

-   **announcements**: Announcements
-   **csrf**: csrf token
-   **template**: the rendered Announcements tamplate (currently empty)
-   **title**: title of rendered endpoint

**Example output**

```json
{
    "announcements": [
        {
            "body": "test123",
            "created": "2017-05-31T15:23:44.858735",
            "id": 5,
            "media_url": null,
            "published": true,
            "title": "title123",
            "updated": "2017-05-31T15:23:44.858735",
            "user_id": 4953
        },
        {
            "body": "new body",
            "created": "2017-05-31T15:23:28.477516",
            "id": 4,
            "media_url": null,
            "published": true,
            "title": "blogpost title",
            "updated": "2017-05-31T15:23:28.477516",
            "user_id": 4953
        },
        {
            "body": "new body",
            "created": "2017-06-01T23:42:45.042010",
            "id": 7,
            "media_url": null,
            "published": true,
            "title": "blogpost title",
            "updated": "2017-06-01T23:42:45.042010",
            "user_id": 4953
        },
        {
            "body": "new body",
            "created": "2017-06-01T23:45:11.612801",
            "id": 8,
            "media_url": null,
            "published": true,
            "title": "blogpost title",
            "updated": "2017-06-01T23:45:11.612801",
            "user_id": 4953
        }
    ],
    "csrf": "1504710446.52##6a7fakjsdhsdflkj",
    "template": "admin/announcement.html",
    "title": "Manage global Announcements"
}
```

### Admin announcement new

**Endpoint: /admin/announcement/new**

*Allowed methods*: **GET/POST**

**GET**

Creates a new PYBOSSA wide announcement

-   **form**: form input
-   **template**: the rendered Announcements tamplate (currently empty)
-   **title**: title of rendered endpoint

**Example output**

```json
{
  "form": {
    "body": null,
    "csrf": "1496394903.81##bb5fb0c527955073ec9ad694ed9097e7c868272a",
    "errors": {},
    "media_url": null,
    "published": true,
    "title": null
  },
  "template": "admin/new_announcement.html",
  "title": "Write a new post"
}
```

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken". On success you will
get a 200 http code and following output:

**Example output**

```json
{
  "flash": "<i class=\"icon-ok\"></i> Annnouncement created!",
  "next": "/admin/announcement",
  "status": "success"
}
```

### Admin announcement update

**Endpoint: /admin/announcement/&lt;id&gt;/update**

*Allowed methods*: **GET/POST**

**GET**

Updates a PYBOSSA announcement

-   **form**: form input
-   **template**: the rendered Announcements tamplate (currently empty)
-   **title**: title of rendered endpoint

**Example output**

```json
{
  "form": {
    "body": "test6",
    "csrf": "1496328993.27##aa51e026938129afdfb0e6a5eab8c6b9427f81f6",
    "errors": {},
    "id": 4,
    "media_url": null,
    "published": true,
    "title": "test6"
  },
  "template": "admin/new_announcement.html",
  "title": "Edit a post"
}
```

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken". On success you will
get a 200 http code and following output:

**Example output**

```json
{
  "flash": "<i class=\"icon-ok\"></i> Announcement updated!",
  "next": "/admin/announcement",
  "status": "success"
}
```

### Admin announcement delete

**Endpoint: /admin/announcement/&lt;id&gt;/delete**

*Allowed methods*: **POST**

Deletes a PYBOSSA announcement

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken". You can get the token
from /admin/announcement On success you will get a 200 http code and
following output:

**Example output**

```json
{
  "flash": "<i class=\"icon-ok\"></i> Announcement deleted!",
  "next": "/admin/announcement",
  "status": "success"
}
```


