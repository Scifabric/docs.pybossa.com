### PYBOSSA server stats

**Endpoint: /stats/**

*Allowed methods*: **GET**

**GET**

Gives you the global stats of the PYBOSSA server.

-   **title**: the title for the endpoint.
-   **locs**: localizations for anonymous users that have contributed.
-   **projects**: statistics about total published and draft projects.
-   **show\_locs**: if GEOIP is enabled to show that data.
-   **stats**: Number of anonymous and authenticated users, number of
    draft and published projects, number of tasks, taskruns and total
    number of users.
-   **tasks**: Task and Taskrun statistics.
-   **tasks**: Task and Taskrun statistics.
-   **top\_5\_projects\_24\_hours**: Top 5 projects in the last 24
    hours.
-   **top\_5\_users\_24\_hours**: Top 5 users in the last 24 hours.
-   **users**: User statistics.

**Example output**

```json
{
  "locs": "[]",
  "projects": {
    "label": "Projects Statistics",
    "values": [
      {
        "label": "Published",
        "value": [
          0,
          534
        ]
      },
      {
        "label": "Draft",
        "value": [
          0,
          1278
        ]
      }
    ]
  },
  "show_locs": false,
  "stats": {
    "n_anon": 27587,
    "n_auth": 11134,
    "n_draft_projects": 1278,
    "n_published_projects": 534,
    "n_task_runs": 1801222,
    "n_tasks": 553012,
    "n_total_projects": 1812,
    "n_total_users": 38721
  },
  "tasks": {
    "label": "Task and Task Run Statistics",
    "values": [
      {
        "label": "Tasks",
        "value": [
          0,
          553012
        ]
      },
      {
        "label": "Answers",
        "value": [
          1,
          1801222
        ]
      }
    ]
  },
  "template": "/stats/global.html",
  "title": "Global Statistics",
  "top5_projects_24_hours": [],
  "top5_users_24_hours": [],
  "users": {
    "label": "User Statistics",
    "values": [
      {
        "label": "Anonymous",
        "value": [
          0,
          27587
        ]
      },
      {
        "label": "Authenticated",
        "value": [
          0,
          11134
        ]
      }
    ]
  }
}
```


