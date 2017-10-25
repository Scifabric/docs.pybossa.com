### Admin dashboard

\*\*Endpoint: /admin/dashboard/

*Allowed methods*: **GET**

**GET**

It shows the server statistics. You can use the argument *?refresh=1* to
update the data, as this data is only updated every 24 hours.

-   **active\_anon\_last\_week**: Active number of anonymous users in
    the server.
-   **published\_projects\_last\_week**: Published projects from the
    last week.
-   **new\_tasks\_week**: Number of new tasks created on the last week.
-   **update\_feed**: Activity feed of actions in the server.
-   **draft\_projects\_last\_week**: List of new draft projects created
    in the last week.
-   **update\_projects\_last\_week**: List of updated projects in the
    last week.
-   **new\_users\_week**: Number of new registered users in the last
    week.
-   **new\_task\_runs\_week**: Number of new task runs in the last week.
-   **returning\_users\_week**: Number of returning users per number of
    days in a row in the last week.
-   **active\_users\_last\_week**: Number of active users in the last
    week.
-   **wait**: This will be False if there's data, otherwise it will be
    True.

**Example output**

```json
{
  "active_anon_last_week": {
    "labels": [
      "2016-04-28"
    ],
    "series": [
      [
        0
      ]
    ]
  },
  "active_users_last_week": {
    "labels": [
      "2016-04-28"
    ],
    "series": [
      [
        1
      ]
    ]
  },
  "draft_projects_last_week": [
    {
      "day": "2016-04-27",
      "email_addr": "email",
      "id": id,
      "owner_id": id,
      "p_name": "name",
      "short_name": "name",
      "u_name": "name"
    },
    {
      "day": "2016-04-26",
      "email_addr": "email",
      "id": id,
      "owner_id": id,
      "p_name": "name",
      "short_name": "name",
      "u_name": "name"
    }
  ],
  "new_task_runs_week": {
    "labels": [
      "2016-04-28"
    ],
    "series": [
      [
        4
      ]
    ]
  },
  "new_tasks_week": {
    "labels": [
      "2016-04-26",
      "2016-04-28"
    ],
    "series": [
      [
        57,
        4
      ]
    ]
  },
  "new_users_week": {
    "labels": [
      "2016-04-27"
    ],
    "series": [
      [
        1
      ]
    ]
  },
  "published_projects_last_week": [],
  "returning_users_week": {
    "labels": [
      "1 day",
      "2 days",
      "3 days",
      "4 days",
      "5 days",
      "6 days",
      "7 days"
    ],
    "series": [
      [
        0,
        0,
        0,
        0,
        0,
        0,
        0
      ]
    ]
  },
  "template": "admin/dashboard.html",
  "title": "Dashboard",
  "update_feed": [],
  "update_projects_last_week": [
    {
      "day": "2016-04-28",
      "email_addr": "email",
      "id": id,
      "owner_id": id,
      "p_name": "name",
      "short_name": "name",
      "u_name": "name"
    },
    {
      "day": "2016-04-27",
      "email_addr": "email",
      "id": id,
      "owner_id": id,
      "p_name": "name",
      "short_name": "name",
      "u_name": "name"
    },
    {
      "day": "2016-04-26",
      "email_addr": "email",
      "id": id,
      "owner_id": id,
      "p_name": "name",
      "short_name": "name",
      "u_name": "name"
    },
  ],
  "wait": false
}
```


