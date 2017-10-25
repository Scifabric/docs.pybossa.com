### Admin categories

**Endpoint: /admin/categories**

*Allowed methods*: **GET/POST**

**GET**

It lists all the available categories. It returns a JSON object with the
following information:

-   **categories**: A list of categories.
-   **form**: A form with the CSRF key to add a new category.
-   **n\_projects\_per\_category**: A dictionary with the number of
    projects per category.

**Example output**

```json
{
  "categories": [
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
  "form": {
    "csrf": "token",
    "description": null,
    "errors": {},
    "id": null,
    "name": null
  },
  "n_projects_per_category": {
    "art": 41,
    "social": 182
  },
  "template": "admin/categories.html",
  "title": "Categories"
}
```

**POST**

It returns the same output as before, but if the form is valid, it will
return the new created Category. Use the CSRFToken for submitting the
data.

-   **categories**: A list of categories.
-   **form**: A form with the CSRF key to add a new category.
-   **n\_projects\_per\_category**: A dictionary with the number of
    projects per category.

**Example output**

```json
{
  "categories": [
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
    {
      "created": "now",
      "description": "new",
      "id": 4,
      "name": "new",
      "short_name": "new"
    },

  ],
  "form": {
    "csrf": "token",
    "description": "new",
    "errors": {},
    "name": "new"
  },
  "n_projects_per_category": {
    "art": 41,
    "social": 182,
    "new": 0
  },
  "template": "admin/categories.html",
  "title": "Categories"
}
```

### Admin categories delete

**Endpoint: /admin/categories/del/&lt;int:id&gt;**

*Allowed methods*: **GET/POST**

**GET**

It shows the category that will be deleted. It gives you the CSRF token
to do a POST and delete it.

-   **category**: The category to be deleted.
-   **form**: A form with the CSRF key to add a new category.

**Example output**

```json
{
  "category": {
    "created": "2017-01-24T13:08:09.873071",
    "description": "new",
    "id": 9,
    "name": "new",
    "short_name": "new"
  },
  "form": {
    "csrf": "token",
  },
  "template": "admin/del_category.html",
  "title": "Delete Category"
}
```

**POST**

It shows the category that will be deleted. It gives you the CSRF token
to do a POST and delete it.

-   **flash**: A human readable message about the action.
-   **next**: The next URL
-   **status**: The status of the POST.

**Example output**

```json
{
  "flash": "Category deleted",
  "next": "/admin/categories",
  "status": "success"
}
```

### Admin categories update

**Endpoint: /admin/categories/update/&lt;int:id&gt;**

*Allowed methods*: **GET/POST**

**GET**

It shows the category that will be updated. It gives you the CSRF token
to do a POST and update it.

-   **category**: The category to be deleted.
-   **form**: A form with the CSRF key to add a new category.

**Example output**

```json
{
  "category": {
    "created": "2017-01-24T13:08:09.873071",
    "description": "new",
    "id": 9,
    "name": "new",
    "short_name": "new"
  },
  "form": {
    "csrf": "token",
    'description': 'new',
    'errors': {},
    'id': 9,
    'name': 'new'
  },
  "template": "admin/update_category.html",
  "title": "Update Category"
}
```

**POST**

It updates the category. Use the CSRF token and form fields from the
previous action to update it.

-   **flash**: A human readable message about the action.
-   **next**: The next URL
-   **status**: The status of the POST.

**Example output**

```json
{
  "flash": "Category updated",
  "next": "/admin/categories",
  "status": "success"
}
```


