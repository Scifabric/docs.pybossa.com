### Home

**Endpoint: /**

*Allowed methods*: **GET**

**GET**

It returns a JSON object with the following information:

-   **top\_projects**: A list of the most active projects.
-   **categories\_projects**: A dictionary with all the published
    categories and its associated projects.
-   **categories**: All the available categories.
-   **template**: Jinja2 template.
-   **top\_users**: List of top contributors.

**Example output**

```json
{
  "categories": [
    {
      "created": null,
      "description": null,
      "id": null,
      "name": "Featured",
      "short_name": "featured"
    },
    {
      "description": "Economic projects",
      "id": 6,
      "name": "Economics",
      "short_name": "economics"
    },
  ],
  "categories_projects": {
    "economics": [
      {
        "description": "Description",
        "info": {
          "container": "user",
          "thumbnail": "415602833.png"
        },
        "n_tasks": 18,
        "n_volunteers": 26,
        "name": "Man made objects identity",
        "overall_progress": 0,
        "short_name": "manmadeobjectsidentity"
      },
    ],
  },
  "template": "/home/index.html",
  "top_projects": [
    {
      "description": "Image pattern recognition",
      "info": {
        "container": "user",
        "thumbnail": "772569.58.png"
      },
      "n_tasks": null,
      "n_volunteers": 17499,
      "name": "Name",
      "overall_progress": null,
      "short_name": "name"
    },
  ],
  "top_users": [
    {
      "created": "2014-08-17T18:28:56.738119",
      "fullname": "John Doe",
      "info": {
        "avatar": "1410771tar.png",
        "container": "05"
      },
      "n_answers": null,
      "name": "johndoe",
      "rank": 1,
      "registered_ago": null,
      "score": 54247
    },
  ]
}
```


