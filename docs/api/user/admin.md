### Admin users

**Endpoint: /admin/users**

*Allowed methods*: **GET/POST**

**GET**

It returns a JSON object with the following information:

-   **form**: A form for searching for users.
-   **found**: A list of found users according to a search.
-   **template**: Jinja2 template.
-   **users**: List of admin users.

**Example output**

```json
{
  "form": {
    "csrf": "token",
    "errors": {},
    "user": null
  },
  "found": [],
  "template": "/admin/users.html",
  "title": "Manage Admin Users",
  "users": [
    {
      "admin": true,
      "api_key": "key",
      "category": null,
      "ckan_api": null,
      "confirmation_email_sent": false,
      "created": "date",
      "email_addr": "email",
      "facebook_user_id": null,
      "flags": null,
      "fullname": "John Doe",
      "google_user_id": null,
      "id": 1,
      "info": {
        "avatar": "avatar.png",
        "container": "user_1"
      },
      "locale": "en",
      "name": "johndoe",
      "newsletter_prompted": false,
      "passwd_hash": "hash",
      "privacy_mode": true,
      "pro": false,
      "subscribed": true,
      "twitter_user_id": null,
      "valid_email": true
    },
  ]
}
```

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

It returns a JSON object with the following information:

-   **form**: A form with the submitted search.
-   **found**: A list of found users according to a search.
-   **template**: Jinja2 template.
-   **users**: List of admin users.

**Example output**

```json
{
  "form": {
    "csrf": "token",
    "errors": {},
    "user": 'janedoe',
  },
  "found": [
        {
          "admin": false,
          "api_key": "key",
          "category": null,
          "ckan_api": null,
          "confirmation_email_sent": false,
          "created": "date",
          "email_addr": "email",
          "facebook_user_id": null,
          "flags": null,
          "fullname": "janedoe",
          "google_user_id": null,
          "id": 80,
          "info": {},
          "locale": "en",
          "name": "janedoe",
          "newsletter_prompted": false,
          "passwd_hash": "hash",
          "privacy_mode": true,
          "pro": false,
          "subscribed": true,
          "twitter_user_id": null,
          "valid_email": true
        },
  ],
  "template": "/admin/users.html",
  "title": "Manage Admin Users",
  "users": [
    {
      "admin": true,
      "api_key": "key",
      "category": null,
      "ckan_api": null,
      "confirmation_email_sent": false,
      "created": "date",
      "email_addr": "email",
      "flags": null,
      "fullname": "John Doe",
      "id": 1,
      "info": {
        "avatar": "avatar.png",
        "container": "user_1"
      },
      "locale": "en",
      "name": "johndoe",
      "newsletter_prompted": false,
      "passwd_hash": "hash",
      "privacy_mode": true,
      "pro": false,
      "subscribed": true,
      "valid_email": true
    },
  ]
  }
```

### Admin users add

**Endpoint: /admin/users/add/&lt;int:user\_id&gt;**

*Allowed methods*: **GET**

**GET**

It adds a user to the admin group. It returns a JSON object with the
following information:

-   **next**: '/admin/users',

**Example output**

```json
{
  "next": "/admin/users",
}
```

!!! note
    You will need to use the /admin/users endpoint to get a list of users
    for adding deleting from the admin group.


### Admin users del

**Endpoint: /admin/users/del/&lt;int:user\_id&gt;**

*Allowed methods*: **GET**

**GET**

It removes a user from the admin group. It returns a JSON object with
the following information:

-   **next**: '/admin/users',

**Example output**

```json
{
  "next": "/admin/users",
}
```

!!! note
    You will need to use the /admin/users endpoint to get a list of users
    for adding deleting from the admin group.


