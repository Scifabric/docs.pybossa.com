### Project Category

**Endpoint: /project/category/&lt;short\_name&gt;/**

*Allowed methods*: **GET**

**GET**

Gives you the list of projects in a category.

-   **pagination**: A pagination object for getting projects from this
    category.
-   **active\_cat**: Active category.
-   **projects**: List of projects belonging to this category.
-   **categories**: List of available categories in this server.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "active_cat": {
    "created": null,
    "description": "Social projects",
    "id": 2,
    "name": "Social",
    "short_name": "social"
  },
  "categories": [
    {
      "created": null,
      "description": "Featured projects",
      "id": null,
      "name": "Featured",
      "short_name": "featured"
    },
    {
      "created": null,
      "description": "Social projects",
      "id": 2,
      "name": "Social",
      "short_name": "social"
    },
    {
      "created": "2013-06-18T11:13:44.789149",
      "description": "Art projects",
      "id": 3,
      "name": "Art",
      "short_name": "art"
    },
  ],
  "pagination": {
    "next": false,
    "page": 1,
    "per_page": 20,
    "prev": false,
    "total": 1
  },
  "projects": [
    {
      "created": "2014-02-22T15:09:23.691811",
      "description": "Image pattern recognition",
      "id": 1377,
      "info": {
        "container": "7",
        "thumbnail": "58.png"
      },
      "last_activity": "2 weeks ago",
      "last_activity_raw": "2017-01-31T09:18:28.450391",
      "n_tasks": 169671,
      "n_volunteers": 17499,
      "name": "Name",
      "overall_progress": 80,
      "owner": "John Doe",
      "short_name": "name",
      "updated": "2017-01-31T09:18:28.491496"
    },
  ],
  "template": "/projects/index.html",
  "title": "Projects"
}
```

!!! note
    To override the default ranking you pass the **orderby** query parameter to
    sort projects by any of the attributes listed above, such as
    *n\_volunteers* or *n\_tasks*. The **desc** query parameter can also
    be added to sort in descending order. For example: GET
    /project/category/&lt;short\_name&gt;/?orderby=n\_tasks&desc=True


### Project Category Featured

**Endpoint: /project/category/featured/**

*Allowed methods*: **GET**

**GET**

Gives you the list of featured projects.

-   **pagination**: A pagination object for getting new featured
    projects from this category.
-   **active\_cat**: Active category.
-   **projects**: List of projects belonging to this category.
-   **categories**: List of available categories in this server.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "active_cat": {
    "created": null,
    "description": "Featured projects",
    "id": null,
    "name": "Featured",
    "short_name": "featured"
  },
  "categories": [
    {
      "created": null,
      "description": "Featured projects",
      "id": null,
      "name": "Featured",
      "short_name": "featured"
    },
    {
      "created": null,
      "description": "Social projects",
      "id": 2,
      "name": "Social",
      "short_name": "social"
    },
    {
      "created": "2013-06-18T11:13:44.789149",
      "description": "Art projects",
      "id": 3,
      "name": "Art",
      "short_name": "art"
    },
  ],
  "pagination": {
    "next": false,
    "page": 1,
    "per_page": 20,
    "prev": false,
    "total": 1
  },
  "projects": [
    {
      "created": "2014-02-22T15:09:23.691811",
      "description": "Image pattern recognition",
      "id": 1377,
      "info": {
        "container": "7",
        "thumbnail": "58.png"
      },
      "last_activity": "2 weeks ago",
      "last_activity_raw": "2017-01-31T09:18:28.450391",
      "n_tasks": 169671,
      "n_volunteers": 17499,
      "name": "Name",
      "overall_progress": 80,
      "owner": "John Doe",
      "short_name": "name",
      "updated": "2017-01-31T09:18:28.491496"
    },
  ],
  "template": "/projects/index.html",
  "title": "Projects"
}
```

!!! note
    To override the default ranking you pass the **orderby** query parameter to
    sort projects by any of the attributes listed above, such as
    *n\_volunteers* or *n\_tasks*. The **desc** query parameter can also
    be added to sort in descending order. For example: GET
    /project/category/featured/?orderby=n\_tasks&desc=True


### Project Category Draft

**Endpoint: /project/category/draft/**

*Allowed methods*: **GET**

**GET**

Gives you the list of featured projects.

-   **pagination**: A pagination object for getting new draft projets
    from this category.
-   **active\_cat**: Active category.
-   **projects**: List of projects belonging to this category.
-   **categories**: List of available categories in this server.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "active_cat": {
    "created": null,
    "description": "Draft projects",
    "id": null,
    "name": "Draft",
    "short_name": "draft"
  },
  "categories": [
    {
      "created": null,
      "description": "Draft projects",
      "id": null,
      "name": "Draft",
      "short_name": "draft"
    },
    {
      "created": null,
      "description": "Social projects",
      "id": 2,
      "name": "Social",
      "short_name": "social"
    },
    {
      "created": "2013-06-18T11:13:44.789149",
      "description": "Art projects",
      "id": 3,
      "name": "Art",
      "short_name": "art"
    },
  ],
  "pagination": {
    "next": false,
    "page": 1,
    "per_page": 20,
    "prev": false,
    "total": 1
  },
  "projects": [
    {
      "created": "2014-02-22T15:09:23.691811",
      "description": "Draft 1",
      "id": 17,
      "info": {
        "container": "7",
        "thumbnail": "58.png"
      },
      "last_activity": "2 weeks ago",
      "last_activity_raw": "2017-01-31T09:18:28.450391",
      "n_tasks": 0,
      "n_volunteers": 0,
      "name": "Name",
      "overall_progress": 0,
      "owner": "John Doe",
      "short_name": "name",
      "updated": "2017-01-31T09:18:28.491496"
    },
  ],
  "template": "/projects/index.html",
  "title": "Projects"
}
```

!!! note
    To override the default ranking you pass the **orderby** query parameter to
    sort projects by any of the attributes listed above, such as
    *n\_volunteers* or *n\_tasks*. The **desc** query parameter can also
    be added to sort in descending order. For example: GET
    /project/category/draft/?orderby=n\_tasks&desc=True


