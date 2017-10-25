### Admin featured projects

**Endpoint: /admin/featured**

*Allowed methods*: **GET**

**GET**

Gives you all featured projects on PYBOSSA.

-   **categories**: Gives you a list of categories where projects can be
    featured.
-   **form**: The form fields that need to be sent for feature and
    unfeature a project. It contains the CSRF token for validating the
    POST/DELETE.
-   **projects**: Featured projects grouped by categories.
-   **template**: The Jinja2 template that could be rendered.

**Example output**

```json
{
  "categories": [
    {
      "created": "2013-06-18T11:13:44.789149",
      "description": "Art projects",
      "id": 3,
      "name": "Art",
      "short_name": "art"
    },
    {
      "created": "2013-06-18T11:14:54.737672",
      "description": "Humanities projects",
      "id": 4,
      "name": "Humanities",
      "short_name": "humanities"
    },
    ...
  ],
  "projects": {
    "art": [
      {
        "created": "2013-12-10T06:54:48.222642",
        "description": "Description",
        "id": 1069,
        "info": {
          "container": "user_3738",
          "thumbnail": "app_1069_thumbnail_1410772175.32.png"
        },
        "last_activity": "just now",
        "last_activity_raw": null,
        "n_tasks": 13,
        "n_volunteers": 0,
        "name": "AAAA Test",
        "overall_progress": 0,
        "owner": "John Doe",
        "short_name": "AAAATest",
        "updated": "2014-11-05T14:55:07.564118"
      },
      ...
    ]
    "humanities": [
      {
        "created": "2014-10-21T12:20:51.194485",
        "description": "test project",
        "id": 2144,
        "info": {
          "container": null,
          "thumbnail": null
        },
        "last_activity": "2 years ago",
        "last_activity_raw": "2014-10-21T12:31:51.560422",
        "n_tasks": 9,
        "n_volunteers": 2,
        "name": "zak's test",
        "overall_progress": 0,
        "owner": "John Doe Cousin",
        "short_name": "cousintest",
        "updated": "2014-11-05T14:55:07.564118"
      },
      ...
    ]
  },
  "form": {
    "csrf": "secret_token_here"
  },
  "template": "/admin/projects.html"
}
```

### Admin un-/feature projects

**Endpoint: /admin/featured/&lt;int:project\_id&gt;**

*Allowed methods*: **POST / DELETE**

**POST**

Features a specific project.

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

**Example output**

On Success it will give you the project information

```json
{
  "info": {
    "task_presenter": "...",
    "container": "user_3738",
    "thumbnail": "app_1069_thumbnail_1410772175.32.png"
  },
  "updated": "2017-01-24T17:21:07.545983",
  "category_id": 3,
  "description": "Description",
  "short_name": "AAAATest",
  "created": "2013-12-10T06:54:48.222642",
  "webhook": null,
  "long_description": "AAAATest\n\n",
  "featured": false,
  "allow_anonymous_contributors": true,
  "published": true,
  "secret_key": "dfgojdsfgsgd",
  "owner_id": 3738,
  "contacted": null,
  "id": 1069,
  "name": "AAAA Test"
}
```

If a project is already featured:

```json
{
  "code": 400,
  "description": "CSRF token missing or incorrect.",
  "template": "400.html"
}
```

**DELETE**

Unfeatures a specific project.

To send a valid DELETE request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

**Example output**

On Success it will give you the project information

```json
{
  "info": {
    "task_presenter": "...",
    "container": "user_3738",
    "thumbnail": "app_1069_thumbnail_1410772175.32.png"
  },
  "updated": "2017-01-24T17:21:07.545983",
  "category_id": 3,
  "description": "Description",
  "short_name": "AAAATest",
  "created": "2013-12-10T06:54:48.222642",
  "webhook": null,
  "long_description": "AAAATest\n\n",
  "featured": false,
  "allow_anonymous_contributors": true,
  "published": true,
  "secret_key": "2ffgjngdf6bcbc38ba52561d4",
  "owner_id": 3738,
  "contacted": null,
  "id": 1069,
  "name": "AAAA Test"
}
```

If a project is already unfeatured:

```json
{
  "status_code": 415,
  "error": "Project.id 1069 is not featured"
}
```

